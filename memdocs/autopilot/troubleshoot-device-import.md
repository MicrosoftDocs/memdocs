---
title: Troubleshoot Autopilot device import
description: Troubleshoot issues that can occur during Autopilot device import
keywords: mdm, setup, windows, windows 10, oobe, manage, deploy, autopilot, ztd, zero-touch, partner, msfb, intune
ms.reviewer: mniehaus
manager: laurawi
ms.technology: windows
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: troubleshooting
---


## Troubleshoot Autopilot device import

**Applies to: Windows 10**

Windows Autopilot is designed to simplify all parts of the Windows device lifecycle, but there are always situations where issues may arise. Review the following information to assist with troubleshooting efforts.

## Clicking Import after selecting CSV does nothing, '400' error appears in network trace with error body **"Cannot convert the literal '[DEVICEHASH]' to the expected type 'Edm.Binary'"**

This error points to the device hash being incorrectly formatted. Anything that corrupts the collected hash can cause this error. One possibility is that the hash itself (even if it's valid) fails to be decoded.

The device hash is Base64. At the device level, it's encoded as unpadded Base64, but Autopilot expects padded Base64. Usually, the payload doesn't require padding and the process works. Sometimes, however, the payload doesn't line up cleanly and padding is necessary. In this case, you get the error displayed above. PowerShell's Base64 decoder also expects padded Base64, so we can use this decoder to validate that the hash is properly padded.

The "A" characters at the end of the hash are effectively empty data. Each character in Base64 is 6 bits, A in Base64 is 6 bits equal to 0. Deleting or adding **A**s at the end doesn't change the actual payload data.

To fix this issue, we'll need to modify the hash, then test the new value, until PowerShell succeeds in decoding the hash. The result is mostly illegible, which is fine. We're just looking for it to not throw the error "Invalid length for a Base-64 char array or string". 

To test the base64, you can use the following PowerShell:
```powershell
[System.Text.Encoding]::ascii.getstring( [System.Convert]::FromBase64String("DEVICE HASH"))
```

So, as an example (this isn't a device hash, but it's misaligned unpadded Base64 so it's good for testing):
```powershell
[System.Text.Encoding]::ascii.getstring( [System.Convert]::FromBase64String("Q29udG9zbwAAA"))
```

Now for the padding rules. The padding character is "=". The padding character can only be at the end of the hash, and there can only be a maximum of two padding characters. Here's the basic logic.

- Does decoding the hash fail?
 - Yes: Are the last two characters "="?
   - Yes: Replace both "=" with a single "A" character, then try again
   - No: Add another "=" character at the end, then try again
 - No: That hash is valid

Looping the logic above on the previous example hash, we get the following permutations:
- Q29udG9zbwAAA
- Q29udG9zbwAAA=
- Q29udG9zbwAAA==
- Q29udG9zbwAAAA
- Q29udG9zbwAAAA=
- **Q29udG9zbwAAAA==** (This one has valid padding)

Replace the collected hash with this new padded hash then try to import again.

## Related topics

[Windows Autopilot - known issues](known-issues.md)<br>
[Diagnose MDM failures in Windows 10](/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10)<br>