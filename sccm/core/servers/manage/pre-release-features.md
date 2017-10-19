---
title: "Pre-release features"
titleSuffix: "Configuration Manager"
description: "Pre-release features in System Center Configuration Manager"
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
caps.latest.revision: 36
author: Brenduns
ms.author: brenduns
manager: angrobe

---
# Pre-release features in System Center Configuration Manager
*Applies to: System Center Configuration Manager (Current Branch)*

Pre-release features are features that are in the Current Branch for early testing in a production environment. These features are fully supported but are still in active development and might receive changes until they move out of the pre-release category.

 Before you can use pre-release features, you must give consent to use Pre-release features from within the Configuration Manager console before you can select and enable their use.  

Giving consent is a one-time action per hierarchy that cannot be undone. Until you give consent, you cannot enable new pre-release features included with updates. After you turn on a pre-release feature, you cannot turn it off.

To give consent, in the console go to **Administration** > **Site Configuration** > **Sites**, and then choose **Hierarchy Settings**. On the **General** tab, choose **Consent to use Pre-Release features**.

 > [!NOTE]
 > If you enabled pre-release features from Update 1602 before you installed a later update version, those features are enabled for use even if you do not give consent to use pre-release features.

When you install an update that includes pre-release features, those features are visible in the Updates and Servicing Wizard with the regular features included in the update:
  - **If you have given consent:** You can enable pre-release features from within the Updates and Servicing Wizard when you are installing the update. To do so, select the pre-release features as you would any other feature.     

    Optionally, you can wait to enable a pre-release feature later from the **Administration** > **Updates and Servicing** > **Features** node of the console. In the **Features** node choose the feature and then choose **Turn on**. This option is grayed out until you give consent. (Prior to version 1702, Updates and Servicing was under **Administration** > **Cloud Services**.)
  -   **If you have not given consent:** When you're installing an update, pre-release features are visible in the Updates and Servicing Wizard but are grayed out and cannot be enabled. After the update is installed, you can view these features in the **Features** node. However, you cannot enable them until after you have given consent in **Hierarchy Settings**.

If you gave consent at a stand-alone primary site and then expand the hierarchy by installing a new central administration site, you must give consent again at the central administration site.

 When you enable a pre-release feature, the Configuration Manager hierarchy manager (HMAN) must process the change before that feature becomes available. Processing of the change is often immediate, but it can take up to 30 minutes to complete, depending on the HMAN processing cycle. After the change is processed, you must restart the console before you can view new UI related to that feature.

**The following pre-release features are available:**

 |Feature          |Added as pre-release | Added as a full feature|  
|------------------|---------------------|---------------------|
| Create and run PowerShell scripts from the Configuration Manager console |  [Version 1706](/sccm/apps/deploy-use/create-deploy-scripts)|![Not yet](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Device Guard management with Configuration Manager |  [Version 1702](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)|![Not yet](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Check for running executable files before installing an application  |   [Version 1702](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application) |[Version 1706](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application)|
| Data Warehouse service point  |  [Version 1702](/sccm/core/servers/manage/data-warehouse) |[Version 1706](/sccm/core/servers/manage/data-warehouse)|
| Peer Cache for content distribution to clients |  [Version 1610](/sccm/core/plan-design/hierarchy/client-peer-cache) |![Not yet](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Cloud management gateway |  [Version 1610](/sccm/core/clients/manage/plan-cloud-management-gateway) |![Not yet](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Client Data Sources dashboard |  [Version 1610](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard) |![Not yet](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Microsoft Operations Management Suite Connector  | [Version 1606](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md) |![Not yet](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Servicing a cluster aware collection (service a server group)| [Version 1602](../../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|![Not yet](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
|Conditional access for PCs managed by System Center Configuration Manager | [Version 1602](../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)     | [Version 1702](/sccm/mdm/deploy-use/manage-access-to-services)                     |
