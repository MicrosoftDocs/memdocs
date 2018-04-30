---
title: "Add site system roles"
titleSuffix: "Configuration Manager"
description: "Understand Configuration Manager site system roles and how to add them to extend the functionality and capacity of your site."
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b90de2d9-494e-43ad-b269-c8ed589f37d3
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Add site system roles for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Each System Center Configuration Manager site supports multiple site system roles. Each role extends the functionality and capacity of your site to provide services to the site and to manage devices and users. Each site system role on a site system server must be from the same site.   

Configuration Manager does not support site system roles for multiple sites on a single site system server.  

> [!TIP]  
>  If you're not familiar with the basics for site system roles or the difference between the site server, site system servers, and site system roles, see [Fundamentals of System Center Configuration Manager](../../../../core/understand/fundamentals.md).  

 The following topics detail procedures and related details for installing site system roles:  

-   [Install site system roles for System Center Configuration Manager](../../../../core/servers/deploy/configure/install-site-system-roles.md)  

     This topic provides basic guidance about how to use the two in-console wizards that you can use to install new site system roles.  

-   [Install cloud-based distribution points in Microsoft Azure for System Center Configuration Manager](../../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)  

    When you want to use Microsoft Azure to host content that you deploy to clients, the information in this topic will help you set up the required certificate files to let Configuration Manager communicate with and use your Microsoft Azure subscription. In addition, you will need to set up name resolution to enable your clients to find your cloud-based distribution points.  

-   [Install site system roles for On-premises Mobile Device Management in System Center Configuration Manager](../../../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md)  

     This topic will help you successfully set up your site system roles to support managing modern devices by using Configuration Manager on-premises MDM.  

-   [Configuration options for site system roles for System Center Configuration Manager](../../../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md)  

     Some site system roles support configurations that require more details than the user interface can explain. This topic provides those details.  
