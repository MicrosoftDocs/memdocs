---
title: Deploy software updates
titleSuffix: Configuration Manager
description: Learn how to manually or automatically deploy software updates in the Configuration Manager console.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/08/2022
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.localizationpriority: medium
---

# Deploy software updates  

*Applies to: Configuration Manager (current branch)*

The software update deployment phase is the process of deploying software updates. No matter how you deploy software updates, the site:
- Adds the updates to a software update group
- Distributes the update content to distribution points
- Deploys the update group to clients  

After you create the deployment, the site sends an associated software update policy to targeted clients. The clients download the software update content files from a content source to their local cache. Clients on the internet always download content from the Microsoft Update cloud service. The software updates are then available for installation by the client.   

> [!Tip]  
>  If a distribution point isn't available, clients on the intranet can also download software updates from Microsoft Update.  

> [!NOTE]  
>  Unlike other deployment types, software updates are all downloaded to the client cache. This is regardless of the maximum cache size setting on the client. For more information about the client cache setting, see [Configure the client cache](../../core/clients/manage/configure-client-cache.md).

If you configure a required software update deployment, the software updates are automatically installed at the scheduled deadline. Alternatively, the user on the client computer can schedule or initiate the software update installation prior to the deadline. After the attempted installation, client computers send state messages back to the site server to report whether the software update installation was successful. For more information about software update deployments, see [Software update deployment workflows](../understand/software-updates-introduction.md#BKMK_DeploymentWorkflows).  

There are three main scenarios for deploying software updates: 
- [Manual deployment](#BKMK_ManualDeployment)  
- [Automatic deployment](#bkmk_auto)  
- [Phased deployment](#bkmk_phased)  

Typically, you start by manually deploying software updates to create a baseline for your clients, and then you manage software updates on clients by using an automatic or phased deployment.  

> [!Note]  
> You can't use an automatic deployment rule with a phased deployment.



## <a name="BKMK_ManualDeployment"></a> Manually deploy software updates
Select software updates in the Configuration Manager console and manually start the deployment process. You typically use this method of deployment to:  

- Get clients up-to-date with required software updates before you create automatic deployment rules that manage monthly deployments  

- Deploy out-of-band software updates  


The following list provides the general workflow for manual deployment of software updates:  

1. Filter for software updates that use specific requirements. For example, provide criteria that retrieves all security or critical software updates that are required on more than 50 clients.  

2. Create a software update group that contains the software updates.  

3. Download the content for the software updates in the software update group.  

4. Manually deploy the software update group.  

For more information and detailed steps, see [Manually deploy software updates](manually-deploy-software-updates.md).

> [!Note]
> - Starting on April 21, 2020, Office 365 ProPlus is being renamed to **Microsoft 365 Apps for enterprise**. For more information, see [Name change for Office 365 ProPlus](/deployoffice/name-change). You may still see references to the old name in the Configuration Manager console and supporting documentation while the console is being updated.
> - When manually deploying Microsoft 365 Apps client updates, find them in the **Office 365 Updates** node under **Office 365 Client Management** of the **Software Library** workspace. 

## <a name="bkmk_auto"></a> Automatically deploy software updates

Configure automatic software updates deployment by using an automatic deployment rule (ADR). This method of deployment is common for monthly software updates (typically known as "Patch Tuesday") and for managing definition updates. You define the criteria for an ADR to automate the deployment process. The following list provides the general workflow to automatically deploy software updates:  

1.  Create an ADR that specifies deployment settings.  

2.  The site adds the software updates to a software update group.  

3.  The site deploys the software update group to the clients in the target collection.  

First, determine your automatic software update deployment strategy. For example, create the ADR to initially target a collection of test clients. After you verify the test group successfully installed the software updates, add a new deployment to the rule. You could also change the targeted collection in the existing deployment to one that includes a larger set of clients. Consider the following behaviors when deciding upon the strategy to use:  

- You're able to modify the properties of the software update objects that the ADR creates.   

- The ADR automatically deploys software updates to clients when you add them to the target collection.  

- When you or the ADR adds new software updates to the software update group, the site automatically deploys them to the clients in the target collection.  

- Enable or disable deployments at any time for the ADR.  


After you create an ADR, add additional deployments to the rule. This action helps you manage the complexity of deploying different updates to different collections. Each new deployment has the full range of functionality and deployment monitoring experience.  

Each new deployment that you add:  

- Uses the same update group and package, which the ADR creates when it first runs  
- Can target a different collection  
- Supports unique deployment properties including:  
  -   Activation time  
  -   Deadline  
  -   User experience  
  -   Separate alerts for each deployment  


For more information and detailed steps, see [Automatically deploy software updates](automatically-deploy-software-updates.md)



## <a name="bkmk_phased"></a> Deploy software updates in phases

<!--1358146-->
Create phased deployments for software updates. Phased deployments allow you to orchestrate a coordinated, sequenced rollout of software based on customizable criteria and groups.

For more information, see [Create phased deployments](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/sum/toc.json&bc=/mem/configmgr/sum/breadcrumb/toc.json).


## <a name="bkmk_folder"></a> Folder support for software update nodes
<!--3601129-->

Starting in version 2203, you can organize software update groups and packages by using folders. This change allows for better categorization and management of software updates.

1. Open the Configuration Manager console and go to the **Software Library** workspace.
1. From the ribbon or right-click menu, in the **Software Updates Groups** or **Deployment Packages** nodes, select from the following options:
   - **Create Folder**
   - **Delete Folder**
   - **Rename Folder**
   - **Move Folders**
   - **Set Security Scopes**
