---
title: Deploy software updates
titleSuffix: "Configuration Manager"
description: "Choose software updates in the Configuration Manager console to manually start the deployment process or automatically deploy updates."
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 02/16/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 04536d51-3bf7-45e5-b4af-36ceed10583d
---

#  <a name="BKMK_SUMDeploy"></a> Deploy software updates  

*Applies to: System Center Configuration Manager (Current Branch)*

The software update deployment phase is the process of deploying the software updates. No matter how you deploy software updates, the updates are typically:
- Added to a software update group.
- Downloaded to distribution points.
- The update group is deployed to clients. 
After you create the deployment, an associated software update policy is sent to client computers. The software update content files are downloaded from a distribution point to the local cache on client computers. The software updates are then available for installation by the client. Clients on the Internet download content from Microsoft Update.  

> [!NOTE]  
>  If a distribution point is not available, you can configure a client on the intranet to download software updates from Microsoft Update.  

> [!NOTE]  
>  Unlike other deployment types, software updates are all downloaded to the client cache. This is regardless of the maximum cache size setting on the client. For more information about the client cache setting, see [Configure the Client Cache for Configuration Manager Clients](../../core/clients/manage/manage-clients.md#BKMK_ClientCache).  

If you configure a required software update deployment, the software updates are automatically installed at the scheduled deadline. Alternatively, the user on the client computer can schedule or initiate the software update installation prior to the deadline. After the attempted installation, client computers send state messages back to the site server to report whether the software update installation was successful. For more information about software update deployments, see [Software update deployment workflows](../understand/software-updates-introduction.md#BKMK_DeploymentWorkflows).  

There are two main scenarios for deploying software updates: manual deployment and automatic deployment. Typically, you start by manually deploying software updates to create a baseline for your client computers, and then you manage software updates on clients by using automatic deployment.  

## <a name="BKMK_ManualDeployment"></a> Manually deploy software updates
You can select software updates in the Configuration Manager console and manually start the deployment process. You typically use this method of deployment to get the client computers up-to-date with required software updates before you create automatic deployment rules that manage ongoing monthly software update deployments, and to deploy out of band software update requirements. The following list provides the general workflow for manual deployment of software updates:  

1. Filter for software updates that use specific requirements. For example, you could provide criteria that retrieves all security or critical software updates that are required on more than 50 client computers.  
2. Create a software update group that contains the software updates.  
3. Download the content for the software updates in the software update group.  
4. Manually deploy the software update group.

For detailed steps, see [Manually deploy software updates](manually-deploy-software-updates.md).

>[!NOTE]
>Starting in Configuration Manager version 1706 Office 365 client updates have moved to the **Office 365 Client Management** >**Office 365 Updates** node. This will not impact your ADR configuration but does affect manual deployment of Office 365 updates. 

## Automatically deploy software updates
Automatic software updates deployment is configured by using an automatic deployment rule (ADR). This is a common method of deployment for monthly software updates (typically known as "Patch Tuesday") and for managing definition updates. When the rule runs, software updates are removed from the software update group (if using an existing update group), the software updates that meet a specified criteria (for example, all security software updates released in the last month) are added to a software update group, the content files for the software updates are downloaded and copied to distribution points, and the software updates are deployed to clients in the target collection. The following list provides the general workflow to automatically deploy software updates:  

1.  Create an ADR that specifies deployment settings.
2.  The software updates are added to a software update group.  
3.  The software update group is deployed to the client computers in the target collection, if it is specified.  

You must determine what deployment strategy to use in your environment. For example, you might create the ADR and target a collection of test clients. After you verify that the software updates are installed on the test group, you can add a new deployment to the rule or change the collection in the existing deployment  to a target collection that includes a larger set of clients. The software update objects that are created by the ADRs are interactive.  

-   Software updates that were deployed by using an ADR are automatically deployed to new clients added to the target collection.  
-   New software updates added to a software update group are automatically deployed to the clients in the target collection.  
-   You can enable or disable deployments at any time for the ADR.  

After you create an ADR, you can add additional deployments to the rule. This can help you manage the complexity of deploying different updates to different collections. Each new deployment has the full range of functionality and deployment monitoring experience, and each new deployment that you add:  

-   Uses the same update group and package, which is created when the ADR first runs  
-   Can specify a different collection  
-   Supports unique deployment properties including:  
   -   Activation time  
   -   Deadline  
   -   Show or hide end-user experience  
   -   Separate alerts for this deployment  

For detailed steps, see [Automatically deploy software updates](automatically-deploy-software-updates.md)

<!-- ###  <a name="BKMK_ClientCache"></a> Client cache setting  
The Configuration Manager client downloads the content for required software updates to the local client cache soon after it receives the deployment. However, the client waits to download the content until after the **Software available time** setting for the deployment. The client does not download software updates in optional deployments (deployments that do not have a scheduled installation deadline) until the user manually starts the installation. When the configured deadline passes, the software updates client agent performs a scan to verify that the software update is still required, then the software updates client agent checks the local cache on the client computer to verify that the software update source file is still available, and then installs the software update. If the content was deleted from the client cache to make room for another deployment, the client downloads the software updates to the cache. Software updates are always downloaded to the client cache regardless of the configured maximum client cache size. For other deployments, such as applications or packages, the client only downloads content that is within the maximum cache size that you configure for the client. Cached content is not automatically deleted, but it remains in the cache for at least one day after the client used that content.  -->


 <!-- For more information about the deployment process, see [Software update deployment process](../../sum/understand/software-updates-introduction.md#BKMK_DeploymentProcess).  -->
