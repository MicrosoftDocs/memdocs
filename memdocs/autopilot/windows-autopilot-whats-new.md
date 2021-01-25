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
ms.date: 12/16/2020
ms.collection: M365-modern-desktop
ms.topic: article
---


# Windows Autopilot: What's new

**Applies to**

- Windows 10
- Windows Holographic, version 2004


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