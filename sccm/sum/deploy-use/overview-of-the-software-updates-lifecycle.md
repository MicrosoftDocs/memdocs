---
# required metadata

title: Overview of the software updates lifecycle | Configuration Manager
description:
keywords:
author: dougeby
manager: angrobe
ms.date: 9/14/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: 9919fad4-104d-46f2-93ed-4a9ecb0bbeef

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
#ms.reviewer:
#ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
# Overview of the software updates lifecycle
The overall process for software updates in System Center Configuration Manager includes four main operational phases:

- **Synchronization**: the process of retrieving the software updates metadata from Microsoft Update and inserting it into the site server database.
- **Compliance assessment**: the process that client computers perform to scan for compliance of software updates and report the compliance state for the software updates.
- **Deployment**: the process of manually or automatically deploying the software updates to clients.
- **Monitoring**: the process of monitoring for software update deployment compliance.  

> [!IMPORTANT]  
>  Before software update compliance assessment data is displayed in the Configuration Manager console and before you can deploy the software updates to clients, you must carefully plan for the software updates in your hierarchy and configure the software update dependencies to meet the needs of your environment. For more information about planning for software updates, see [Plan for software updates in System Center Configuration Manager](../../sum/plan-design/plan-for-software-updates.md). For more information about configuring software updates, see [Configure software updates in System Center Configuration Manager](../../sum/deploy-use/configure-software-updates.md).  

