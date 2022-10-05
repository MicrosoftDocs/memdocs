---
title: Configuration Manager and Windows as a Service
titleSuffix: Configuration Manager
description: Get basic information on adopting Configuration Manager current branch to support Windows as a service.
ms.date: 12/07/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: overview
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Configuration Manager and Windows as a service

*Applies to: Configuration Manager (current branch)*

Configuration Manager provides comprehensive control over feature updates for Windows. To fully adopt the Windows as a service model, you also must adopt the Configuration Manager current branch model. To stay current with Windows, requires that you stay current with Configuration Manager for the best experience. New versions of Configuration Manager are required to take full advantage of the exciting new enterprise features for Windows. This article is intended to be a landing page for the key articles required to adopt Configuration Manager current branch. Configuration Manager current branch gets you on your way to Windows as a service.

## Configuration Manager current branch

| Article | Description |
|--|--|
| [Overview of Configuration Manager current branch](../plan-design/changes/whats-new-incremental-versions.md) | Provides a brief summary of the key points for the servicing model for Configuration Manager current branch |
| [Support lifecycle](../servers/manage/current-branch-versions-supported.md) | Explains the current branch support and servicing model. |
| [Removed and deprecated items](../plan-design/changes/deprecated/removed-and-deprecated.md) | Provides early notice about future changes that might affect your use of Configuration Manager. |
| [Updates to Configuration Manager current branch](../servers/manage/updates.md) | Explains the easy in-console method of applying feature updates to Configuration Manager. |
| [Get available updates](../servers/manage/prepare-in-console-updates.md#get-available-updates) | Explains the two modes available to get new Configuration Manager feature updates. |
| [Update checklist](../servers/manage/prepare-in-console-updates.md#before-you-install-an-in-console-update) | Provides update version-specific checklists, if applicable. |
| [Install new Configuration Manager feature updates](../servers/manage/install-in-console-updates.md) | Explains the simple installation steps for feature updates. |
| [Support for Windows 11](../plan-design/configs/support-for-windows-11.md) | Provides a support matrix for Windows 11 versions. |
| [Support for Windows 10](../plan-design/configs/support-for-windows-10.md) | Provides a support matrix for Windows 10 versions. |
| [Support for Windows ADK](../plan-design/configs/support-for-windows-adk.md) | Provides a support matrix for the Windows Assessment and Deployment Kit (Windows ADK). |
| [Technical Previews for Configuration Manager](../get-started/technical-preview.md) | Provides information about the Configuration Manager technical preview program. |

## Windows as a service

| Article | Description |
|--|--|
| [Manage Windows as a service](../../osd/deploy-use/manage-windows-as-a-service.md) | Explains how to use servicing plans to deploy Windows feature updates. |
| [Upgrade Windows via task sequence](../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md) | The details of creating a task sequence to upgrade Windows with additional recommendations. |
| [Phased deployments](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md) | Phased deployments automate a coordinated, sequenced rollout of a task sequence across multiple collections. |
| [Optimize Windows update delivery](../../sum/deploy-use/optimize-windows-10-update-delivery.md) | Use Configuration Manager to manage update content to stay current with Windows. |
| [Use Desktop Analytics](../../desktop-analytics/overview.md) | Desktop Analytics allows you to assess and analyze the readiness of devices in your environment for an upgrade to Windows. |
| [Windows Update for Business integration (optional)](../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md) | Explains how to define and deploy Windows Update for Business (WUfB) policies using Configuration Manager. |
| [Use co-management with Microsoft Intune and Windows Update for Business (optional)](../../comanage/overview.md) | Provides an overview of co-management. |

## Product lifecycle

<!-- 10976295 -->

Another important aspect of staying current with Windows and Configuration Manager is to monitor product lifecycles. Configuration Manager has built-in features to help:

- Be proactive with dashboards for planning:
  - [Product lifecycle dashboard](../clients/manage/asset-intelligence/product-lifecycle-dashboard.md): View the Microsoft Lifecycle Policy for applicable products.
  - [Windows servicing dashboard](../../osd/deploy-use/manage-windows-as-a-service.md): Provides you with information about computers in your environment, servicing plans, and compliance information.

- Be reactive with notifications, management insights, and reports:
  - [Configuration Manager console notifications](../servers/manage/admin-console-notifications.md#new-notifications-in-version-2010): Look for in-console notifications about devices with operating systems that are past the end of support date and that are no longer eligible to receive security updates.
  - Management insights
    - [Security](../servers/manage/management-insights.md#security): Identify clients with unsupported antimalware client versions or clients running earlier versions of Windows that don't receive security updates by default.
    - [Simplified management](../servers/manage/management-insights.md#simplified-management): Identify clients running an unsupported version of Windows or with an earlier version of the Configuration Manager client.
  - Reports:
    - [Data warehouse historical reporting](../servers/manage/list-of-reports.md#data-warehouse): View computers that are missing software updates.
    - [OS reports](../servers/manage/list-of-reports.md#operating-system): View computers by OS versions and servicing details.
    - [Software Updates compliance reports](../servers/manage/list-of-reports.md#software-updates---a-compliance): View software update compliance details.
  - [Power BI sample reports for software updates](../servers/manage/powerbi-sample-reports.md): Use Power BI to view software update compliance status.

## Next steps

- [In-place upgrade to Configuration Manager current branch from System Center 2012 Configuration Manager](../servers/deploy/install/upgrade-to-configuration-manager.md)
- [Plan for migration to Configuration Manager current branch](../migration/planning-for-migration.md)
