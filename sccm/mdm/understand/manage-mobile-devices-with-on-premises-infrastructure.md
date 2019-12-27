---
title: On-premises MDM
titleSuffix: Configuration Manager
description: Learn about on-premises mobile device management, a device management solution in Configuration Manager
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 497c05c7-fe9f-4b88-983b-1c5b3d59308e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---

# On-premises MDM in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Configuration Manager on-premises mobile device management (MDM) is a device management solution that relies on the built-in management capabilities of device OS. This feature is based on the Open Mobile Alliance (OMA) Device Management (DM) standard. It uses your organization's Configuration Manager infrastructure to manage and maintain the devices. On-premises MDM requires Microsoft Intune to set up the management capability, but it's only needed for the subscription. Intune is used at times to help notify devices to check in for policy changes, but it's not used to manage devices or store data about them.  

![On\-premises conceptual](media/On-premises-conceptual.png)  

On-premises MDM differs from Microsoft Intune, which also relies on built-in OMA DM capabilities. All of the management functions in Intune are delivered through cloud services. On-premises MDM also differs from the client-based management solution traditionally offered by Configuration Manager. It relies on similar infrastructure but doesn't use separately installed client software on the devices it manages.  

> [!Note]  
> Starting in version 1810, an Intune connection is no longer required for new on-premises MDM deployments.<!--3607730, fka 1359124--> Your organization still requires Intune licenses to use this feature. You can't currently remove the Intune connection from existing on-premises MDM deployments. For more information, see the [Intune support blog post](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).  

The following table lists the advantages and disadvantages of on-premises MDM as compared to traditional client-based management:  

|Advantages|Disadvantages|  
|----------------|-------------------|  
|**Simplified infrastructure** - Fewer site system roles are required.<br /><br /> **Easier to maintain** - Because management functionality is built in to the device operating system, new versions of the client software are not required when new management features are introduced to the Configuration Manager system.<br /><br /> **On-premises** - All management and data kept on-premises.|**Less client management functionality** - No orchestration, software metering, third-party integration, task sequencing, or software center support.<br /><br /> **Limited device support** - currently on-premises MDM only supports devices running Windows 10 and Windows 10 Mobile.|  

The following articles provide information you can use to plan, prepare, and enroll devices for on-premises MDM:  

- [Plan for on-premises MDM](/sccm/mdm/plan-design/plan-on-premises-mdm)  

    Learn about what to consider when setting up the Configuration Manager infrastructure and planning for device enrollment in on-premises MDM.  

- [Preparation steps for on-premises MDM](/sccm/mdm/get-started/preparation-steps-for-on-premises-mdm)  

    Get Configuration Manager ready for on-premises MDM. Set up the Microsoft Intune subscription, set up certificates, install site system roles, and set up device enrollment.  

- [Enroll devices for on-premises MDM](/sccm/mdm/deploy-use/enroll-devices-on-premises-mdm)  

    Learn about how enrollment occurs, how users can enroll their own devices, and how to bulk-enroll devices with an enrollment package.  

