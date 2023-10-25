---
title: Troubleshoot Windows Autopilot Microsoft Entra join issues
description: Troubleshoot issues with Microsoft Entra join issues during the Windows Autopilot deployment process.
ms.technology: itpro-deploy
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 11/17/2022
ms.collection:
  - M365-modern-desktop
  - tier2
ms.topic: troubleshooting
---

# Troubleshoot Microsoft Entra join issues

*Applies to:*

- Windows 11
- Windows 10

The following are common Microsoft Entra join issues that can affect Windows Autopilot deployment.

<a name='azure-ad-permissions'></a>

## Microsoft Entra permissions

The most common issue joining a device to Microsoft Entra ID is related to Microsoft Entra permissions. Make sure that [the correct configuration is in place](configuration-requirements.md) to allow users to join devices to Microsoft Entra ID.

## Maximum number of devices

Errors can also happen if the user exceeds the [number of devices](/mem/intune/enrollment/device-limit-intune-azure) that they're allowed to join. This limit is configured in Microsoft Entra ID.

## Deleted objects

A Microsoft Entra device is created upon import. It's important this object isn't deleted. The object acts as Autopilot's anchor in Microsoft Entra ID for group membership and targeting (including the profile). Deleting it may lead to join errors. If this object is deleted, you can fix the issue by deleting and reimporting this autopilot hash so it can recreate the associated object.

## Error code 801C0003

Error code 801C0003 will typically be reported on an error page titled "Something went wrong". This error means that the Microsoft Entra join failed.

## Related topics

[Windows Autopilot - known issues](known-issues.md)

[Diagnose MDM failures in Windows 10](/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10)
