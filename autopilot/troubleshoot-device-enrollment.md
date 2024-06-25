---
title: Troubleshoot Autopilot device import and enrollment
description: Troubleshoot issues that can occur during Autopilot device import and enrollment.
ms.subservice: itpro-deploy
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/25/2024
ms.collection:
  - M365-modern-desktop
  - highpri
  - tier2
ms.topic: troubleshooting
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Troubleshoot Autopilot device import and enrollment

See the following sections for information about issues that can occur when importing and enrolling devices into Intune.

## Error code 0x80180014 when re-enrolling using self-deployment or pre-provisioning mode

After the first Autopilot deployment, devices with a targeted Autopilot self-deployment mode or pre-provisioning mode profile can't automatically re-enroll using Autopilot. If device is redeployed, then the `0x80180014` error code is returned.

The Event Tracing for Windows (ETW) logs might show the following mobile device management (MDM) error:

`MDM Enroll: Server Returned Fault/Code/Subcode/Value=(DeviceNotSupported) Fault/Reason/Text=(Enrollment blocked for AP device by SDM One Time Limit Check)`

### Cause A for error code 0x80180014

Microsoft Intune changed the Windows Autopilot self-deployment mode and Pre-Provisioning mode experience. To reuse a device, the device record created by Intune must be deleted.

This change impacts all Autopilot deployments that use the self-deployment or pre-provisioning mode. This change impacts devices when they're reused, reset, or when redeploying a profile.

### Resolution A for error code 0x80180014

To redeploy the device through Autopilot:

1. Delete the device record in Intune. For the specific steps, see [Delete devices from the Intune admin center](/mem/intune/remote-actions/devices-wipe#delete-devices-from-the-intune-admin-center).
1. Redeploy the Autopilot deployment profile.

### Cause B for error code 0x80180014

Windows MDM enrollment is disabled in the Intune tenant.

### Resolution B for error code 0x80180014

To fix this issue in a stand-alone Intune environment, follow these steps:

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices**.

1. In the **Devices | Overview** screen, under **Device onboarding** select **Enrollment**.

1. In the **Devices | Enrollment** screen:

   1. Verify that **Windows** is selected at the top of the page.

   1. Under **Enrollment options**, select **Device platform restriction**.

1. In the **Enrollment restrictions** screen, under **Device type restrictions**, select **All Users** under the **Name** column.

1. In the **All Users** screen that opens, under **Manage**, select **Properties**.

1. In the **Properties** screen that opens, next to **Platform settings**, select the **Edit** link.

1. In the **Edit restriction** screen that opens:

   1. Locate **Windows (MDM)** under the **Type** column.

   1. Make sure that **Windows (MDM)** is set to **Allow** under the **Platform** column.

   1. If **Windows (MDM)** is set to **Block**, change it to **Allow**.

   1. Select **Review + save**, and then either **Save** if a setting was changed, or **Cancel** if not settings were changed.

1. Repeat the above steps for any additional restrictions that might exist in the **Enrollment restrictions** screen other than **All Users**. Only restrictions for the **Windows** platform need to be verified.

> [!NOTE]
>
> When multiple restrictions exist, restrictions might exist that only allow certain groups MDM enrollment. Some of the restrictions blocking MDM enrollment might be valid based on what group they're assigned to. When experiencing this problem, verify that the device isn't a member of one of the groups where there's MDM enrollment is blocked, or if applicable, change the MDM enrollment setting for that restriction to **Allow**.

## Device import issues

### Cannot convert device hash error

- Selecting **Import** after selecting a CSV file doesn't do anything.
- A **400** error appears in network trace with error body **"Cannot convert the literal '[DEVICEHASH]' to the expected type 'Edm.Binary'**.

#### Cause of Cannot convert device hash error

This error points to the device hash being incorrectly formatted. Anything that corrupts the collected hash can cause this error. One possibility is that the hash itself (even if it's valid) fails to be decoded.

#### Explanation of Cannot convert device hash error

The device hash is Base64. At the device level, it's encoded as unpadded Base64, but Autopilot expects padded Base64. Usually, the payload doesn't require padding and the process works. Sometimes, however, the payload doesn't line up cleanly and padding is necessary. In this case, the above error is displayed. PowerShell's Base64 decoder also expects padded Base64, so we can use this decoder to validate that the hash is properly padded.

The "A" characters at the end of the hash are effectively empty data. Each character in Base64 is 6 bits. A in Base64 is 6 bits equal to 0. Deleting or adding **A**s at the end doesn't change the actual payload data.

#### Resolution for Cannot convert device hash error

To fix this issue, the hash needs to be modified, then the new value tested, until PowerShell succeeds in decoding the hash. The result is mostly illegible, which is fine. We're just looking for it to not throw the error **Invalid length for a Base-64 char array or string**.

To test the base64, use the following PowerShell:

```powershell
[System.Text.Encoding]::ascii.getstring( [System.Convert]::FromBase64String("DEVICE HASH"))
```

So, as an example:

```powershell
[System.Text.Encoding]::ascii.getstring( [System.Convert]::FromBase64String("Q29udG9zbwAAA"))
```

This particular example isn't a device hash, but it's a misaligned unpadded Base64 so it's good for testing.

Now for the padding rules. The padding character is "=". The padding character can only be at the end of the hash, and there can only be a maximum of two padding characters. Here's the basic logic.

- Does decoding the hash fail?
  - Yes: Are the last two characters "="?
    - Yes: Replace both "=" with a single "A" character, then try again
    - No: Add another "=" character at the end, then try again
- No: That hash is valid

Looping the above logic on the previous example hash, we get the following permutations:

- Q29udG9zbwAAA
- Q29udG9zbwAAA=
- Q29udG9zbwAAA==
- Q29udG9zbwAAAA
- Q29udG9zbwAAAA=
- **Q29udG9zbwAAAA==** (This one has valid padding)

Replace the collected hash with this new padded hash then try to import again.

## Autopilot profile not applied after reimaging to an older OS version

If a device is enrolled with one of the following Windows versions:

- Windows 11 with Windows Update [KB5017383](https://support.microsoft.com/topic/september-20-2022-kb5017383-os-build-22000-1042-preview-62753265-68e9-45d2-adcb-f996bf3ad393) or later
- Windows 10 with Windows Update [KB5015878](https://support.microsoft.com/topic/july-26-2022-kb5015878-os-builds-19042-1865-19043-1865-and-19044-1865-preview-549f5551-fcc5-4fee-8811-c5df12e04d40) or later

and then reimage to an older OS version, the Autopilot profile isn't applied. The device would need to be re-registered to complete a successful Autopilot deployment. The message **Fix pending** or **Attention required** might be displayed in the Autopilot devices page, which indicates that there was a hardware change on the device. When the link for the **Fix pending** status is selected, the following message appears:

**We've detected a hardware change on this device. We're trying to automatically register the new hardware. You don't need to do anything now; the status will be updated at the next check in with the result.**

### Cause of Autopilot profile not applied after reimaging to an older OS version

The Autopilot profile not applying after a device is reimaged to an older OS version is expected behavior when there's a hardware change on the device. For more information, see [Return of key functionality for Windows Autopilot sign-in and deployment experience](https://techcommunity.microsoft.com/t5/intune-customer-success/return-of-key-functionality-for-windows-autopilot-sign-in-and/ba-p/3583130).

### Resolution of Autopilot profile not applied after reimaging to an older OS version

When a device is reimaged to an older OS version after a hardware change on a device, deregister and re-register the device. For more information including how to deregister a device, see the following articles:

- [Windows Autopilot motherboard replacement scenario guidance](autopilot-motherboard-replacement.md).
- [Deregister a device](registration-overview.md#deregister-a-device).

<!-- MAXADO-8911669 -->

## Device appears as Microsoft Entra registered instead of Microsoft Entra joined

When checking the **Join type** of a device that has been joined to Microsoft Entra ID, it shows **Microsoft Entra registered** instead of **Microsoft Entra joined**.

### Cause of device appearing as Microsoft Entra registered instead of Microsoft Entra joined

This issue occurs if the device was previously registered in Microsoft Entra ID, for example via a [Workplace join](/entra/identity/devices/concept-device-registration), before it was joined to Microsoft Entra ID. If the Microsoft Entra ID registered device isn't deleted from Microsoft Entra ID before it's joined to Microsoft Entra ID, then the previous trust type is retained in the record. Joining an existing Microsoft Entra registered device to Microsoft Entra ID results in the Windows Autopilot device showing as **Microsoft Entra registered** instead of **Microsoft Entra joined**.

### Resolution for device appearing as Microsoft Entra registered instead of Microsoft Entra joined

Before registering an existing Microsoft Entra ID registered devices as Windows Autopilot devices, make sure that any existing Microsoft Intune, Microsoft Entra ID, and Windows Autopilot device objects are deleted. After all device objects are deleted, re-register the device as a Windows Autopilot device and then re-enroll the device. For more information on properly deleting all of the device objects, see [Deregister a device](registration-overview.md#deregister-a-device).

## Intune enrollment issues

See [Troubleshooting Windows device enrollment errors in Intune](/troubleshoot/mem/intune/device-enrollment/troubleshoot-windows-enrollment-errors) for assistance with Intune enrollment issues. Common issues can include:

- Incorrect or missing licenses assigned to the user.
- Too many devices enrolled for the user.

Error code 80180018 is typically reported on an error page titled **Something went wrong**. This error means that the MDM enrollment failed.

If Autopilot Reset fails immediately with the error **Ran into trouble. Please sign in with an administrator account to see why and reset manually**, see [Troubleshoot Autopilot Reset](/education/windows/autopilot-reset#troubleshoot-autopilot-reset) for more help.

## Related content

- [Windows Autopilot - known issues](known-issues.md).
- [Collect MDM logs](/windows/client-management/mdm-collect-logs).
