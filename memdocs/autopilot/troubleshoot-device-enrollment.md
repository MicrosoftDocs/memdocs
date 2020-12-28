---
title: Troubleshoot Autopilot device import and enrollment
description: Troubleshoot issues that can occur during Autopilot device import and enrollment
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
ms.date: 12/17/2020
ms.collection: M365-modern-desktop
ms.topic: troubleshooting
---


# Troubleshoot Autopilot device import and enrollment

**Applies to: Windows 10**

See the following topics for information about issues that can occur when importing and enrolling devices into Intune.

## Device import issues

### Cannot convert device hash error

#### Description

- Clicking Import after selecting CSV does nothing 
- A **400** error appears in network trace with error body **"Cannot convert the literal '[DEVICEHASH]' to the expected type 'Edm.Binary'**

#### Cause

This error points to the device hash being incorrectly formatted. Anything that corrupts the collected hash can cause this error. One possibility is that the hash itself (even if it's valid) fails to be decoded.

#### Explanation

The device hash is Base64. At the device level, it's encoded as unpadded Base64, but Autopilot expects padded Base64. Usually, the payload doesn't require padding and the process works. Sometimes, however, the payload doesn't line up cleanly and padding is necessary. In this case, you get the error displayed above. PowerShell's Base64 decoder also expects padded Base64, so we can use this decoder to validate that the hash is properly padded.

The "A" characters at the end of the hash are effectively empty data. Each character in Base64 is 6 bits, A in Base64 is 6 bits equal to 0. Deleting or adding **A**s at the end doesn't change the actual payload data.

#### Resolution

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

## Intune enrollment issues

See [this knowledge base article](https://support.microsoft.com/help/4089533/troubleshooting-windows-device-enrollment-problems-in-microsoft-intune) for assistance with Intune enrollment issues. Common issues can include"
- incorrect or missing licenses assigned to the user.
- too many devices enrolled for the user.

Error code 80180018 will typically be reported on an error page titled "Something went wrong". This error means that the MDM enrollment failed.

If Autopilot Reset fails immediately with the error **Ran into trouble. Please sign in with an administrator account to see why and reset manually**, see [Troubleshoot Autopilot Reset](/education/windows/autopilot-reset#troubleshoot-autopilot-reset) for more help.

## Related topics

[Windows Autopilot - known issues](known-issues.md)<br>
[Diagnose MDM failures in Windows 10](/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10)<br>