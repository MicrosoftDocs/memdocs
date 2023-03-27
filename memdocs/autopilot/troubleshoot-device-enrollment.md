---
title: Troubleshoot Autopilot device import and enrollment
description: Troubleshoot issues that can occur during Autopilot device import and enrollment.
ms.technology: itpro-deploy
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 11/17/2022
ms.collection: 
  - M365-modern-desktop
  - highpri
  - tier2
ms.topic: troubleshooting
---


# Troubleshoot Autopilot device import and enrollment

*Applies to:*

- Windows 11
- Windows 10

See the following sections for information about issues that can occur when importing and enrolling devices into Intune.

## Error code 0x80180014 when re-enrolling using self-deployment or pre-provisioning mode

After the first Autopilot deployment, devices with a targeted Autopilot self-deployment mode or pre-provisioning mode profile can't automatically re-enroll using Autopilot. If you try to redeploy the device, then the `0x80180014` error code is returned:

:::image type="content" source="./images/troubleshoot-device-enrollment/0x80180014-error-code-enrollment-status-page.png" alt-text="Enrollment status page shows 0x80180014 error code on devices using self-deployment mode or pre-provisioning mode.":::

:::image type="content" source="./images/troubleshoot-device-enrollment/0x80180014-error-code-pre-provisioning-page.png" alt-text="Pre-provisioning page shows 0x80180014 error code on devices using self-deployment mode or pre-provisioning mode.":::

The ETW logs may show the following error:

`MDM Enroll: Server Returned Fault/Code/Subcode/Value=(DeviceNotSupported) Fault/Reason/Text=(Enrollment blocked for AP device by SDM One Time Limit Check)`

### Cause A

Microsoft Endpoint Manager changed the Windows Autopilot self-deployment mode (Public Preview) and Pre-Provisioning mode (formerly known as white glove, in Public Preview) experience.
To reuse a device, you must delete the device record created by Intune.

This change impacts all Autopilot deployments that use the self-deployment or pre-provisioning mode. This change impacts devices when they're reused, reset, or when redeploying a profile.

#### Resolution A

To redeploy the device through Autopilot:

1. Delete the device record in Intune. For the specific steps, see [Delete devices from the Intune admin center](../intune/remote-actions/devices-wipe.md#delete-devices-from-the-intune-admin-center).
2. Redeploy the Autopilot deployment profile.

### Cause B

Windows MDM enrollment is disabled in your Intune tenant.

#### Resolution B

To fix this issue in a stand-alone Intune environment, follow these steps:

1. In the Microsoft Intune admin center, chooses **Devices** > **Enrollment restrictions**, and then choose a device type restriction.
1. Choose **Properties** > **Edit** next to Platform settings. Then select **Allow for Windows (MDM)**.
1. Select **Review** and then **Save**.

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

## Related articles

[Windows Autopilot - known issues](known-issues.md)<br>
[Diagnose MDM failures in Windows 10](/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10)<br>
