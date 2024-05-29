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

| Feature | **Windows Autopilot device preparation** | **Windows Autopilot** |
| --- | --- | --- |
| Features | <ul><li>Support for Government Community Cloud High (GCCH) and Department of Defense (DoD) environments.</li><li>Faster, more consistent provisioning experience.</li><li>Near real-time monitoring and troubleshooting info.</li></ul> | <ul><li>Support for multiple device types</li><li>Many customization options of the provisioning experience.</li></ul> |
| Supported modes | <ul><li>User-driven</li></ul> | <ul><li>User-driven</li><li>Pre-provisioned</li><li>Self-deploying</li><li>Existing devices</li><li>Autopilot reset</li></ul>|
| Join types supported | Microsoft Entra join | Microsoft Entra join and Microsoft Entra hybrid join |
|Device registration required? | No | Yes |
| What do admins need to configure? | <ul><li>Windows Autopilot device preparation policy</li><li>Device security group with **Intune Provisioning Client** as owner</li></ul> | <ul><li>Windows Autopilot deployment profile</li><li>Enrollment Status Page (ESP)</li></ul> |


## Which Autopilot to use

## Related content
