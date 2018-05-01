---
title: Pre-release features
titleSuffix: Configuration Manager
description: Pre-release features are features that are in the Current Branch for early testing in a production environment.
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Pre-release features in System Center Configuration Manager
*Applies to: System Center Configuration Manager (Current Branch)*

Pre-release features are features that are in the Current Branch for early testing in a production environment. These features are fully supported but are still in active development and might receive changes until they move out of the pre-release category.

 Before you can use pre-release features, you must give consent to use Pre-release features from within the Configuration Manager console before you can select and enable their use.  

Giving consent is a one-time action per hierarchy that cannot be undone. Until you give consent, you cannot enable new pre-release features included with updates. After you turn on a pre-release feature, you cannot turn it off.

To give consent, in the console go to **Administration** > **Site Configuration** > **Sites**, and then choose **Hierarchy Settings**. On the **General** tab, choose **Consent to use Pre-Release features**.

When you install an update that includes pre-release features, those features are visible in the Updates and Servicing Wizard with the regular features included in the update:
  - **If you have given consent:** You can enable pre-release features from within the Updates and Servicing Wizard when you are installing the update. To do so, select the pre-release features as you would any other feature.     

    Optionally, you can wait to enable a pre-release feature later from the **Administration** > **Updates and Servicing** > **Features** node of the console. In the **Features** node choose the feature and then choose **Turn on**. This option is grayed out until you give consent. (Prior to version 1702, Updates and Servicing was under **Administration** > **Cloud Services**.)
  -   **If you have not given consent:** When you're installing an update, pre-release features are visible in the Updates and Servicing Wizard but are grayed out and cannot be enabled. After the update is installed, you can view these features in the **Features** node. However, you cannot enable them until after you have given consent in **Hierarchy Settings**.


> [!Important]  
> In a multi-site hierarchy, you can only enable optional or pre-release features from the central administration site. This behavior ensures there are no conflicts across the hierarchy. <!--507197-->  
> If you gave consent at a stand-alone primary site and then expand the hierarchy by installing a new central administration site, you must give consent again at the central administration site.  

 When you enable a pre-release feature, the Configuration Manager hierarchy manager (HMAN) must process the change before that feature becomes available. Processing of the change is often immediate, but it can take up to 30 minutes to complete, depending on the HMAN processing cycle. After the change is processed, you must restart the console before you can view new UI related to that feature.

**The following pre-release features are available:**

 |Feature          |Added as pre-release | Added as a full feature|  
|------------------|---------------------|---------------------|
|Phased Deployments<!--1356837-->|[Version 1802](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)|![Not yet](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Run Task Sequence Step <!-- 1261338 --> |  [Version 1710](/sccm/osd/understand/task-sequence-steps#child-task-sequence) |[Version 1802](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#add-child-task-sequences-to-a-task-sequence)|
| Windows Defender Exploit Guard <!-- 1355468 --> |  [Version 1710](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) |[Version 1802](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy)|
| Device Health Attestation assessment for conditional access compliance policies <!-- 1235616 --> |  [Version 1710](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) |[Version 1802](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)|
| Create and run PowerShell scripts from the Configuration Manager console <!-- 1236459 --> |  [Version 1706](/sccm/apps/deploy-use/create-deploy-scripts)|[Version 1802](/sccm/apps/deploy-use/create-deploy-scripts)|
| Manage Microsoft Surface driver updates <!-- 1098490 --> |  [Version 1706](/sccm/sum/get-started/configure-classifications-and-products) | [Version 1710](/sccm/sum/get-started/configure-classifications-and-products)|
| Device Guard management with Configuration Manager <!-- 1319346 --> |  [Version 1702](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)|![Not yet](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Task sequence content pre-caching <!-- 1021244 --> |  [Version 1702](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content) | [Version 1710](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content)|
| Check for running executable files before installing an application <!-- 1284624 --> |   [Version 1702](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application) |[Version 1706](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application)|
| Data Warehouse service point <!-- 1277922 --> |  [Version 1702](/sccm/core/servers/manage/data-warehouse) |[Version 1706](/sccm/core/servers/manage/data-warehouse)|
| Peer Cache for content distribution to clients <!-- 1101436 --> |  [Version 1610](/sccm/core/plan-design/hierarchy/client-peer-cache) | [Version 1710](/sccm/core/plan-design/hierarchy/client-peer-cache)|
| Cloud management gateway <!-- 1101764 --> |  [Version 1610](/sccm/core/clients/manage/plan-cloud-management-gateway) |[Version 1802](/sccm/core/clients/manage/plan-cloud-management-gateway)|
| Microsoft Operations Management Suite Connector <!-- 1236739 --> | [Version 1606](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md) |[Version 1802](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md)|
| Servicing a cluster aware collection (service a server group) <!-- 1081776 --> | [Version 1602](../../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|![Not yet](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Conditional access for PCs managed by System Center Configuration Manager <!--  --> | [Version 1602](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)     | [Version 1702](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)                     |
<!--Image used = ![Not yet](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif) -->

> [!Tip]  
> For more information on non-pre-release features that you must enable first, see [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  
> For more information on features that are only available in the technical preview branch, see [Technical Preview](/sccm/core/get-started/technical-preview).  
