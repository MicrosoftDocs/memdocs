---
title: Windows Autopilot what's new
ms.reviewer: 
manager: laurawi
description: Read news and resources about the latest updates and past versions of Windows Autopilot.
keywords: mdm, setup, windows, windows 10, oobe, manage, deploy, autopilot, ztd, zero-touch, partner, msfb, intune, hololens
ms.technology: windows
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.date: 07/30/2021
ms.collection: M365-modern-desktop
ms.topic: article
---


# Windows Autopilot: What's new

**Applies to**

- Windows 10
- Windows 11
- Windows Holographic, version 2004

## [Preview] Windows Autopilot Diagnostics page

When you deploy Windows 11 with Autopilot, you can enable users to view additional detailed troubleshooting information about the Autopilot provisioning process. A new **Windows Autopilot Diagnostic Page** is available to provide IT admins and end users with a user-friendly view to troubleshoot Autopilot failures. 

An example of the diagnostic page is shown below. In this example, the user has expanded Configuration info and then clicks on Deployjment info to display details about Network Connectivity, Autopilot Settings, and Enrollment Status. The user also has the option to Export logs to perform detailed [troubleshooting](troubleshoot-oobe.md) analysis.

![diagnostics page start](images/oobe-tx-01.png)<br>
![diagnostics page click](images/oobe-tx-02.png)<br>
![diagnostics page expand](images/oobe-tx-03.png)

The diagnostics page can be enabled by going to the [ESP profile](/mem/intune/enrollment/windows-enrollment-status#available-settings) and selecting **Yes** to **Allow users to collect logs about installation errors**. 

The Autopilot diagnostic page is currently supported for commercial OOBE, and Autopilot user-driven mode. The new diagnostics page is only available on Windows 11, however Windows 10 users can still collect and export diagnostic logs when this setting is enabled in Intune. 

## Windows Autopilot for HoloLens 2

Windows Autopilot now enables you to configure HoloLens 2 devices! For more information, see [Windows Autopilot for HoloLens 2](/hololens/hololens2-autopilot).

## Feature name change

September, 2020

The Windows Autopilot white glove feature has been renamed to **Windows Autopilot for pre-provisioned deployment**. All references in our documentation to **white glove** have been replaced with: **pre-provisioning**.  The term **white glove** might still appear in some blogs and other articles about Windows Autopilot. These references correspond to the pre-provisioning process described in [this article](pre-provision.md).

## New in Windows 10, version 2004

With this release, you can configure Windows Autopilot [user-driven](user-driven.md) Hybrid Azure Active Directory join with VPN support. This support is also backported to Windows 10, version 1909 and 1903.

If you configure the language settings in the Autopilot profile and the device is connected to Ethernet, all scenarios will now skip the language, locale, and keyboard pages. In previous versions, this was only supported with self-deploying profiles.

## New in Windows 10, version 1903

[Windows Autopilot pre-provisioning](pre-provision.md) is new in Windows 10, version 1903. See the following video:

<br>

> [!VIDEO https://www.youtube.com/embed/nE5XSOBV0rI]

Also new in this version of Windows:
- The Intune enrollment status page (ESP) now tracks Intune Management Extensions.
- [Cortana voiceover and speech recognition during OOBE](windows-autopilot-scenarios.md#cortana-voiceover-and-speech-recognition-during-oobe) is disabled by default for all Windows 10 Pro Education, and Enterprise SKUs.
- [Windows Autopilot is self-updating during OOBE](windows-autopilot-scenarios.md#windows-autopilot-is-self-updating-during-oobe). Starting with the Windows 10, version 1903 Autopilot functional and critical updates will begin downloading automatically during OOBE.
- Windows Autopilot will set the diagnostics data level to Full during OOBE on devices running Windows 10 version 1903 or later. 

## New in Windows 10, version 1809

Windows Autopilot [self-deploying mode](self-deploying.md) is a zero touch device provisioning process. Simply power on the device, connect to Ethernet, and Autopilot automatically configures the device. End users don't have to press the "Next” button during the deployment process. 

You can use Windows Autopilot self-deploying mode to register the device to an AAD tenant, enroll in your organization’s MDM provider, and provision policies and applications. No user authentication or user interaction is required.

>[!NOTE]
>Window 10, version 1903 or later is required to use self-deploying mode due to issues with TPM device attestation in Windows 10, version 1809.

## Related topics

[What's new in Microsoft Intune](/intune/whats-new)<br>
[What's new in Windows 10](/windows/whats-new/)