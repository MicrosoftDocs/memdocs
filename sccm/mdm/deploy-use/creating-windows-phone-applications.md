---
title: Create Windows Phone applications
titleSuffix: Configuration Manager
description: How to create and deploy applications for Windows Phone devices in Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 68fe11fa-5fb2-4b81-b0f5-b6f2392fb4ad
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Create Windows Phone applications in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

A Configuration Manager application has one or more deployment types. The deployment type includes the installation files and information that's required to deploy software to a device. A deployment type also has rules that specify when and how the software is deployed.  

See [create an application](/sccm/apps/deploy-use/create-applications#bkmk_create) for the steps to create Configuration Manager applications and deployment types. 

Keep in mind the following considerations when you create and deploy applications for Windows Phone devices:  


Configuration Manager supports deploying the following app file types:  

|Device type|Supported file types|  
|-----------------|---------------------|  
|Windows Phone 8|xap|  
|Windows Phone 8.1|xap, appx, appxbundle|
|Windows 10 Mobile|xap, appx, appxbundle|

Deploy Windows Phone apps as **Available** or **Required**. Also use deployments to uninstall apps.  
