---
title: Troubleshoot Windows Autopilot Microsoft Entra join issues
description: Troubleshoot issues with Microsoft Entra join issues during the Windows Autopilot deployment process.
ms.subservice: itpro-deploy
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 06/06/2024
ms.collection:
  - M365-modern-desktop
  - tier2
ms.topic: troubleshooting
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Troubleshoot Microsoft Entra join issues

The following are common Microsoft Entra join issues that can affect Windows Autopilot deployment.

## Microsoft Entra permissions

The most common issue joining a device to Microsoft Entra ID is related to Microsoft Entra permissions. Make sure that [the correct configuration is in place](requirements.md?tabs=configuration) to allow users to join devices to Microsoft Entra ID.

## Maximum number of devices

Errors can also happen if the user exceeds the [number of devices](/mem/intune/enrollment/device-limit-intune-azure) that they're allowed to join. This limit is configured in Microsoft Entra ID.

## Deleted objects

A Microsoft Entra device is created upon import. It's important this object isn't deleted. The object acts as Autopilot's anchor in Microsoft Entra ID for group membership and targeting (including the profile). Deleting it might lead to join errors. If this object is deleted, the issue can be fixed by deleting and reimporting this autopilot hash so it can recreate the associated object.

## Error code 801C0003

Error code **801C0003** is typically reported on an error page titled **Something went wrong**. This error means that the Microsoft Entra join failed.

## Related content

- [Windows Autopilot - known issues](known-issues.md).
- [Collect MDM logs](/windows/client-management/mdm-collect-logs).
