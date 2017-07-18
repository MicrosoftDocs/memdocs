---
title: "Choose Intune standalone or hybrid MDM | Microsoft Docs"
description: "Choose whether to deploy hybrid mobile device management with Intune and Configuration Manager or run Intune standalone."
ms.custom: na
ms.date: 07/13/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 73ff9bb9-e605-4b68-92a1-487684fed42d
caps.latest.revision: 10
author: dougeby
ms.author: dougeby
manager: angrobe
---
# Choose between Microsoft Intune standalone and hybrid mobile device management with System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

One of the most commonly asked questions regarding mobile device management (MDM) with Microsoft Intune is "Should I integrate Intune with Configuration Manager (hybrid MDM) or run Intune standalone in the cloud only configuration?" To answer that question, you should carefully compare the two options.

## Intune standalone
Intune standalone is Microsoft’s recommend deployment topology.  Intune standalone is a cloud-only MDM solution and is managed using a web console that can be accessed from anywhere in the world. Intune datacenters are hosted in North America, Europe, and Asia. Because Intune is a cloud service, you can deploy Intune management to your devices in a relatively short timeframe.

Customers generally find it faster and easier to deploy the standalone topology because there is no dependency for on-premise components. Intune standalone is now on the Microsoft Azure cloud platform and provides many advanced features, such as:
- Integrated enterprise mobility management platform - An integrated cloud platform and admin experience in Azure portal for Intune, Azure AD Premium, and Azure Information Protection.
- Mobile device management - Rich mobile device management and information protection capabilities.
- Scale - Deploy and manage mobile devices without worrying about scale.
- Role-based Access Control – restrict access to administrative functions based on assigned roles and scopes.
- Programmatic access (API) - Microsoft Graph API support, and SDK and PowerShell management options.
- Web console - An HTML 5-based console built on web standards with support for most modern web browsers.
- Advanced reporting - ability to create customized reports.
- Agility - Simple setup and rapid delivery of new capabilities.


## Hybrid MDM with Configuration Manager
Hybrid MDM is a solution that integrates Intune's mobile device management capabilities into Configuration Manager. It uses Intune as the delivery channel for policies, profiles, and applications to devices but uses Configuration Manager on-premises infrastructure to administer content and manage the devices. A hybrid implementation gives you “single pane of glass” control.  This means you can use the same on-premises infrastructure and administrative console to manage mobile devices with Intune as well as PCs and servers with the traditional Configuration Manager client. You may choose hybrid MDM for the following reasons:  
- You want to manage both mobile devices enrolled in Intune and devices managed with the Configuration Manager client from the same administrative console
- Your infrastructure requires that you have multiple NDES servers for certificate delivery to mobile devices
- Your infrastructure requires that you have multiple Exchange connectors
- You require S/MIME encryption support


## Changing the MDM authority setting
If you need to change the MDM authority setting, you can change it yourself without having to contact Microsoft Support, and without having to unenroll and reenroll your existing managed devices. For details, see [Change your MDM authority](/sccm/mdm/deploy-use/change-mdm-authority.md).

> [!NOTE]    
> You must have Configuration Manager version 1610 or later to change your MDM authority to Intune standalone. When you have an earlier version of Configuration Manager, you can change the MDM authority, but it requires help from Microsoft support and operations. It also requires you to unenroll and reenroll all your devices after the MDM authority is changed.  
