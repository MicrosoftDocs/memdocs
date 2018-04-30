---
title: "Preparation steps "
titleSuffix: "Configuration Manager"
description: "Prepare to manage devices with On-premises Mobile Device Management in System Center Configuration Manager."
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 1ef60106-8f31-46d6-95a6-25a6495f22c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Preparation steps for On-premises Mobile Device Management in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Managing devices with System Center Configuration Manager On\-premises Mobile Device Management requires the Configuration Manager infrastructure to be set up so that the required site system roles (enrollment proxy point, enrollment point, device management point, and distribution point) can communicate across a trusted channel with the mobile devices to be managed.  

 The following high-level tasks are required to prepare the Configuration Manager system for On\-premises Mobile Device Management:  

-   [Set up a Microsoft Intune subscription for On-premises Mobile Device Management in System Center Configuration Manager](../../mdm/get-started/set-up-intune-subscription-on-premises-mdm.md)  

     In this task, you sign up for Microsoft Intune, and then add the subscription to Configuration Manager through the Configuration Manager console. This step is required for licensing purposes only. Intune is not used to manage the devices or store management information. All coordination and management of devices is with your organization's enterprise using the on-premises Configuration Manager infrastructure.  

-   [Install site system roles for On-premises Mobile Device Management in System Center Configuration Manager](../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md)  

     In this task, you install and configure the site system roles required to manage devices with on-premises Configuration Manager infrastructure. On\-premises Mobile Device Management minimally requires the enrollment proxy point, enrollment point, device management point, and distribution point site system roles.  

-   [Set up certificates for trusted communications for On-premises Mobile Device Management in System Center Configuration Manager](../../mdm/get-started/set-up-certificates-on-premises-mdm.md)  

     In this task, you configure the on-premises Configuration Manager infrastructure to allow trusted communications (HTTPS) between managed devices and the servers hosting the required site system roles.  

-   [Set up device enrollment for On-premises Mobile Device Management in System Center Configuration Manager](../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md)  

     In this task, you grant permission to users to enroll computers and devices and you install the trusted root certificate on devices (typically ones that are not domain-joined) to permit HTTPS connections to the site system servers.  
