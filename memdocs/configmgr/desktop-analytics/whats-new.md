---
title: What's new in Desktop Analytics
titleSuffix: Configuration Manager
description: A summary of the new features in the latest monthly release of the Desktop Analytics cloud service.
ms.date: 11/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.localizationpriority: medium
---

# What's new in Desktop Analytics

> [!IMPORTANT]
> The recent shift to hybrid and remote work is changing the way organizations manage enterprise devices. Many organizations are moving to modern cloud management solutions. Microsoft is making new features available in Microsoft Endpoint Manager to better facilitate and support this change as you begin your transition to Windows 11 devices.
>
> To align investments with this shift, **Desktop Analytics will be retired on November 30, 2022**. Over the next year, the types of insights currently found in Desktop Analytics will be incorporated directly into the Microsoft Endpoint Manager admin center.<!-- 10946169 -->
>
> For more information, see [A data-driven approach to managing devices in your organization](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/a-data-driven-approach-to-managing-devices-in-your-organization/ba-p/2932082).

## July 2021

### Support for the Windows diagnostic data processor configuration

<!-- 10220671 -->

Desktop Analytics now supports the new [Windows diagnostic data processor configuration](/windows/privacy/changes-to-windows-diagnostic-data-collection#new-windows-diagnostic-data-processor-configuration). This configuration provides you greater control of your Windows diagnostic data. Microsoft acts as a data processor, processing Windows diagnostic data for you as the controller. You'll continue to get insights to plan your deployments, and can fulfill [data subject requests](/windows/privacy/windows-10-and-privacy-compliance#3-the-process-for-exercising-data-subject-rights). These requests are typically to access or export Windows diagnostic data for a particular user.

To take advantage of this change, make sure your environment is up to date:

- Use Configuration Manager version 2006 with [update rollup (4575789)](https://support.microsoft.com/topic/revised-update-rollup-for-microsoft-endpoint-configuration-manager-current-branch-version-2006-5861b9ee-9257-a15c-723e-c60110ce0c85) or a later version. Configuration Manager configures enrolled devices with policies for the Windows diagnostic data processor configuration. Update your site and clients to make sure they're using the latest configurations. Use Configuration Manager for the best experience with configuring and [enrolling devices into Desktop Analytics](enroll-devices.md#device-enrollment).

- The Windows diagnostic data processor configuration is supported on the following Windows 10 versions:
  - Pro, Education, and Enterprise editions
  - Version 1809 or later
  - July 2021 cumulative update or later

  > [!IMPORTANT]
  > Devices with an older OS version like Windows 7 will continue to show in Desktop Analytics until January 31, 2022. Use Desktop Analytics to update those devices to a supported version of Windows 10. After that date, Desktop Analytics will only display devices with supported versions of Windows 10.

## What's new in Configuration Manager

The Desktop Analytics docs always refer to functionality in the latest version of Configuration Manager current branch. For more information on the latest changes in Configuration Manager, see [What's new in Configuration Manager incremental versions](../core/plan-design/changes/whats-new-incremental-versions.md).
