---
title: Windows Autopilot resolved issues
ms.reviewer: 
manager: laurawi
description: Inform yourself about issues with Windows Autopilot deployment that can be resolved by applying the latest cumulative update.
keywords: mdm, setup, windows, windows 10, oobe, manage, deploy, autopilot, ztd, zero-touch, partner, msfb, intune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.date: 03/08/2021
ms.collection: M365-modern-desktop
ms.topic: troubleshooting
---


# Windows Autopilot - resolved issues

**Applies to**

- Windows 10

The following issues are resolved by installing Windows updates. For a list of issues that can be resolved through configuration changes, see [Windows Autopilot - known issues](known-issues).

<table>
<th>Cumulative update<th>Resolved issues
 
<tr><td><a href="https://support.microsoft.com/help/4517211/windows-10-update-kb4517211">KB4517211</a>.
<td>A missing AKI extension in EK certificate caused TPM attestation to fail on Windows 10 1903. This was due to an additional validation added in Windows 10 1903 to check that the TPM EK certs had the proper attributes according to the TCG specifications. The KB4517211 update removes this validation.

<tr><td><a href="https://support.microsoft.com/help/4512941">KB4512941</a>.

<td>The following known issues are resolved by installing the August 30, 2019 KB4512941 update (OS Build 18362.329):

- Windows Autopilot for existing devices feature doesn't properly suppress “Activities” page during OOBE. (Because of this issue, you’ll see that extra page during OOBE).
- TPM attestation state isn't cleared by sysprep /generalize, causing TPM attestation failure during later OOBE flow. (This isn’t a particularly common issue, but you could run into it while testing if you're running sysprep /generalize and then rebooting or reimaging the device to go back through an Autopilot pre-provisioning or self-deploying scenario).
- TPM attestation may fail if the device has a valid AIK cert but no EK cert. (This issue is related to the previous item).
- If TPM attestation fails during the Windows Autopilot pre-provisioning process, the landing page appears to be hung. (Basically, the pre-provisioning landing page, where you click “Provision” to start the pre-provisioning process, isn’t reporting errors properly).
- TPM attestation fails on newer Infineon TPMs (firmware version > 7.69). (Before this fix, only a specific list of firmware versions was accepted).
- Device naming templates may truncate the computer name at 14 characters instead of 15.
- Assigned Access policies cause a reboot, which can interfere with the configuration of single-app kiosk devices.


<tr><td><a href="https://support.microsoft.com/help/4505903">KB4505903</a>.

<td>The following known issues are resolved by installing the July 26, 2019 KB4505903 update (OS Build 18362.267):

- Windows Autopilot pre-provisioning doesn't work for a non-English OS and you see a red screen that says "Success."
- Windows Autopilot reports an AUTOPILOTUPDATE error during OOBE after sysprep, reset, or other variations. This issue typically happens if you reset the OS or used a custom sysprepped image.
- BitLocker encryption isn't correctly configured. Ex: BitLocker didn’t get an expected notification after policies were applied to begin encryption.
- You're unable to install UWP apps from the Microsoft Store, causing failures during Windows Autopilot. If you're deploying Company Portal as a blocking app during Windows Autopilot ESP, you’ve probably seen this error.
- A user isn't granted administrator rights in the Windows Autopilot user-driven Hybrid Azure AD join scenario. This is another non-English OS issue.

</table>

## Related topics

[Windows Autopilot - known issues](known-issues.md)<br>
[Diagnose MDM failures in Windows 10](/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10)<br>
[Troubleshooting Windows Autopilot](troubleshooting.md)