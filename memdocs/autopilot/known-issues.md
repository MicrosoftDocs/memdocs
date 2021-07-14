---
title: Windows Autopilot known issues
ms.reviewer: 
manager: laurawi
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
ms.date: 07/13/2021
ms.collection: M365-modern-desktop
ms.topic: troubleshooting
---


# Windows Autopilot - known issues

**Applies to**

- Windows 10

The following table describes known issues that can often be resolved by configuration changes.  For information about issues that can be resolved by applying a cumulative update, see [Windows Autopilot - resolved issues](resolved-issues.md).

<table>
<th>Issue</th><th>More information</th>

<tr><td>Intune connector is inactive but still appears in the Intune Connectors blade</td>
<td>Inactive Intune connectors will be automatically cleaned up after 30 days of inactivity without admin interaction.</td></tr>

<tr><td>Autopilot sign-in page displays HTML tags from company branding settings</td>
<td>When <a href="/azure/active-directory/fundamentals/customize-branding#to-customize-your-branding">customizations are applied to the company branding settings</a> the HTML tags may be visible and not rendered correctly on the update password page. This issue should be fixed in future versions of Windows.</td></tr>
 
<tr><td>TPM attestation is not working on Intel Tiger Lake platforms when using firmware TPM.</td>
<td>TPM attestation support for Intel Tiger Lake firmware TPM is only supported with Windows 21H2 or higher.</td> </tr>

<tr><td>Blocking apps specified in a user-targeted Enrollment Status Profile are ignored during device ESP.</td>
<td>The services responsible for determining the list of apps that should be blocking during device ESP aren't able to determine the correct ESP profile containing the list of apps because they don't know the user identity. As a workaround, enable the default ESP profile (which targets all users and devices) and place the blocking app list there. To avoid this issue, target the ESP profile to <a href="enrollment-autopilot.md">device groups</a>.</td></tr>

<tr><td>That username looks like it belongs to another organization. Try signing in again or start over with a different account.</td>
 <td>Confirm that all of your information is correct at HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Provisioning\Diagnostics\AutoPilot. For more information, see <a href="troubleshoot-oobe.md#windows-10-version-1709-and-above">Troubleshoot OOBE issues</a>.</td></tr>

<tr><td>Windows Autopilot user-driven Hybrid Azure AD deployments don't grant users Administrator rights even when specified in the Windows Autopilot profile.</td>
<td>This issue will occur when there's another user on the device that already has Administrator rights. For example, a PowerShell script or policy could create another local account that is a member of the Administrators group. To ensure this works properly, don't create another account until after the Windows Autopilot process has completed.</td></tr>

<tr><td>Windows Autopilot device provisioning can fail with TPM attestation errors or ESP timeouts on devices where the real-time clock is off by a significant amount of time (for example, several minutes or more).</td>
<td>To fix this issue: <ol><li>Boot the device to the start of the out-of-box experience (OOBE).
<li>Establish a network connection (wired or wireless).
<li>Run the command <b>w32tm /resync /force</b> to sync the time with the default time server (time.windows.com).</ol>
 </td>
</tr>

<tr><td>Windows Autopilot for existing devices doesn't work for Windows 10, version 1903 or 1909; you see screens that you've disabled in your Windows Autopilot profile, such as the Windows 10 License Agreement screen.
<br>&nbsp;<br>
This issue happens because Windows 10, version 1903 and 1909 deletes the AutopilotConfigurationFile.json file.</td>
<td>To fix this issue: <ol><li>Edit the Configuration Manager task sequence and disable the <b>Prepare Windows for Capture</b> step.
<li>Add a new <b>Run command-line</b> step that runs <b>c:\windows\system32\sysprep\sysprep.exe /oobe /reboot</b>.</ol>
<a href="https://oofhours.com/2019/09/19/a-challenge-with-windows-autopilot-for-existing-devices-and-windows-10-1903/">More information</a></td></tr>
 
<tr><td>PushButtonReset (PBR) is taking machines to recovery mode with secure boot enabled: BSOD 0xC000000F.
<td>The “Enable with UEFI Lock” setting causes this behavior, and is enabled in the Intune Security Baseline. Issue occurs with 1909, this issue is fixed with later versions of Windows.</td></tr>

<tr><td>Windows Autopilot <a href="self-deploying.md">self-deploying mode</a> fails with an error code:
<td><table>
<tr><td>0x800705B4<td>This is a general error indicating a timeout. A common cause of this error in self-deploying mode is that the device isn't TPM 2.0 capable (ex: a virtual machine). Devices that aren't TPM 2.0 capable can't be used with self-deploying mode.
<tr><td>0x801c03ea<td>This error indicates that TPM attestation failed, causing a failure to join Azure Active Directory with a device token.
<tr><td>0xc1036501<td>The device can't do an automatic MDM enrollment because there are multiple MDM configurations in Azure AD. See <a href="https://oofhours.com/2019/10/01/inside-windows-autopilot-self-deploying-mode/">Inside Windows Autopilot self-deploying mode</a>.
</table>
<tr><td>Pre-provisioning gives a red screen and the <b>Microsoft-Windows-User Device Registration/Admin</b> event log displays <b>HResult error code 0x801C03F3</b><td>This issue can happen if Azure AD can’t find an Azure AD device object for the device that you're trying to deploy. This issue will occur if you manually delete the object. To fix it, remove the device from Azure AD, Intune, and Autopilot, then re-register it with Autopilot, which will recreate the Azure AD device object.<br> 
<br>To obtain troubleshooting logs, use: <b>Mdmdiagnosticstool.exe -area Autopilot;TPM -cab c:\autopilot.cab</b>
<tr><td>Pre-provisioning gives a red screen<td>Pre-provisioning isn't supported on a VM.
<tr><td>Error importing Windows Autopilot devices from a .csv file<td>Ensure that you haven't edited the .csv file in Microsoft Excel or an editor other than Notepad. Some of these editors can introduce extra characters causing the file format to be invalid. 
<tr><td>Windows Autopilot for existing devices doesn't follow the Autopilot OOBE experience.<td>Ensure that the JSON profile file is saved in <b>ANSI/ASCII</b> format, not Unicode or UTF-8.
<tr><td><b>Something went wrong</b> is displayed page during OOBE.<td>The client is likely unable to access all the required Azure AD/MSA-related URLs. For more information, see <a href="networking-requirements.md">Networking requirements</a>.
<tr><td>Using a provisioning package in combination with Windows Autopilot can cause issues, especially if the PPKG contains join, enrollment, or device name information.<td>Using PPKGs in combination with Windows Autopilot isn't recommended.
</table>

## Related topics

[Windows Autopilot - resolved issues](resolved-issues.md)<br>
[Diagnose MDM failures in Windows 10](/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10)<br>
[Troubleshooting Windows Autopilot](troubleshooting.md)