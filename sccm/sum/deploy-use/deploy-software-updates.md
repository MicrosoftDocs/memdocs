---
# required metadata

title: Deploy software updates | Configuration Manager
description:
keywords:
author: dougeby
manager: angrobe
ms.date: 9/14/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: 04536d51-3bf7-45e5-b4af-36ceed10583d

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
#ms.reviewer:
#ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

#  <a name="BKMK_SUMDeploy"></a> Deploy software updates  
 The software update deployment phase is the process of deploying the software updates. Typically, you add software updates to a software update group and then deploy the software update group to clients. When you create the deployment, the software update policy is sent to client computers, the software update content files are downloaded from a distribution point to the local cache on the client computer, and then the software updates are available for installation on the client. Clients on the Internet download content from Microsoft Update.  

> [!NOTE]  
>  You can configure a client on the intranet to download software updates from Microsoft Update if a distribution point is not available.  

> [!NOTE]  
>  Unlike other deployment types, software updates are all downloaded to the client cache regardless of the maximum cache size setting on the client. For more information about the client cache setting, see [Configure the Client Cache for Configuration Manager Clients](../../core/clients/manage/manage-clients.md#BKMK_ClientCache).  

 If you configure a required software update deployment, the software updates are automatically installed at the scheduled deadline. Alternatively, the user on the client computer can schedule or initiate the software update installation prior to the deadline. After the attempted installation, client computers send state messages back to the site server to report whether the software update installation was successful. For more information about software update deployments, see [Software update deployment workflows](../understand/software-updates-introduction.md#BKMK_DeploymentWorkflows).  

## Choose how to deploy software updates
There are two main scenarios for deploying software updates: manual deployment and automatic deployment. Typically, you will initially manually deploy software updates to create a baseline for your client computers, and then you will manage software updates on clients by using automatic deployment.  r manual and automatic deployment workflows for software updates.  

### Manually deploy software updates
[Manually deploy software updates](manually-deploy-software-updates.md)

### Automatically deploy software updates
[Automatically deploy software updates](automatically-deploy-software-updates.md)
    
 <!--- For more information about the deployment process, see [Software update deployment process](../../sum/understand/software-updates-introduction.md#BKMK_DeploymentProcess).  --->

