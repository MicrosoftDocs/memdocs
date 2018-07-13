---
title: Pre-release features
titleSuffix: Configuration Manager
description: Pre-release features are features that are in the Current Branch for early testing in a production environment.
ms.date: 07/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Pre-release features in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Pre-release features are features that are in the current branch for early testing in a production environment. These features are fully supported, but still in active development. They might receive changes until they move out of the pre-release category.



## Give consent  

Before using pre-release features, give consent to use pre-release features. Giving consent is a one-time action per hierarchy that you can't undo. Until you give consent, you can't enable new pre-release features included with updates. After you turn on a pre-release feature, you can't turn it off.

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node.  

2. Click **Hierarchy Settings** in the ribbon.  

3. On the **General** tab of Hierarchy Settings Properties, enable the option to **Consent to use pre-release features**. Click **OK**.  



## Enabling pre-release features

When you install an update that includes pre-release features, those features are visible in the Updates and Servicing Wizard with the regular features included in the update.

#### If you have given consent
In the Updates and Servicing Wizard, enable pre-release features. Select the pre-release features as you would any other feature.     

Optionally, wait to enable pre-release features later from the **Features** node under **Updates and Servicing** in the **Administration** workspace. Select a feature, and then click **Turn on** in the ribbon. Until you give consent, this option isn't available for use.

#### If you haven't given consent
In the Updates and Servicing Wizard, pre-release features are visible but you can't enable them. After the update is installed, these features are visible in the **Features** node. However, you can't enable them until you give consent.


> [!Important]  
> In a multi-site hierarchy, you can only enable optional or pre-release features from the central administration site. This behavior ensures there are no conflicts across the hierarchy. <!--507197-->  
> 
> If you gave consent at a stand-alone primary site, and then expand the hierarchy by installing a new central administration site, you must give consent again at the central administration site.  

When you enable a pre-release feature, the Configuration Manager hierarchy manager (HMAN) must process the change before that feature becomes available. Processing of the change is often immediate. Depending on the HMAN processing cycle, it can take up to 30 minutes to complete. After the change is processed, restart the console before using the feature.



## Pre-release features


| Feature          | Added as pre-release | Added as a full feature |  
|------------------|----------------------|-------------------------|
| Mobile apps for co-managed devices<!--1357892-->|[Version 1806](/sccm/core/clients/manage/co-management-switch-workloads#workloads-able-to-be-transitioned-to-intune)|![Not yet](media/red_x.png)|
| Package Conversion Manager<!--1357861-->|[Version 1806]()<!--NEED FINAL LINK-->|![Not yet](media/red_x.png)|
| Support for Cisco AnyConnect 4.0.07x and later for iOS<!--1357393-->|[Version 1802](/sccm/mdm/deploy-use/create-vpn-profiles)| [Version 1802 with update 4163547](/sccm/mdm/deploy-use/create-vpn-profiles) |
| Phased Deployments<!--1356837-->|[Version 1802](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)|[Version 1806](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)|
| Run Task Sequence Step <!-- 1261338 --> |  [Version 1710](/sccm/osd/understand/task-sequence-steps#child-task-sequence) |[Version 1802](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#add-child-task-sequences-to-a-task-sequence)|
| Windows Defender Exploit Guard <!-- 1355468 --> |  [Version 1710](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) |[Version 1802](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy)|
| Device Health Attestation assessment for conditional access compliance policies <!-- 1235616 --> |  [Version 1710](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) |[Version 1802](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)|
| Create and run PowerShell scripts from the Configuration Manager console <!-- 1236459 --> |  [Version 1706](/sccm/apps/deploy-use/create-deploy-scripts)|[Version 1802](/sccm/apps/deploy-use/create-deploy-scripts)|
| Manage Microsoft Surface driver updates <!-- 1098490 --> |  [Version 1706](/sccm/sum/get-started/configure-classifications-and-products) | [Version 1710](/sccm/sum/get-started/configure-classifications-and-products)|
| Device Guard management with Configuration Manager <!-- 1319346 --> |  [Version 1702](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)|![Not yet](media/red_x.png)|
| Task sequence content pre-caching <!-- 1021244 --> |  [Version 1702](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content) | [Version 1710](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content)|
| Check for running executable files before installing an application <!-- 1284624 --> |   [Version 1702](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application) |[Version 1706](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application)|
| Data Warehouse service point <!-- 1277922 --> |  [Version 1702](/sccm/core/servers/manage/data-warehouse) |[Version 1706](/sccm/core/servers/manage/data-warehouse)|
| Peer Cache for content distribution to clients <!-- 1101436 --> |  [Version 1610](/sccm/core/plan-design/hierarchy/client-peer-cache) | [Version 1710](/sccm/core/plan-design/hierarchy/client-peer-cache)|
| Cloud management gateway <!-- 1101764 --> |  [Version 1610](/sccm/core/clients/manage/plan-cloud-management-gateway) |[Version 1802](/sccm/core/clients/manage/plan-cloud-management-gateway)|
| Microsoft Operations Management Suite Connector <!-- 1236739 --> | [Version 1606](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) |[Version 1802](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite)|
| Servicing a cluster aware collection (service a server group) <!-- 1081776 --> | [Version 1602](/sccm/core/get-started/capabilities-in-technical-preview-1605#BKMK_ServerGroups)|![Not yet](media/red_x.png)|
| Conditional access for PCs managed by System Center Configuration Manager <!--  --> | [Version 1602](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)     | [Version 1702](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)                     |
<!--Image used = ![Not yet](media/red_x.png) -->

> [!Tip]  
> For more information on non-pre-release features that you must enable first, see [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  
> 
> For more information on features that are only available in the technical preview branch, see [Technical Preview](/sccm/core/get-started/technical-preview).  
