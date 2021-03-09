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

The following issues are resolved by installing Windows updates. For a list of issues that can be resolved through configuration changes, see [Windows Autopilot - known issues](known-issues.md).

| Applies to | Issues         | KB |
| :---         | :---         |  :---  |
|18362.145	|Autopilot pre-provisioning fails for non-English builds.	|[KB4497935](https://support.microsoft.com/help/4497935)|
|18362.207	|Bitlocker policies not enforced during Autopilot for non-default encryption options.	|[KB4501375](https://support.microsoft.com/help/4501375)|
|18362.267	|Windows Autopilot pre-provisioning doesn't work for a non-English OS and you see a red screen that says "Success."	|[KB4505903](https://support.microsoft.com/help/4505903)|
|18362.267	|Windows Autopilot reports an AUTOPILOTUPDATE error during OOBE after sysprep, reset, or other variations. This issue typically happens if you reset the OS or used a custom sysprepped image.	|[KB4505903](https://support.microsoft.com/help/4505903)|
|18362.267	|BitLocker encryption isn't correctly configured. Ex: BitLocker didn’t get an expected notification after policies were applied to begin encryption.	|[KB4505903](https://support.microsoft.com/help/4505903)|
|18362.267	|You're unable to install UWP apps from the Microsoft Store, causing failures during Windows Autopilot. If you're deploying Company Portal as a blocking app during Windows Autopilot ESP, you’ve probably seen this error.	|[KB4505903](https://support.microsoft.com/help/4505903)|
|18362.267	|A user isn't granted administrator rights in the Windows Autopilot user-driven Hybrid Azure AD join scenario. This is another non-English OS issue.	|[KB4505903](https://support.microsoft.com/help/4505903)|
|18362.329	|Windows Autopilot for existing devices feature doesn't properly suppress “Activities” page during OOBE. (Because of this issue, you’ll see that extra page during OOBE).	|[KB4512941](https://support.microsoft.com/help/4512941)|
|18363.329	|TPM attestation state isn't cleared by sysprep /generalize, causing TPM attestation failure during later OOBE flow. (This isn’t a particularly common issue, but you could run into it while testing if you're running sysprep /generalize and then rebooting or reimaging the device to go back through an Autopilot pre-provisioning or self-deploying scenario).	|[KB4512941](https://support.microsoft.com/help/4512941)|
|18364.329	|TPM attestation may fail if the device has a valid AIK cert but no EK cert. (This issue is related to the previous item).	|[KB4512941](https://support.microsoft.com/help/4512941)|
|18365.329	|If TPM attestation fails during the Windows Autopilot pre-provisioning process, the landing page appears to be hung. (Basically, the pre-provisioning landing page, where you click “Provision” to start the pre-provisioning process, isn’t reporting errors properly).	|[KB4512941](https://support.microsoft.com/help/4512941)|
|18366.329	|TPM attestation fails on newer Infineon TPMs (firmware version > 7.69). (Before this fix, only a specific list of firmware versions was accepted).	|[KB4512941](https://support.microsoft.com/help/4512941)|
|18367.329	|Device naming templates may truncate the computer name at 14 characters instead of 15.	|[KB4512941](https://support.microsoft.com/help/4512941)|
|18368.329	|Assigned Access policies cause a reboot, which can interfere with the configuration of single-app kiosk devices.	|[KB4512941](https://support.microsoft.com/help/4512941)|
|18362.387	|A missing AKI extension in EK certificate caused TPM attestation to fail on Windows 10 1903. This was due to an additional validation added in Windows 10 1903 to check that the TPM EK certs had the proper attributes according to the TCG specifications. The KB4517211 update removes this validation.	|[KB4517211](https://support.microsoft.com/help/4517211)|
|18362.449	|On self-deploying scenarios, the device is no longer AAD-joined after OOBE and cannot login with AAD credentials or access company resources.	|[KB4522355](https://support.microsoft.com/help/4522355) |
|18362.693, 18363.693	|For pre-provisioning scenarios, ESP is marked as required to show to ensure the technician flow completes successfully	|[KB4535996](https://support.microsoft.com/help/4535996) |
|18362.752, 18363.752	|For hybrid scenarios where the user should bean administrator, the user is forced to log off at the end of ESP so that user is part of the administrators group on the next logon	|[KB4541335](https://support.microsoft.com/help/4541335) |
|18362.752, 18363.752	|Improves the timeout algorithm on ESP to use processor ticks instead of the system time, which can drift if the device has not been powered on after a long duration.	|[KB4541335](https://support.microsoft.com/help/4541335) |
|18362.815, 18363.815	|Autopilot Reset state not set to success on completion, causing the MEM portal to not show the correct status of the device after reset. 	|[KB4550945](https://support.microsoft.com/help/4550945) |
|18362.815, 18363.815	|Enable additional log collection useful for support cases and investigations.	|[KB4550945](https://support.microsoft.com/help/4550945) |
|18362.815, 18363.815, 19041.488	|ESP takes a long time during the "Identifying" phase, especially in hybrid and pre-provisioning scenarios.	|[KB4550945](https://support.microsoft.com/help/4550945), [KB4571744](https://support.microsoft.com/help/4571744) |
|18362.815, 18363.815, 19041.488	|Autopilot Update disabled policy was not enforced during pre-provisioning scenarios.	|[KB4550945](https://support.microsoft.com/help/4550945), [KB4571744](https://support.microsoft.com/help/4571744) |
|18362.815, 18363.815, 19041.488	|Device setup category fails in self-deploying and pre-provisioning scenarios when the ESP policy is set to disabled.	|[KB4550945](https://support.microsoft.com/help/4550945), [KB4571744](https://support.microsoft.com/help/4571744) |
|18362.815, 18363.815, 19041.488	|Allows self-deploying scenarios to succeed even if multiple MDM providers are listed in AAD.	|[KB4550945](https://support.microsoft.com/help/4550945), [KB4571744](https://support.microsoft.com/help/4571744) |
|18362.815, 18363.815, 19041.488	|For self-deploying scenarios, a reboot causes the device to navigate to the pre-provisioning flow, even if the user did not select the pre-provisioning flow.	|[KB4550945](https://support.microsoft.com/help/4550945), [KB4571744](https://support.microsoft.com/help/4571744) |
|18362.836, 18363.836	|Devices with incompatible TPM versions (before v2.0), attestation times out instead of notifying the user of an incompatible hardware version	|[KB4556799](https://support.microsoft.com/help/4556799) |
|18362.1110, 18363.1110, 19041.488	|Microphone icon always shows in OOBE even on devices without audio/voiceover support.	|[KB4571744](https://support.microsoft.com/help/4571744), [KB4577062](https://support.microsoft.com/help/4577062)|
|18362.1237, 18363.1237, 19041.661, 19042.661	|The Privacy page isn't skipped during OOBE for some policy configurations.	|[KB4586819](https://support.microsoft.com/help/4586819), [KB4586853](https://support.microsoft.com/help/4586853)|
|18362.1237, 18363.1237, 19041.661, 19042.661	|Fixes issues during ESP when multiple policy providers are registered (e.g. IME and co-management)	|[KB4586819](https://support.microsoft.com/help/4586819), [KB4586853](https://support.microsoft.com/help/4586853)|
|18362.1237, 18363.1237, 19041.661, 19042.661	|For pre-provisioning scenarios, addresses an issue where the ESP seems to hang during Device Preparation category if a reboot occurs	|[KB4586819](https://support.microsoft.com/help/4586819), [KB4586853](https://support.microsoft.com/help/4586853)|
|19041.661, 19042.661	|ESP does not use the configured timeout value.	|[KB4586853](https://support.microsoft.com/help/4586853)|

## Related topics

[Windows Autopilot - known issues](known-issues.md)<br>
[Diagnose MDM failures in Windows 10](/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10)<br>
[Troubleshooting Windows Autopilot](troubleshooting.md)