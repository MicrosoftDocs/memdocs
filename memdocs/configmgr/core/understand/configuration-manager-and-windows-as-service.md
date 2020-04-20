---
title: Configuration Manager and Windows as a Service
titleSuffix: Configuration Manager
description: Get basic information on adopting Configuration Manager current branch to support Windows as a service.
ms.date: 06/15/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c8534a1e-57b8-4688-b6e6-299d82cfcec9
author: aczechowski
ms.author: aaroncz
manager: dougeby


---

# Configuration Manager and Windows as a Service

*Applies to: Configuration Manager (current branch)*

Configuration Manager provides comprehensive control over feature updates for Windows 10. To fully adopt the Windows as a service model, you also must adopt the Configuration Manager current branch model. To stay current with Windows 10, requires that you stay current with Configuration Manager for the best experience. New versions of Configuration Manager are required to take full advantage of the exciting new enterprise features for Windows 10. This article is intended to be a landing page for the key articles required to adopt Configuration Manager current branch. Configuration Manager current branch gets you on your way to Windows as a service.

## Key articles about adopting Configuration Manager current branch

| Article        | Description          | 
| ------------- |-------------|
|[Overview of Configuration Manager current branch](../plan-design/changes/whats-new-incremental-versions.md)|Provides a brief summary of the key points for the new servicing model for Configuration Manager (Current Branch)|
|[Support lifecycle](../servers/manage/current-branch-versions-supported.md)|Explains the new support and servicing model.|
|[Removed and deprecated items](../plan-design/changes/deprecated/removed-and-deprecated.md)|Provides early notice about future changes that might affect your use of Configuration Manager.|
|[Updates to Configuration Manager current branch](../servers/manage/updates.md)|Explains the easy in-console method of applying feature updates to Configuration Manager.|
|[Get available updates](../servers/manage/install-in-console-updates.md#get-available-updates)|Explains the two modes available to get new Configuration Manager feature updates.|
|[Update checklist](../servers/manage/install-in-console-updates.md#bkmk_beforeinstall)|Provides update version-specific checklists, if applicable.| 
|[Install new Configuration Manager feature updates](../servers/manage/install-in-console-updates.md#bkmk_install)|Explains the simple installation steps for feature updates.|
|[Support for Windows 10](../plan-design/configs/support-for-windows-10.md)|Provides a support matrix for Windows 10 (and ADK) versions.|
|[Technical Previews for Configuration Manager](../get-started/technical-preview.md)|Provides information about the ConfigMgr technical preview program.|


## Key articles about adopting Windows as a service

| Article        | Description          |
| ------------- |-------------|
|[Manage Windows as a service](../../osd/deploy-use/manage-windows-as-a-service.md)|Explains how to use servicing plans to deploy Windows 10 feature updates.|
|[Upgrade Windows 10 via task sequence](../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)|The details of creating a task sequence to upgrade Windows 10 with additional recommendations.|
|[Phased deployments](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)|Phased deployments automate a coordinated, sequenced rollout of a task sequence across multiple collections.|  
|[Optimize Windows 10 update delivery](../../sum/deploy-use/optimize-windows-10-update-delivery.md)|Use Configuration Manager to manage update content to stay current with Windows 10.|
|[Use Desktop Analytics](../../desktop-analytics/overview.md)|Desktop Analytics allows you to assess and analyze the readiness of devices in your environment for an upgrade to Windows 10.|
|[Windows Update for Business integration (optional)](../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md)|Explains how to define and deploy Windows Update for Business (WUfB) policies using Configuration Manager.|
|[Use co-management with Microsoft Intune and Windows Update for Business (optional)](../../comanage/overview.md)|Provides an overview of co-management|


## Related articles

- [In-place upgrade to Configuration Manager current branch from System Center 2012 Configuration Manager](../servers/deploy/install/upgrade-to-configuration-manager.md)
- [Plan for migration to Configuration Manager current branch](../migration/planning-for-migration.md)
