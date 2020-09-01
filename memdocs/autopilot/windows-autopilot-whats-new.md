---
title: Windows Autopilot what's new
ms.reviewer: 
manager: laurawi
description: Read news and resources about the latest updates and past versions of Windows Autopilot.
keywords: mdm, setup, windows, windows 10, oobe, manage, deploy, autopilot, ztd, zero-touch, partner, msfb, intune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
---


# Windows Autopilot: What's new

**Applies to**

- Windows 10

## Windows Autopilot update history

The following [Windows Autopilot updates](autopilot-update.md) are available. **Note**: Updates are automatically downloaded and applied during the Windows Autopilot deployment process. 

No updates are available yet. Check back here later for more information.

## New in Windows 10, version 2004

With this release, you can configure Windows Autopilot [user-driven](user-driven.md) Hybrid Azure Active Directory join with VPN support. This support is also backported to Windows 10, version 1909 and 1903.

You can configure the Autopilot profile language settings to skip the language, locale, and keyboard pages during deployment. These pages will be skipped if the target device is connected to the Ethernet. In previous versions, skipping these pages was only supported with self-deploying profiles. Now, the pages will be skipped in all scenarios.

## New in Windows 10, version 1903

[Windows Autopilot for white glove deployment](white-glove.md) is new in Windows 10, version 1903. See the following video:

<br>

> [!VIDEO https://www.youtube.com/embed/nE5XSOBV0rI]

Also new in this version of Windows:
- The Intune enrollment status page (ESP) now tracks Intune Management Extensions.
- [Cortana voiceover and speech recognition during OOBE](windows-autopilot-scenarios.md#cortana-voiceover-and-speech-recognition-during-oobe) is disabled by default for all Windows 10 Pro Education, and Enterprise SKUs.
- [Windows Autopilot is self-updating during OOBE](windows-autopilot-scenarios.md#windows-autopilot-is-self-updating-during-oobe). Starting with the Windows 10, version 1903 Autopilot functional and critical updates will begin downloading automatically during OOBE.
- During OOBE on Windows 10 version 1903 devices, Windows Autopilot sets the diagnostics data level to Full. 

## New in Windows 10, version 1809

Windows Autopilot [self-deploying mode](self-deploying.md) is a zero touch device provisioning process. Simply power on the device, plug it into the Ethernet, and Autopilot automatically configures the device. End users don't have to press the “Next” button during the deployment process. 

You can use Windows Autopilot self-deploying mode complete the following tasks with no user authentication or interaction requires:
- register the device to an Azure AD tenant
- enroll in your organization’s MDM provider
- provision policies and applications 

>[!NOTE]
>Window 10, version 1903 or later is required to use self-deploying mode due to issues with TPM device attestation in Windows 10, version 1809.

## Related topics

[What's new in Microsoft Intune](/intune/whats-new)<br>
[What's new in Windows 10](/windows/whats-new/)