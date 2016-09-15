---
# required metadata

title: Plan for software updates capacity | Configuration Manager
description:
keywords:
author: dougeby
manager: angrobe
ms.date: 9/14/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: bec30e2e-a599-4b27-aaf0-eeae44b7346a

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
#ms.reviewer:
#ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Plan for software updates capacity
 You can use the following recommendations as a baseline that can help you determine the information for the software updates capacity planning that is appropriate to your organization. The actual capacity requirements might vary from the recommendations that are listed in this topic depending on the following criteria: your specific networking environment, the hardware that you use to host the software update point site system, the number of clients that are installed, and the site system roles that are installed on the server.  

##  <a name="BKMK_SUMCapacity"></a> Capacity planning for the software update point  
 The number of supported clients depends on the version of Windows Server Update Services (WSUS) that runs on the software update point, and it also depends on whether the software update point site system role co-exists with another site system role:  

-   The software update point can support up to 25,000 clients when WSUS runs on the software update point computer and the software update point co-exists with another site system role.  

-   The software update point can support up to 150,000 clients when the remote computer meets the WSUS requirements to support this number of clients.   
    By default, Configuration Manager does not support configuring software update points as NLB clusters. However, you can use the Configuration Manager SDK to configure up to four software update points on a NLB cluster.  

## Capacity planning for software updates objects  
 Use the following capacity information to plan for software updates objects.  

-   **Limit of 1000 software updates in a deployment**  

     You must limit the number of software updates to 1000 for each software update deployment. When you create an automatic deployment rule, specify a criteria that limits the number of software updates that are returned. The automatic deployment rule fails when the criteria that you specify returns more than 1000 software updates. You can check the status of the automatic deployment rule from the **Automatic Deployment Rules** node in the Configuration Manager console. When you manually deploy software updates, do not select more than 1000 updates to deploy.  

     You must also limit the number of software updates to 1000 in a configuration baseline. For more information, see [How to create configuration baselines](../../compliance/deploy-use/create-configuration-baselines.md).
