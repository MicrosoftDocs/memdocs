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
ms.date: 12/16/2020
ms.collection: M365-modern-desktop
ms.topic: troubleshooting
---


# Windows Autopilot - known issues

**Applies to**

- Windows 10

<table>
<th>Issue<th>More information

<tr><td>TPM attestation failure on Windows 11 error code 0x81039024.</td>
<td>Some devices may fail TPM attestation on Windows 11 during the pre-provisioning technician flow or self-deployment mode with the error code 0x81039024. This error code indicates that there are known vulnerabilities detected with the TPM and as a result will fail attestation. If you receive this error, please visit your PC manufacturer’s website to update the TPM firmware.</tr>

<tr><td>Blocking apps specified in a user-targeted Enrollment Status Profile are ignored during device ESP.</td>
<td>The services responsible for determining the list of apps that should be blocking during device ESP aren't able to determine the correct ESP profile containing the list of apps because they don't know the user identity. As a workaround, enable the default ESP profile (which targets all users and devices) and place the blocking app list there. In the future, it will be possible to instead target the ESP profile to device groups to avoid this issue.</tr>

<tr><td>That username looks like it belongs to another organization. Try signing in again or start over with a different account.</td>
 <td>Confirm that all of your information is correct at HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Provisioning\Diagnostics\AutoPilot. For more information, see <a href="troubleshoot-oobe.md#windows-10-version-1709-and-above">Troubleshoot OOBE issues</a>.</td></tr>

<tr><td>Windows Autopilot user-driven Hybrid Azure AD deployments don't grant users Administrator rights even when specified in the Windows Autopilot profile.</td>
<td>This issue will occur when there's another user on the device that already has Administrator rights. For example, a PowerShell script or policy could create an additional local account that is a member of the Administrators group. To ensure this works properly, don't create an additional account until after the Windows Autopilot process has completed.</tr>

<tr><td>Windows Autopilot device provisioning can fail with TPM attestation errors or ESP timeouts on devices where the real-time clock is off by a significant amount of time (for example, several minutes or more).</td>
<td>To fix this issue: <ol><li>Boot the device to the start of the out-of-box experience (OOBE).
<li>Establish a network connection (wired or wireless).
<li>Run the command <b>w32tm /resync /force</b> to sync the time with the default time server (time.windows.com).</ol>
</tr>

<tr><td>Windows Autopilot for existing devices doesn't work for Windows 10, version 1903 or 1909; you see screens that you've disabled in your Windows Autopilot profile, such as the Windows 10 License Agreement screen.
<br>&nbsp;<br>
This issue happens because Windows 10, version 1903 and 1909 deletes the AutopilotConfigurationFile.json file.
<td>To fix this issue: <ol><li>Edit the Configuration Manager task sequence and disable the <b>Prepare Windows for Capture</b> step.
<li>Add a new <b>Run command line</b> step that runs <b>c:\windows\system32\sysprep\sysprep.exe /oobe /reboot</b>.</ol>
<a href="https://oofhours.com/2019/09/19/a-challenge-with-windows-autopilot-for-existing-devices-and-windows-10-1903/">More information</a></tr>
 
<tr><td>TPM attestation fails on Windows 10 1903 because of missing AKI extension in EK certificate. (An additional validation added in Windows 10 1903 to check that the TPM EK certs had the proper attributes according to the TCG specifications uncovered that a number of them don’t, so that validation will be removed).
<td>Download and install the <a href="https://support.microsoft.com/help/4517211/windows-10-update-kb4517211">KB4517211 update</a>.
<tr><td>The following known issues are resolved by installing the August 30, 2019 KB4512941 update (OS Build 18362.329):

- Windows Autopilot for existing devices feature doesn't properly suppress “Activities” page during OOBE. (Because of this issue, you’ll see that extra page during OOBE).
- TPM attestation state isn't cleared by sysprep /generalize, causing TPM attestation failure during later OOBE flow. (This isn’t a particularly common issue, but you could run into it while testing if you're running sysprep /generalize and then rebooting or reimaging the device to go back through an Autopilot pre-provisioning or self-deploying scenario).
- TPM attestation may fail if the device has a valid AIK cert but no EK cert. (This issue is related to the previous item).
- If TPM attestation fails during the Windows Autopilot pre-provisioning process, the landing page appears to be hung. (Basically, the pre-provisioning landing page, where you click “Provision” to start the pre-provisioning process, isn’t reporting errors properly).
- TPM attestation fails on newer Infineon TPMs (firmware version > 7.69). (Before this fix, only a specific list of firmware versions was accepted).
- Device naming templates may truncate the computer name at 14 characters instead of 15.
- Assigned Access policies cause a reboot, which can interfere with the configuration of single-app kiosk devices.
<td>Download and install the <a href="https://support.microsoft.com/help/4512941">KB4512941 update</a>. <br><br>See the section: <b>How to get this update</b> for information on specific release channels you can use to obtain the update.
<tr><td>The following known issues are resolved by installing the July 26, 2019 KB4505903 update (OS Build 18362.267):

- Windows Autopilot pre-provisioning doesn't work for a non-English OS and you see a red screen that says "Success."
- Windows Autopilot reports an AUTOPILOTUPDATE error during OOBE after sysprep, reset, or other variations. This issue typically happens if you reset the OS or used a custom sysprepped image.
- BitLocker encryption isn't correctly configured. Ex: BitLocker didn’t get an expected notification after policies were applied to begin encryption.
- You're unable to install UWP apps from the Microsoft Store, causing failures during Windows Autopilot. If you're deploying Company Portal as a blocking app during Windows Autopilot ESP, you’ve probably seen this error.
- A user isn't granted administrator rights in the Windows Autopilot user-driven Hybrid Azure AD join scenario. This is another non-English OS issue.
<td>Download and install the <a href="https://support.microsoft.com/help/4505903">KB4505903 update</a>. <br><br>See the section: <b>How to get this update</b> for information on specific release channels you can use to obtain the update.
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

[Diagnose MDM failures in Windows 10](/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10)<br>
[Troubleshooting Windows Autopilot](troubleshooting.md)