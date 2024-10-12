---
title: Compare Windows Autopilot device preparation and Windows Autopilot
description: Compare Windows Autopilot device preparation and Windows Autopilot features and when to use each.
ms.service: windows-client
ms.subservice: autopilot
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/26/2024
ms.topic: overview
ms.collection:
  - M365-modern-desktop
  - m365initiative-coredeploy
  - highpri
  - tier1
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---

# Compare Windows Autopilot device preparation and Windows Autopilot

## Windows Autopilot device preparation vs. Windows Autopilot

| Feature | **Windows Autopilot<br>device preparation** | **Windows Autopilot** |
| --- | --- | --- |
| Features | <ul><li>Support for Government Community Cloud High (GCCH) and Department of Defense (DoD) environments.</li><li>Faster, more consistent provisioning experience.</li><li>Near real-time monitoring and troubleshooting info.</li></ul> | <ul><li>Support for multiple device types ([HoloLens](/hololens/hololens2-autopilot), [Teams Meeting Room](/microsoftteams/rooms/autopilot-autologin)).</li><li>Many customization options for the provisioning experience.</li></ul> |
| Supported modes | <ul><li>[User-driven](tutorial/user-driven/entra-join-workflow.md).</li></ul> | <ul><li>[User-driven](../tutorial/user-driven/azure-ad-join-workflow.md).</li><li>[Pre-provisioned](../tutorial/pre-provisioning/azure-ad-join-workflow.md).</li><li>[Self-deploying](../tutorial/self-deploying/self-deploying-workflow.md).</li><li>[Existing devices](../tutorial/existing-devices/existing-devices-workflow.md).</li></ul>|
| Join types supported | <ul><li>Microsoft Entra join.</li></ul> | <ul><li>Microsoft Entra join.</li><li>Microsoft Entra hybrid join.</li></ul> |
|Device registration required? | No. | Yes. |
| What do admins need to configure? | <ul><li>Windows Autopilot device preparation policy.</li><li>Device security group with **Intune Provisioning Client** as owner.</li></ul> | <ul><li>Windows Autopilot deployment profile.</li><li>Enrollment Status Page (ESP).</li></ul> |
| What configurations can be delivered during provisioning? | <ul><li>Device-based only during the out-of-box experience (OOBE).</li><li>Up to 10 essential applications (line-of-business (LOB), Win32, Microsoft Store, Microsoft 365).</li><li>Up to 10 essential PowerShell scripts.</li></ul> | <ul><li>Device-based during device ESP.</li><li>User-based during user ESP.</li><li>Any number of applications.</li></ul> |
| Reporting & troubleshooting |  Windows Autopilot device preparation deployment report:<ul><li>Shows all Windows Autopilot device preparation deployments.</li><li>More data available.</li><li>Near real-time.</li></ul> | Windows Autopilot deployment report:<ul><li>Only shows Windows Autopilot registered devices.</li><li>Not real-time.</li></ul> |
| Supports LOB and Win32 applications in same deployment? | Yes. | No. |
| Supported versions of Windows | <ul><li>Windows 11, version 23H2 with [KB5035942](https://support.microsoft.com/topic/march-26-2024-kb5035942-os-builds-22621-3374-and-22631-3374-preview-3ad9affc-1a91-4fcb-8f98-1fe3be91d8df) or later.</li><li> Windows 11, version 22H2 with [KB5035942](https://support.microsoft.com/topic/march-26-2024-kb5035942-os-builds-22621-3374-and-22631-3374-preview-3ad9affc-1a91-4fcb-8f98-1fe3be91d8df) or later.</li></ul> | <ul><li>All [currently supported](/windows/release-health/supported-versions-windows-client#windows-11-supported-versions) versions of Windows 11 General Availability Channel.</li><li>All [currently supported](/windows/release-health/supported-versions-windows-client#windows-10-supported-versions) versions of Windows 10 General Availability Channel.</li></ul> |

## Which Windows Autopilot solution to use

Which version of Windows Autopilot to use is dependent on many factors and variables, with each environment having different needs. Windows Autopilot device preparation in its initial offering isn't as feature rich as Windows Autopilot, but it does have some advantages and features not available in Windows Autopilot.

In general, the following are some of the major factors when considering between Windows Autopilot device preparation or Windows Autopilot:

| Requirement | **Windows Autopilot<br>device preparation** | **Windows<br>Autopilot** |
| --- | --- | --- |
| Government Community Cloud High (GCCH) and<br>Department of Defense (DoD) environments | ✅ | ❌ |
| User-driven scenario | ✅ | ✅ |
| Pre-provisioned scenario | ❌ | ✅ |
| Self-deploying scenario | ❌ | ✅ |
| Existing devices scenario | ❌ | ✅ |
| Autopilot reset support | ❌ | ✅ |
| Microsoft Entra join | ✅ | ✅ |
| Microsoft Entra hybrid join | ❌ | ✅ |
| [Windows Autopilot Reset](../tutorial/reset/autopilot-reset-overview.md) | ❌ | ✅ |
| Windows 11 | ✅ | ✅ |
| Windows 10 | ❌ | ✅ |
| Deploy Win32 and LOB applications<br>in the same deployment | ✅ | ❌ |
| Simpler deployment configuration and experience | ✅ | ❌ |
| Extensive customization of deployment<br>and OOBE experience | ❌ | ✅ |
| No requirement to pre-stage devices | ✅ | ❌ |
| Install more than 10 applications during OOBE | ❌ | ✅ |
| Run more than 10 PowerShell scripts during OOBE | ❌ | ✅ |
| Near real-time monitoring | ✅ | ❌ |
| Block user from accessing desktop until<br>user based configurations are applied | ❌ | ✅ |
| [HoloLens](/hololens/hololens2-autopilot) support | ❌ | ✅ |
| [Teams Meeting Room](/microsoftteams/rooms/autopilot-autologin) support | ❌ | ✅ |
| Device Firmware Configuration Interface<br>([DFCI](../dfci-management.md)) Management support | ❌ | ✅ |
| [Autopilot into co-management](/mem/configmgr/comanage/autopilot-enrollment) | ❌ | ✅ |

## Using Windows Autopilot device preparation and Windows Autopilot concurrently

Windows Autopilot device preparation and Windows autopilot can be used concurrently and side by side within an organization. However, any one device in an environment can only run one of the two solutions. Windows Autopilot profiles take precedence over Windows Autopilot device preparation policies. If a Windows Autopilot registered device needs to go through a Windows Autopilot device preparation deployment, it must first be removed as a Windows Autopilot device. For more information, see [Deregister a device](../registration-overview.md#deregister-a-device).
