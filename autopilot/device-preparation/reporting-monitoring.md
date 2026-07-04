---
title: Windows Autopilot device preparation reporting and monitoring
description: Reporting and monitoring in Windows Autopilot device preparation.
ms.date: 05/11/2026
ms.topic: how-to
ms.collection:
  - M365-modern-desktop
  - m365initiative-coredeploy
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---

# Windows Autopilot device preparation reporting and monitoring

This feature provides built-in reporting and monitoring with near real-time status of deployments, including applications and PowerShell script details, and deployment time. It provides improved troubleshooting.

## Accessing reports and near real-time monitoring

To access Windows Autopilot device preparation reports and monitor deployments in near real-time:

[!INCLUDE [Windows Autopilot device preparation reporting and monitoring](includes/reporting-monitoring.md)]

> [!IMPORTANT]
> Deployment logs are automatically cleaned up every 28 days to prevent outdated or redundant records from accumulating in your reports. Automatic cleanup applies only to deployment records created after the auto-cleanup feature was introduced. 
> 
> If you enabled Windows Autopilot device preparation for Windows 365 before automatic cleanup was available, manually remove any older deployment records that remain in your reports. This one-time manual cleanup ensures your reports reflect only current deployments.  
