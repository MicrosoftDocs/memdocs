---
title: Compare Windows Autopilot device preparation and Windows Autopilot
description: Compare Windows Autopilot device preparation and Windows Autopilot features and when to use each.
ms.service: windows-client
ms.subservice: itpro-deploy
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 05/31/2024
ms.topic: article
ms.collection:
  - M365-modern-desktop
  - m365initiative-coredeploy
  - highpri
  - tier1
  - essentials-overview
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---

# Compare Windows Autopilot device preparation and Windows Autopilot

## Windows Autopilot device preparation vs. Windows Autopilot

| Feature | **Windows Autopilot<br>device preparation** | **Windows Autopilot** |
| --- | --- | --- |
| Features | <ul><li>Support for Government Community Cloud High (GCCH) and Department of Defense (DoD) environments.</li><li>Faster, more consistent provisioning experience.</li><li>Near real-time monitoring and troubleshooting info.</li></ul> | <ul><li>Support for multiple device types (Hololens, Teams Meeting Room)</li><li>Many customization options of the provisioning experience.</li></ul> |
| Supported modes | <ul><li>User-driven</li></ul> | <ul><li>User-driven</li><li>Pre-provisioned</li><li>Self-deploying</li><li>Existing devices</li></ul>|
| Join types supported | <ul><li>Microsoft Entra join</li></ul> | <ul><li>Microsoft Entra join</li><li>Microsoft Entra hybrid join</li></ul> |
|Device registration required? | No | Yes |
| What do admins need to configure? | <ul><li>Windows Autopilot device preparation policy</li><li>Device security group with **Intune Provisioning Client** as owner</li></ul> | <ul><li>Windows Autopilot deployment profile</li><li>Enrollment Status Page (ESP)</li></ul> |
| What can be delivered during provisioning? | <ul><li>Device-based only during the out of box experience (OOBE)</li><li>Up to 10 essential applications (line-of-business (LOB), Win32, WinGet, Microsoft 365)</li><li>Up to 10 essential PowerShell scripts</li></ul> | <ul><li>Device-based during device ESP</li><li>User-based during user ESP</li><li>Any number of applications</li></ul> |
| Reporting & troubleshooting | Windows Autopilot deployment report:<ul><li> Only shows Windows Autopilot registered devices.</li><li>Not real-time.</li></ul> | Windows Autopilot device preparation deployment report:<ul><li>Shows all Windows Autopilot device preparation deployments.<li>More data available</li><li>More accurate.</li><li>Near real-time.</li></ul> |
| Supports LOB and Win32 applications in same deployment? | Yes | No |
| Supported versions of Windows | <ul><li>>Windows 11, version 23H2 with [KB5035942](https://support.microsoft.com/topic/march-26-2024-kb5035942-os-builds-22621-3374-and-22631-3374-preview-3ad9affc-1a91-4fcb-8f98-1fe3be91d8df) or later</li><li> Windows 11, version 22H2 with [KB5035942](https://support.microsoft.com/topic/march-26-2024-kb5035942-os-builds-22621-3374-and-22631-3374-preview-3ad9affc-1a91-4fcb-8f98-1fe3be91d8df) or later</li></ul> | <ul><li>All [currently supported](/windows/release-health/supported-versions-windows-client#windows-11-supported-versions) versions of Windows 11 General Availability Channel</li><li>All [currently supported](/windows/release-health/supported-versions-windows-client#windows-10-supported-versions) versions of Windows 10 General Availability Channel</li></ul> |

## Which Autopilot to use

## Related content
