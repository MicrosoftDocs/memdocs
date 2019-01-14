---
title: Configuration Manager and Windows as a Service
titleSuffix: Configuration Manager
description: Get basic information on adopting Configuration Manager current branch to support Windows as a service.
ms.date: 06/15/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c8534a1e-57b8-4688-b6e6-299d82cfcec9
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Configuration Manager and Windows as a Service

*Applies To: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager provides comprehensive control over feature updates for Windows 10. To fully adopt the Windows as a service model, you also must adopt the Configuration Manager current branch model. To stay current with Windows 10, requires that you stay current with Configuration Manager for the best experience. New versions of Configuration Manager are required to take full advantage of the exciting new enterprise features for Windows 10. This article is intended to be a landing page for the key articles required to adopt Configuration Manager current branch. Configuration Manager current branch gets you on your way to Windows as a service.

## Key articles about adopting Configuration Manager current branch

| Article        | Description          | 
| ------------- |-------------|
|[Overview of Configuration Manager current branch](/sccm/core/plan-design/changes/whats-new-incremental-versions)|Provides a brief summary of the key points for the new servicing model for Configuration Manager (Current Branch)|
|[Support lifecycle](/sccm/core/servers/manage/current-branch-versions-supported)|Explains the new support and servicing model.|
|[Removed and deprecated items](/sccm//core/plan-design/changes/deprecated/removed-and-deprecated)|Provides early notice about future changes that might affect your use of Configuration Manager.|
|[Updates to Configuration Manager current branch](/sccm/core/servers/manage/updates)|Explains the easy in-console method of applying feature updates to Configuration Manager.|
|[Get available updates](/sccm/core/servers/manage/install-in-console-updates#get-available-updates)|Explains the two modes available to get new Configuration Manager feature updates.|
|[Update checklist](/sccm/core/servers/manage/install-in-console-updates#bkmk_beforeinstall)|Provides update version-specific checklists, if applicable.| 
|[Install new Configuration Manager feature updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_install)|Explains the simple installation steps for feature updates.|
|[Support for Windows 10](/sccm/core/plan-design/configs/support-for-windows-10)|Provides a support matrix for Windows 10 (and ADK) versions.|
|[Technical Previews for Configuration Manager](/sccm/core/get-started/technical-preview)|Provides information about the ConfigMgr technical preview program.|


## Key articles about adopting Windows as a service

| Article        | Description          | 
| ------------- |-------------|
|[Manage Windows as a service](/sccm/osd/deploy-use/manage-windows-as-a-service)|Explains how to use servicing plans to deploy Windows 10 feature updates.|
|[Upgrade Windows 10 via task sequence](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)|The details of creating a task sequence to upgrade Windows 10 with additional recommendations.|
|[Phased deployments](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)|Phased deployments automate a coordinated, sequenced rollout of a task sequence across multiple collections.|  
|[Optimize Windows 10 update delivery](/sccm/sum/deploy-use/optimize-windows-10-update-delivery)|Use Configuration Manager to manage update content to stay current with Windows 10.|
|[Integrate with Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics)|Upgrade Readiness allows you to assess and analyze the readiness of devices in your environment for an upgrade to Windows 10.| 
|[Windows Update for Business integration (optional)](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10)|Explains how to define and deploy Windows Update for Business (WUfB) policies using Configuration Manager.|
|[Use co-management with Microsoft Intune and Windows Update for Business (optional)](/sccm/comanage/overview)|Provides an overview of co-management| 


## Related articles

- [In-place upgrade to System Center Configuration Manager (Current Branch) from ConfigMgr 2012](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
- [Plan for migration to System Center Configuration Manager (Current Branch) from ConfigMgr 2007](/sccm/core/migration/planning-for-migration)