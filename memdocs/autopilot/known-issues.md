---
title: Windows Autopilot known issues
description: Inform yourself about known issues that may occur during Windows Autopilot deployment.
keywords: mdm, setup, windows, windows 10, oobe, manage, deploy, autopilot, ztd, zero-touch, partner, msfb, intune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.reviewer: jubaptis
manager: dougeby
ms.date: 12/08/2021
ms.collection: M365-modern-desktop
ms.topic: troubleshooting
---

# Windows Autopilot - known issues

**Applies to**

- Windows 11
- Windows 10

This article describes known issues that can often be resolved by configuration changes, or might be resolved automatically in a future release. For information about issues that can be resolved by applying a cumulative update, see [Windows Autopilot - resolved issues](resolved-issues.md).

## Known issues

### Duplicate device objects with hybrid Azure AD deployments 

A device object is pre-created in Azure AD once a device is registered in Autopilot. If a device goes through a hybrid Azure AD deployment, by design, another device object is created resulting in duplicate entries. 

### TPM attestation failure on Windows 11 error code 0x81039024

Some devices may fail TPM attestation on Windows 11 during the pre-provisioning technician flow or self-deployment mode with the error code 0x81039024. This error code indicates that there are known vulnerabilities detected with the TPM and as a result will fail attestation. If you receive this error, please visit your PC manufacturer’s website to update the TPM firmware.

### Delete device record in Intune before reusing devices in self-deployment mode or Pre-Provisioning mode

You have devices enrolled using Autopilot self-deployment mode or pre-provisioning mode. If you redeploy an Autopilot profile, it fails with a `0x80180014` error code. To resolve this error, delete the device record in Intune, and then redeploy the profile.

For more information on this issue, see [Troubleshoot Autopilot device import and enrollment](troubleshoot-device-enrollment.md).

### A non-assigned user can sign in when using user-driven mode with Active Directory Federation Services (ADFS)

In a Windows Autopilot user-driven Azure Active Directory (Azure AD) joined environment, administrators can pre-assign a user to a device. If the user is a cloud-native Azure AD account, the username is enforced and the user is only asked for their password; there is no way to sign in with another user ID. However, when ADFS is used, the username assignment is not enforced. A different user than the one assigned can sign in on the device.

### Intune connector is inactive but still appears in the Intune Connectors

Inactive Intune connectors will be automatically cleaned up after 30 days of inactivity without admin interaction.

### Autopilot sign-in page displays HTML tags from company branding settings

When [customizations are applied to the company branding settings](/azure/active-directory/fundamentals/customize-branding#to-customize-your-branding) the HTML tags may be visible and not rendered correctly on the update password page. This issue should be fixed in future versions of Windows.

### TPM attestation is not working on Intel Tiger Lake platforms

TPM attestation support for Intel firmware TPM Tiger Lake platforms are only supported on devices with Windows 10 version 21H2 or higher.

### Blocking apps specified in a user-targeted Enrollment Status Profile are ignored during device ESP

The services responsible for determining the list of apps that should be blocking during device ESP aren't able to determine the correct ESP profile containing the list of apps because they don't know the user identity. As a workaround, enable the default ESP profile (which targets all users and devices) and place the blocking app list there. To avoid this issue, target the ESP profile to [device groups](enrollment-autopilot.md).

### That username looks like it belongs to another organization. Try signing in again or start over with a different account

Confirm that all of your information is correct at `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Provisioning\Diagnostics\AutoPilot`. For more information, see [Troubleshoot OOBE issues](troubleshoot-oobe.md#windows-10-version-1709-and-above).

### Windows Autopilot user-driven hybrid Azure AD deployments don't grant users Administrator rights even when specified in the Windows Autopilot profile

This issue will occur when there's another user on the device that already has Administrator rights. For example, a PowerShell script or policy could create another local account that is a member of the Administrators group. To ensure this works properly, don't create another account until after the Windows Autopilot process has completed.

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
| 0x801c03ea | This error indicates that TPM attestation failed, causing a failure to join Azure AD with a device token.
| 0xc1036501 | The device can't do an automatic MDM enrollment because there are multiple MDM configurations in Azure AD. For more information, see the blog post [Inside Windows Autopilot self-deploying mode](https://oofhours.com/2019/10/01/inside-windows-autopilot-self-deploying-mode/). |

### Pre-provisioning gives a red screen and the **Microsoft-Windows-User Device Registration/Admin** event log displays **HResult error code 0x801C03F3**

This issue can happen if Azure AD can't find an Azure AD device object for the device that you're trying to deploy. This issue will occur if you manually delete the object. To fix it, remove the device from Azure AD, Intune, and Autopilot, then re-register it with Autopilot, which will recreate the Azure AD device object

To get troubleshooting logs, run the following command: `Mdmdiagnosticstool.exe -area Autopilot;TPM -cab c:\autopilot.cab`

### Pre-provisioning gives a red screen

Pre-provisioning isn't supported on a VM.

### Error importing Windows Autopilot devices from a .csv file

Ensure that you haven't edited the .csv file in Microsoft Excel or an editor other than Notepad. Some of these editors can introduce extra characters causing the file format to be invalid.

### Windows Autopilot for existing devices doesn't follow the Autopilot OOBE experience

Ensure that the JSON profile file is saved in **ANSI/ASCII** format, not Unicode or UTF-8.

### **Something went wrong** is displayed page during OOBE

The client is likely unable to access all the required Azure AD/MSA-related URLs. For more information, see [Networking requirements](networking-requirements.md).

### Using a provisioning package in combination with Windows Autopilot can cause issues, especially if the PPKG contains join, enrollment, or device name information

Using PPKGs in combination with Windows Autopilot isn't recommended.

## Autopilot & Device-based Conditional Access policies
There should be a consideration for Conditional Access policies that enforce device compliance when Autopiloting Hybrid Azure AD Joined devices. There are 2 devices ID's for the same device name after the Autopilot process is completed (1 Azure AD Joined Device which is compliant and 1 Hybrid Azure AD Joined device whose compliance state says 'N/A', viewed from the Devices List on Azure Portal). The Intune service is only able to sync with the new device id that points to the Hybrid device once the user successfully sign-in's once. once this occurs, then the device ID pointing to the Hybrid Azure AD Joined device reports as 'Compliant'. This could cause issues for users in scope of a device-based Conditional Access policy that blocks based on compliance.


## Next steps

[Windows Autopilot - resolved issues](resolved-issues.md)

[Diagnose MDM failures in Windows 10](/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10)

[Troubleshooting Windows Autopilot](troubleshooting.md)
