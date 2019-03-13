---
title: Prepare for on-premises MDM
titleSuffix: Configuration Manager
description: Prepare to manage devices with on-premises mobile device management in Configuration Manager
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 1ef60106-8f31-46d6-95a6-25a6495f22c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---

# Preparation steps for on-premises MDM in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

To manage devices with Configuration Manager on-premises mobile device management (MDM), first set up the necessary infrastructure. The required site system roles need to communicate across a trusted channel with the mobile devices. These roles include the enrollment proxy point, enrollment point, device management point, and distribution point.

The following high-level tasks are required to prepare Configuration Manager for on-premises MDM:  

- [Set up a Microsoft Intune subscription for on-premises MDM](/sccm/mdm/get-started/set-up-intune-subscription-on-premises-mdm)  

    Sign up for Microsoft Intune, and then add the subscription to Configuration Manager through the Configuration Manager console. This step is required for licensing purposes only. Intune isn't used to manage the devices or store management information. All coordination and management of devices is with your organization's enterprise using the on-premises Configuration Manager infrastructure.  

    > [!Note]  
    > Starting in version 1810, an Intune connection is no longer required for new on-premises MDM deployments.<!--3607730, fka 1359124--> Your organization still requires Intune licenses to use this feature. You can't currently remove the Intune connection from existing on-premises MDM deployments. For more information, see the [Intune support blog post](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).  

- [Install site system roles for on-premises MDM](/sccm/mdm/get-started/install-site-system-roles-for-on-premises-mdm)  

    Install and configure the site systems required to manage devices with on-premises Configuration Manager infrastructure. At a minimum, this feature requires the enrollment proxy point, enrollment point, device management point, and distribution point roles.  

- [Set up certificates for trusted communications for on-premises MDM](/sccm/mdm/get-started/set-up-certificates-on-premises-mdm)  

    Configure the on-premises Configuration Manager infrastructure to allow trusted communications (HTTPS) between managed devices and the servers hosting the required site system roles.  

- [Set up device enrollment for on-premises MDM](/sccm/mdm/get-started/set-up-device-enrollment-on-premises-mdm)  

    Grant permission to users to enroll computers and devices. Install the trusted root certificate on devices to permit HTTPS connections to the site system servers. These devices typically aren't domain-joined.  

