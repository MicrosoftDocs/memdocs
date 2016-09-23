---
title: "Plan for software updates | System Center Configuration Manager"
ms.custom: na
ms.date: 2016-08-11
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-sum
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d071b0ec-e070-40a9-b7d4-564b92a5465f
caps.latest.revision: 19
author: Dougeby

---
# Plan for software updates in System Center Configuration Manager
<<<<<<< HEAD
Before you implement software updates in a Configuration Manager production environment, you must first plan for this implementation. Use the following sections in this topic to plan for software updates in your Configuration Manager hierarchy:  

-   [Prerequisites for software updates](prerequisites-for-software-updates.md)
-   [Capacity planning for the software update point](capacity-planning-for-the-software-update-point.md)  
-   [Determine the software update point infrastructure](determine-the-software-update-point-infrastructure.md)  
-   [Plan for Software Update Point Installation](plan-for-software-update-point-installation.md)  
-   [Plan for software updates synchronization](plan-for-software-updates-synchronization.md)  
-   [Security and privacy for software updates](security-and-privacy-for-software-updates.md)  
=======
Before you implement software updates in a System Center 2012 Configuration Manager production environment, you must first plan for this implementation. Use the following sections in this topic to plan for software updates in your Configuration Manager hierarchy:  

-   [Capacity planning for the software update point](#BKMK_SUMCapacity)  

-   [Determine the software update point infrastructure](#BKMK_SUPInfrastructure)  

    -   [Software update points in Configuration Manager](#BKMK_SUP)  

        -   [Software update point list](#BKMK_SUPList)  

        -   [Software update point switching](#BKMK_SUPSwitching)  

        -   [Manually switching clients to a new software update point](#BKMK_ManuallySwitchSUPs)

        -   [Software update points in an untrusted forest](#BKMK_SUP_CrossForest)  

        -   [Use an existing WSUS server as the synchronization source at the Top-level site](#BKMK_WSUSSyncSource)  
        -   [Software update point on a secondary site](#BKMK_SUPSecSite)  

-   [Planning for Software Update Point Installation](#BKMK_SUPInstallation)  

    -   [Requirements for the software update point](#BKMK_SUPSystemRequirements)  

    -   [Plan for WSUS installation](#BKMK_PlanningForWSUS)  

    -   [Configure firewalls](#BKMK_ConfigureFirewalls)  

-   [Plan for synchronization settings](#BKMK_SyncSettings)  

    -   [Synchronization source](#BKMK_SyncSource)  

    -   [Synchronization schedule](#BKMK_SyncSchedule)  

    -   [Update classifications](#BKMK_UpdateClassifications)  

    -   [Products](#BKMK_UpdateProducts)  

    -   [Supersedence rules](#BKMK_SupersedenceRules)  

    -   [Languages](#BKMK_UpdateLanguages)  

-   [Plan for settings associated with software updates](#BKMK_Settings)  

    -   [Client settings for software updates](#BKMK_ClientSettings)  

    -   [Client cache setting](#BKMK_ClientCache)  

    -   [Group policy settings for software updates](#BKMK_GroupPolicySettings)  

-   [Plan for a Software Updates Maintenance Window](#BKMK_MaintenanceWindow)  

-   [Restart options for Windows 10 clients after software update installation](#BKMK_RestartOptions)





##  <a name="BKMK_Settings"></a> Plan for settings associated with software updates  
 The software updates client settings in Configuration Manager are site-wide and are configured with default values. There are software updates client settings that affect when software updates are scanned for compliance, and how and when software updates are installed on client computers. There are also Group Policy settings on the client computer that might need to be configured depending on your environment. For more information about how to configure settings that are associated with software updates, see the [Step 4: Verify software updates client settings and group policy configurations](../../sum/deploy-use/configure-software-updates.md#BKMK_AssociatedSettings) section in the [Configure software updates in System Center Configuration Manager](../../sum/deploy-use/configure-software-updates.md) topic.  

###  <a name="BKMK_ClientSettings"></a> Client settings for software updates  
 After you install the software update point, the software updates client agent is enabled by default and you are not required to configure specific client settings, but you should review the settings to ensure that the default values meet your needs. You configure software updates and NAP client settings in **Client Settings** in the **Administration** workspace. For more information about how to configure the settings that are associated with software updates, see the [Client settings for software updates](../../sum/deploy-use/configure-software-updates.md#BKMK_ClientSettings) section in the [Configure software updates in System Center Configuration Manager](../../sum/deploy-use/configure-software-updates.md) topic.  

> [!IMPORTANT]  
>  The **Enable software updates on clients** setting is enabled by default. If you clear this setting, Configuration Manager removes the existing deployment policies from client.  

###  <a name="BKMK_GroupPolicySettings"></a> Group policy settings for software updates  
 There are specific Group Policy settings that are used by Windows Update Agent (WUA) on client computers to connect to the WSUS that runs on the active software updates point, successfully scan for software update compliance, and automatically update the software updates and the WUA.  

> [!WARNING]  
>  If you have an Active Directory Group Policy object assigned to clients that specify a WSUS server that is not a Configuration Manager software update point, it will override the local Group Policy setting that is configured by Configuration Manager. Before you can assess software updates compliance and manage software update deployments on these clients, you must reconfigure the Active Directory Group Policy setting, or move client computers to an organizational unit (OU) that does not have this Group Policy setting applied.  

 For more information about how to configure the settings that are associated with software updates, see the  [Group policy settings for software updates](../../sum/deploy-use/configure-software-updates.md#BKMK_GroupPolicy) section in the [Configure software updates in System Center Configuration Manager](../../sum/deploy-use/configure-software-updates.md) topic.  

###  <a name="BKMK_ClientCache"></a> Client cache setting  
 The Configuration Manager client downloads the content for required software updates to the local client cache soon after it receives the deployment. However, the client waits download the content until after the **Software available time** setting for the deployment. The client does not download software updates in optional deployments (deployments that do not have a scheduled installation deadline) until the user manually initiates the installation. When the configured deadline passes, the software updates client agent performs a scan to verify that the software update is still required, then the software updates client agent checks the local cache on the client computer to verify that the software update source file is still available, and then installs the software update. If the content was deleted from the client cache to make room for another deployment, the client downloads the software updates to the cache. Software updates are always downloaded to the client cache regardless of the configured maximum client cache size. For other deployments, such as applications or packages, the client only downloads content that is within the maximum cache size that you configure for the client. Cached content is not automatically deleted, but it remains in the cache for at least one day after the client used that content.  
