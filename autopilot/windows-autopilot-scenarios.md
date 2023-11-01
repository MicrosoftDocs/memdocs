---
title: Windows Autopilot scenarios and capabilities
description: Follow along with several typical Windows Autopilot deployment scenarios, such as redeploying a device in a business-ready state.
ms.prod: windows-client
ms.technology: itpro-deploy
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 11/17/2022
ms.collection:
  - M365-modern-desktop
  - tier2
ms.topic: conceptual
---

# Windows Autopilot scenarios and capabilities

*Applies to:*

- Windows 11
- Windows 10
- Windows Holographic, version 2004 or later

## Scenarios

Windows Autopilot supports a growing list of scenarios that organizations commonly need. These needs vary based on:
- Organization type.
- Progress moving to Windows 10/11.
- How far they've [transitioned to modern management](/windows/client-management/manage-windows-10-in-your-organization-modern-management).

The following Windows Autopilot scenarios are described in this guide:

| Scenario | More information |
| --- | --- |
| Deploy and configure devices so that an end user can set it up for themselves | [Windows Autopilot user-driven mode](user-driven.md) |
| Deploy devices to be automatically configured for shared use, as a kiosk, or as a digital signage device.| [Windows Autopilot self-deploying mode](self-deploying.md) |
| Redeploy a device in a business-ready state.| [Windows Autopilot Reset](windows-autopilot-reset.md) |
| Pre-provision a device with up-to-date applications, policies, and settings.| [Pre-provisioning](pre-provision.md) |
| Deploy Windows 10/11 on an existing Windows device | [Windows Autopilot for existing devices](existing-devices.md) |

These scenarios are summarized in the following video.

&nbsp;

> [!video https://www.microsoft.com/videoplayer/embed/RE4Ci1b?autoplay=false]

## Windows Autopilot capabilities

### Temporary Access Pass
Organizations leveraging [Temporary Access Pass](/azure/active-directory/authentication/howto-authentication-temporary-access-pass) can use this feature with Windows Autopilot Microsoft Entra join user driven, pre-provisioning, and self-deploying mode for shared devices. Temporary Access Pass is not supported by the native Windows login credential provider so it requires the enablement of WebSign-in. To enable this feature in your organization you can follow the CSP details outlined in [Policy CSP - Authentication](/windows/client-management/mdm/policy-csp-authentication#authentication-enablewebsignin). This feature is not supported with Windows Autopilot Microsoft Entra hybrid join devices and is not applicable on self-deploying mode kiosks.

### Cortana voiceover and speech recognition during OOBE

In Windows 10, version 1903 and later, Cortana voiceover and speech recognition during OOBE is DISABLED by default. This default applies to all Windows Pro, Education, and Enterprise editions.

You can also enable Cortana voiceover and speech recognition during OOBE by creating the following registry key. This key doesn't exist by default:

HKLM\Software\Microsoft\Windows\CurrentVersion\OOBE\EnableVoiceForAllEditions

The key value is a DWORD with **0** = disabled and **1** = enabled.

| Value | Description |
| --- | --- |
| 0 | Cortana voiceover is disabled |
| 1 | Cortana voiceover is enabled |
| No value | Device will fall back to default behavior of the edition |

To change this key value, use WCD tool to create as PPKG as documented [here](/windows/configuration/wcd/wcd-oobe#nforce).

[!INCLUDE [cortana-app-deprecation](../memdocs/intune/includes/cortana-app-deprecation.md)]

### BitLocker encryption

With Windows Autopilot, you can configure the BitLocker encryption settings to be applied before automatic encryption is started. For more information, see [Setting the BitLocker encryption algorithm for Autopilot devices](bitlocker.md)

## Related topics

[Windows Autopilot: What's new](windows-autopilot-whats-new.md)
