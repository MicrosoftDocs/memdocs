---
title: Deploy software updates
titleSuffix: Configuration Manager
description: Learn how to manually or automatically deploy software updates in the Configuration Manager console.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 11/27/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 04536d51-3bf7-45e5-b4af-36ceed10583d
---

# Deploy software updates  

*Applies to: System Center Configuration Manager (Current Branch)*

The software update deployment phase is the process of deploying the software updates. No matter how you deploy software updates, the site:
- Adds the updates to a software update group
- Distributes the update content to distribution points
- Deploys the update group to clients  

After you create the deployment, the site sends an associated software update policy to targeted clients. The clients download the software update content files from a content source to their local cache. Clients on the internet always download content from the Microsoft Update cloud service. The software updates are then available for installation by the client.   

> [!Tip]  
>  If a distribution point isn't available, clients on the intranet can also download software updates from Microsoft Update.  

> [!NOTE]  
>  Unlike other deployment types, software updates are all downloaded to the client cache. This is regardless of the maximum cache size setting on the client. For more information about the client cache setting, see [Configure the client cache for Configuration Manager clients](/sccm/core/clients/manage/manage-clients#BKMK_ClientCache).  

If you configure a required software update deployment, the software updates are automatically installed at the scheduled deadline. Alternatively, the user on the client computer can schedule or initiate the software update installation prior to the deadline. After the attempted installation, client computers send state messages back to the site server to report whether the software update installation was successful. For more information about software update deployments, see [Software update deployment workflows](/sccm/sum/understand/software-updates-introduction#BKMK_DeploymentWorkflows).  

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

> [!Tip]  
> When manually deploying Office 365 client updates, find them in the **Office 365 Updates** node under **Office 365 Client Management** of the **Software Library** workspace.  



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
Starting in version 1810, create phased deployments for software updates. Phased deployments allow you to orchestrate a coordinated, sequenced rollout of software based on customizable criteria and groups.

For more information, see [Create phased deployments](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json).

