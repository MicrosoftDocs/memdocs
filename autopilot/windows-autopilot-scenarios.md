---
title: Windows Autopilot scenarios and capabilities
description: Follow along with several typical Windows Autopilot deployment scenarios, such as redeploying a device in a business-ready state.
ms.service: windows-client
ms.subservice: autopilot
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/11/2024
ms.collection:
  - M365-modern-desktop
  - tier2
ms.topic: conceptual
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
  - ✅ <a href="https://learn.microsoft.com/hololens/hololens-release-notes" target="_blank">Windows Holographic</a>
---

# Windows Autopilot scenarios and capabilities

## Scenarios

Windows Autopilot supports a growing list of scenarios that organizations commonly need. These needs vary based on:

- Organization type.
- Progress moving to the latest version of Windows.
- The state of transitioning to [modern management](/windows/client-management/manage-windows-10-in-your-organization-modern-management).

The following Windows Autopilot scenarios are described in this guide:

| **Scenario** | **Description** |
| --- | --- |
| [Windows Autopilot user-driven mode](user-driven.md) | Deploy and configure devices so that an end user can set it up for themselves. |
| [Windows Autopilot self-deploying mode](self-deploying.md) | Deploy devices to be automatically configured for shared use, as a kiosk, or as a digital signage device. |
| [Windows Autopilot Reset](windows-autopilot-reset.md) | Redeploy a device in a business-ready state. |
| [Pre-provisioning](pre-provision.md) | Pre-provision a device with up-to-date applications, policies, and settings. |
| [Windows Autopilot for existing devices](existing-devices.md) | Deploy Windows on an existing Windows device. |

These scenarios are summarized in the following video:

> [!VIDEO https://learn-video.azurefd.net/vod/player?id=7e47e04e-7f51-4eba-9a23-d65f3411b425]

## Windows Autopilot capabilities

### Temporary Access Pass

Organizations using [Temporary Access Pass](/azure/active-directory/authentication/howto-authentication-temporary-access-pass) can use this feature with Windows Autopilot Microsoft Entra join user driven, pre-provisioning, and self-deploying mode for shared devices. The native Windows sign-in credential provider doesn't support Temporary Access Pass so it requires the enablement of WebSign-in. To enable this feature in the organization, follow the Configuration Service Provider (CSP) details outlined in [Policy CSP - Authentication](/windows/client-management/mdm/policy-csp-authentication#authentication-enablewebsignin). This feature isn't supported with Windows Autopilot Microsoft Entra hybrid join devices and isn't applicable on self-deploying mode kiosks.

### Cortana voiceover and speech recognition during OOBE

In Windows 10, Cortana voiceover and speech recognition during the out-of-box experience (OOBE) is **DISABLED** by default. This default applies to all Windows Pro, Education, and Enterprise editions. This feature isn't available in versions of Windows after Windows 10.

Cortana voiceover and speech recognition can be enabled during OOBE by creating the registry key value `EnableVoiceForAllEditions` in the following registry key:

> `HKLM\Software\Microsoft\Windows\CurrentVersion\OOBE\`

This registry key value doesn't exist by default.

The key value is a DWORD with **0** = disabled and **1** = enabled.

| **Value** | **Description** |
| --- | --- |
| **0** | Cortana voiceover is disabled |
| **1** | Cortana voiceover is enabled |
| No value | Device falls back to default behavior of the edition |

To change this key value, use the Windows Configuration Designer (WCD) tool to create as PPKG as documented in [EnableCortanaVoice](/windows/configuration/wcd/wcd-oobe#enablecortanavoice).

For more information, see [Cortana voice support](/windows-hardware/customize/desktop/cortana-voice-support).

[!INCLUDE [cortana-app-deprecation](../memdocs/intune/includes/cortana-app-deprecation.md)]

### BitLocker encryption

With Windows Autopilot, BitLocker encryption settings can be configured to apply before automatic encryption is started. For more information, see [Setting the BitLocker encryption algorithm for Autopilot devices](bitlocker.md).

## Related content

- [Windows Autopilot: What's new](whats-new.md).
