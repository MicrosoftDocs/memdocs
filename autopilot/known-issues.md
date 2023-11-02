---
title: Windows Autopilot known issues
description: Inform yourself about known issues that may occur during Windows Autopilot deployment.
ms.prod: windows-client
ms.technology: itpro-deploy
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 11/01/2023
ms.collection: 
  - M365-modern-desktop
  - highpri
  - tier2
ms.topic: troubleshooting
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Windows Autopilot - known issues

This article describes known issues that can often be resolved with configuration changes, through cumulative updates, or might be resolved automatically in a future release.

> [!NOTE]
>
> If you are experiencing issues with Autopilot with Co-management, see [Windows Autopilot with co-management](/mem/configmgr/comanage/autopilot-enrollment).

## Known issues

### Enrolled date for Autopilot device is incorrect

The **Enrolled date** in the **Devices | All devices** and **Windows | Windows devices** panes display the date the device was registered to Autopilot instead of the date it was enrolled to Autopilot. For a more accurate date for when the device enrolled to the tenant:

1. Use the Intune Graph API to query the device:

    `devices?$filter=physicalIds/any(p: startswith(p, '[ZTDID]'))&$select=id,deviceId,displayName,physicalIds,createdDateTime`

    For more information, see [Intune devices and apps API overview](/graph/intune-concept-overview) and [Working with Intune in Microsoft Graph ](/graph/api/resources/intune-graph-overview).

1. Use the Windows Autopilot deployment report for recently deployed devices.

### Filtering Windows Autopilot devices not working as expected

Viewing Windows Autopilot devices within Intune may not work as expected if you're attempting to filter results. While this issue is being worked on, a workaround is to use [Microsoft Graph API](/graph/use-the-api) to properly query and filter necessary devices.

### TPM attestation isn't working on some platforms with Infineon SLB9672 discrete TPMs

Platforms with the Infineon SLB9672 TPM with firmware release 15.22 with EK certificate may fail with error message **Something happened, and TPM attestation timed out.** To resolve this issue, contact your OEM for an update.

### Kiosk device profile not auto logging in

There's currently a known issue in the following Windows Updates released in January 2023:

- Windows 11 22H2: [KB5022303](https://support.microsoft.com/topic/january-10-2023-kb5022303-os-build-22621-1105-c45956c6-4ccb-4216-832c-2ec6309c7629)
- Windows 11 21H2: [KB5022287](https://support.microsoft.com/topic/january-10-2023-kb5022287-os-build-22000-1455-951898ec-2628-4d25-850e-9a44207bc139)
- Windows 10: [KB5022282](https://support.microsoft.com/topic/january-10-2023-kb5022282-os-builds-19042-2486-19044-2486-and-19045-2486-9587e4e3-c2d7-48a6-86e2-8cd9146b47fd)

where Kiosk device profiles that have auto sign-in enabled won't auto sign in. After Autopilot completes provisioning, the device stays on the sign-in screen prompting for credentials. To work around this known issue, you can manually enter the kiosk user credentials with the username `kioskUser0` and no password. After you enter this username with no password, it should take you to the desktop. This issue should be resolved in cumulative updates released for Windows 11 in April 2023 and Windows 10 in March 2023:

- Windows 11 22H2: [KB5025239](https://support.microsoft.com/topic/april-11-2023-kb5025239-os-build-22621-1555-5eaaaf42-bc4d-4881-8d38-97e0082a6982) or later.
- Windows 11 21H2: [KB5025224](https://support.microsoft.com/topic/april-11-2023-kb5025224-os-build-22000-1817-ebc75372-608d-4a77-a6e0-cb1e15f117fc) or later.
- Windows 10: [KB5023773](https://support.microsoft.com/topic/march-21-2023-kb5023773-os-builds-19042-2788-19044-2788-and-19045-2788-preview-5850ac11-dd43-4550-89ec-9e63353fef23) or later.


### TPM attestation isn't working on AMD platforms with ASP fTPM

TPM attestation for AMD platforms with ASP firmware TPM may fail with error code 0x80070490 on Windows 10 and Windows 11 systems. This issue is resolved on later versions of AMD firmware. Consult with device manufacturers and firmware release notes for which firmware versions contain the update.

### TPM attestation failure with error code 0x81039001

Some devices may intermittently fail TPM attestation during Windows Autopilot pre-provisioning technician flow or self-deployment mode with the error code 0x81039001 E_AUTOPILOT_CLIENT_TPM_MAX_ATTESTATION_RETRY_EXCEEDED. This failure occurs during the 'Securing your hardware' step for Windows Autopilot devices deployed using self-deploying mode or pre-provisioning mode. Subsequent attempts to provision may resolve the issue.

### Autopilot deployment report shows "failure" status on a successful deployment

The Autopilot deployment report (preview) shows a failed status for any device that experiences an initial deployment failure. For subsequent deployment attempts, using the **Try again** or **Continue to desktop** options, the deployment state in the report doesn't update. If the user resets the device, a new deployment row is shown in the report with the previous attempt remaining as failed.

### Autopilot deployment report doesn't show deployed device

Autopilot deployments that take longer than one hour may display an incomplete deployment status in the deployment report. If the device successfully enrolls but doesn't complete provisioning after more than one hour, the device status may not be updated in the report.

### Autopilot profile not being applied when assigned

In Windows 10 21H2 April 2022 and some May 2022 update releases, there's an issue where the Autopilot profile may fail to apply to the device. Additionally, the hardware hash may not be harvested. As a result, any settings made in the profile may not be configured for the user such as device renaming. To resolve this issue, apply [KB5015020](https://support.microsoft.com/topic/may-19-2022-kb5015020-os-builds-19042-1708-19043-1708-and-19044-1708-out-of-band-9b5bd38a-ab3c-4ada-96b0-b754134fcd2a) cumulative update or later to the device.

### DefaultuserX profile not deleted

When you use the [EnableWebSignIn CSP](/windows/client-management/mdm/policy-csp-authentication#authentication-enablewebsignin), the `defaultuserX` profile may not be deleted. 

### Autopilot reset ran into trouble. Could not find the recovery environment

When you attempt an Autopilot reset, you see the following message: **Autopilot reset ran into trouble. Could not find the recovery environment**. If there isn't an issue with the recovery environment, enter administrator credentials to continue with the reset process.

### Device-based Conditional Access policies

1. The Intune Enrollment app must be excluded from any Conditional Access policy requiring **Terms of Use** because it isn't supported.  See [Per-device terms of use](/azure/active-directory/conditional-access/terms-of-use#per-device-terms-of-use).

2. Exceptions to Conditional Access policies to exclude **Microsoft Intune Enrollment** and **Microsoft Intune** cloud apps are needed to complete Autopilot enrollment in cases where restrictive polices are present such as:

    - Conditional Access policy 1: Block all apps except those apps on an exclusion list.
    - Conditional Access policy 2: Require a compliant device for the apps on the exclusion list.

    In this case, Microsoft Intune Enrollment and Microsoft Intune should be included in that exclusion list of policy 1.

    If a policy is in place such that **all cloud apps** require a compliant device (there's no exclusion list), by default Microsoft Intune Enrollment is excluded, so that the device can register with Microsoft Entra ID and enroll with Intune and avoid a circular dependency.

3. **Hybrid Microsoft Entra devices**: When Hybrid Microsoft Entra devices are deployed with Autopilot, two device IDs are initially associated with the same device - one Microsoft Entra ID and one hybrid.  The hybrid compliance state displays as **N/A** when viewed from the devices list in the Azure portal until a user signs in. Intune only syncs with the Hybrid device ID after a successful user sign-in.

    The temporary **N/A** compliance state can cause issues with device based Conditional Access polices that block access based on compliance. In this case, Conditional Access is behaving as intended. To resolve the conflict, a user must to sign in to the device, or the device-based policy must be modified. For more information, see [Conditional Access: Require compliant or Microsoft Entra hybrid joined device](/azure/active-directory/conditional-access/howto-conditional-access-policy-compliant-device).

4. Conditional Access policies such as BitLocker compliance require a grace period for Autopilot devices. This grace period is needed because until the device has been rebooted, the status of BitLocker and Secure Boot haven't been captured. Since the status hasn't been captured, it can't be used as part of the Compliance Policy. The grace period can be as short as 0.25 days.

### Device goes through Autopilot deployment without an assigned profile

When a device is registered in Autopilot and no profile is assigned, the default Autopilot profile is taken. This behavior is by design. It makes sure that all devices that you register with Autopilot go through the Autopilot experience. If you don't want the device to go through an Autopilot deployment, remove the Autopilot registration.

<a name='white-screen-during-hybrid-azure-ad-joined-deployment'></a>

### White screen during Microsoft Entra hybrid joined deployment

There's a UI bug on Autopilot Microsoft Entra hybrid joined deployments where the Enrollment Status page is displayed as a white screen. This issue is limited to the UI and shouldn't affect the deployment process.

This issue was resolved in September 2022.

### Virtual machine failing at "Preparing your device for mobile management"

This error can be resolved by configuring your virtual machine with a minimum of 2 processors and 4 GB of memory.

### ODJConnectorSvc.exe leaks memory

When you use a proxy server with the ODJConnector service, the memory file can get too large when processing requests resulting in impacts to performance. The current workaround for this issue is to restart the ODJConnectSvc.exe service.

### Reset button causes pre-provisioning to fail on retry

When ESP fails during the pre-provisioning flow and the user selects the reset button, TPM attestation may fail during the retry.

### TPM attestation failure on Windows 11 error code 0x81039023

Some devices may fail TPM attestation on Windows 11 during the pre-provisioning technician flow or self-deployment mode with the error code **0x81039023**. This issue is resolved with the following cumulative updates released in May 2022:

- Windows 11: [KB5013943](https://support.microsoft.com/topic/may-10-2022-kb5013943-os-build-22000-675-14aa767a-aa87-414e-8491-b6e845541755).
- Windows 10: [KB5013942](https://support.microsoft.com/topic/may-10-2022-kb5013942-os-builds-19042-1706-19043-1706-and-19044-1706-60b51119-85be-4a34-9e21-8954f6749504).

<a name='duplicate-device-objects-with-hybrid-azure-ad-deployments'></a>

### Duplicate device objects with hybrid Microsoft Entra deployments

A device object is pre-created in Microsoft Entra ID once a device is registered in Autopilot. If a device goes through a hybrid Microsoft Entra deployment, by design, another device object is created resulting in duplicate entries.

### TPM attestation failure on Windows 11 error code 0x81039024

Some devices may fail TPM attestation on Windows 11 during the pre-provisioning technician flow or self-deployment mode with the error code 0x81039024. This error code indicates that there are known vulnerabilities detected with the TPM and as a result attestation fails. If you receive this error, visit your PC manufacturer's website to update the TPM firmware.

### Delete device record in Intune before reusing devices in self-deployment mode or Pre-Provisioning mode

You have devices enrolled using Autopilot self-deployment mode or pre-provisioning mode. If you redeploy a device so that it reruns the Autopilot deployment again, it fails with a `0x80180014` error code.

To resolve this error, use one of the following work around methods:

- Delete the device record in Intune, and then redeploy the device so that it reruns the Autopilot deployment. For more information, see [Deregister a device](registration-overview.md#deregister-a-device).
- Remove the device enrollment restriction for **Windows (MDM)** personally owned devices. For more information, see [Set enrollment restrictions in Microsoft Intune](/mem/intune/enrollment/enrollment-restrictions-set).<!-- MEMDocs #2748 -->

For more information on this issue, see [Troubleshoot Autopilot device import and enrollment](troubleshoot-device-enrollment.md).

### A non-assigned user can sign in when using user-driven mode with Active Directory Federation Services (ADFS)

In a Windows Autopilot user-driven Microsoft Entra joined environment, you can pre-assign a user to a device. If the user is a cloud-native Microsoft Entra account, the username is enforced and the user is only asked for their password. There's no way to sign in with another user ID. However, when ADFS is used, the username assignment isn't enforced. A different user than the one assigned can sign in on the device.

### Intune connector is inactive but still appears in the Intune Connectors

Inactive Intune connectors will be automatically cleaned up after 30 days of inactivity without admin interaction.

### Autopilot sign-in page displays HTML tags from company branding settings

When [customizations are applied to the company branding settings](/azure/active-directory/fundamentals/customize-branding#to-customize-your-branding), the HTML tags may be visible and not rendered correctly on the update password page. This issue should be fixed in future versions of Windows.

### TPM attestation isn't working on Intel Tiger Lake platforms

TPM attestation support for Intel firmware TPM Tiger Lake platforms is only supported on devices with Windows 10 version 21H2 or later. This issue should be resolved by applying the November 2021 cumulative update [KB5007253](https://support.microsoft.com/topic/november-22-2021-kb5007253-os-builds-19041-1387-19042-1387-19043-1387-and-19044-1387-preview-d1847be9-46c1-49fc-bf56-1d469fc1b3af) or later.

### Blocking apps specified in a user-targeted Enrollment Status Profile are ignored during device ESP

The services responsible for determining the list of apps that should be blocking during device ESP aren't able to determine the correct ESP profile containing the list of apps because they don't know the user identity. As a workaround, enable the default ESP profile (which targets all users and devices) and place the blocking app list there. To avoid this issue, target the ESP profile to [device groups](enrollment-autopilot.md).

### That username looks like it belongs to another organization. Try signing in again or start over with a different account

Confirm that all of your information is correct at `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Provisioning\Diagnostics\Autopilot`. For more information, see [Troubleshoot OOBE issues](troubleshoot-oobe.md#windows-10-version-1709-and-above).

<a name='windows-autopilot-user-driven-hybrid-azure-ad-deployments-dont-grant-users-administrator-rights-even-when-specified-in-the-windows-autopilot-profile'></a>

### Windows Autopilot user-driven hybrid Microsoft Entra deployments don't grant users Administrator rights even when specified in the Windows Autopilot profile

This issue occurs when there's another user on the device that already has Administrator rights. For example, a PowerShell script or policy could create another local account that is a member of the Administrators group. To ensure this works properly, don't create another account until after the Windows Autopilot process has completed.

### Windows Autopilot device provisioning can fail

These failures may be because of TPM attestation errors or ESP timeouts on devices where the real-time clock is off by a significant amount of time. For example, several minutes or more.

To fix this issue:

- Boot the device to the start of the out-of-box experience (OOBE).
- Establish a network connection (wired or wireless).
- Run the command `w32tm /resync /force` to sync the time with the default time server (`time.windows.com`).

### Windows Autopilot for existing devices doesn't work for Windows 10, version 1903 or 1909

You see screens that you've disabled in your Windows Autopilot profile, such as the Windows 10 License Agreement screen.

This issue happens because Windows 10, version 1903 and 1909 deletes the AutopilotConfigurationFile.json file.

To fix this issue:

- Edit the Configuration Manager task sequence and disable the **Prepare Windows for Capture** step.
- Add a new **Run command-line** step that runs `c:\windows\system32\sysprep\sysprep.exe /oobe /reboot`

For more information, see the blog post [A challenge with Windows Autopilot for existing devices and Windows 10 1903](https://oofhours.com/2019/09/19/a-challenge-with-windows-autopilot-for-existing-devices-and-windows-10-1903/).

### PushButtonReset (PBR) is taking machines to recovery mode with secure boot enabled: BSOD 0xC000000F

The **Enable with UEFI Lock** setting causes this behavior, and is enabled in the Intune Security Baseline. Issue occurs with 1909, this issue is fixed with later versions of Windows.

### Windows Autopilot self-deploying mode fails with an error code

For more information on this scenario, see [Windows Autopilot self-deploying mode](self-deploying.md).

| Error code | Description |
| ---------- | ----------- |
| 0x800705B4 | This general error indicates a timeout. A common cause of this error in self-deploying mode is that the device isn't TPM 2.0 capable. For example, it's a virtual machine. Devices that aren't TPM 2.0 capable can't be used with self-deploying mode. |
| 0x801c03ea | This error indicates that TPM attestation failed, causing a failure to join Microsoft Entra ID with a device token.
| 0xc1036501 | The device can't do an automatic MDM enrollment because there are multiple MDM configurations in Microsoft Entra ID. For more information, see the blog post [Inside Windows Autopilot self-deploying mode](https://oofhours.com/2019/10/01/inside-windows-autopilot-self-deploying-mode/). |

### Pre-provisioning gives an error screen and the **Microsoft-Windows-User Device Registration/Admin** event log displays **HResult error code 0x801C03F3**

This issue can happen if Microsoft Entra ID can't find a Microsoft Entra device object for the device that you're trying to deploy. This issue occurs if you manually delete the object. To fix it, remove the device from Microsoft Entra ID, Intune, and Autopilot, then re-register it with Autopilot, which recreates the Microsoft Entra device object

To get troubleshooting logs, run the following command: `Mdmdiagnosticstool.exe -area Autopilot;TPM -cab c:\autopilot.cab`

### Pre-provisioning gives an error screen

Pre-provisioning isn't supported on a VM.

### Error importing Windows Autopilot devices from a .csv file

Ensure that you haven't edited the .csv file in Microsoft Excel or an editor other than Notepad. Some of these editors can introduce extra characters causing the file format to be invalid.

### Windows Autopilot for existing devices doesn't follow the Autopilot OOBE experience

Ensure that the JSON profile file is saved in **ANSI/ASCII** format, not Unicode or UTF-8.

### **Something went wrong** is displayed page during OOBE

The client is likely unable to access all the required Azure AD/MSA-related URLs. For more information, see [Networking requirements](networking-requirements.md).

### Using a provisioning package in combination with Windows Autopilot can cause issues, especially if the PPKG contains join, enrollment, or device name information

Using PPKGs in combination with Windows Autopilot isn't recommended.

## Next steps

[Windows Autopilot - resolved issues](resolved-issues.md)

[Diagnose MDM failures in Windows 10](/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10)

[Troubleshooting Windows Autopilot](troubleshooting.md)

