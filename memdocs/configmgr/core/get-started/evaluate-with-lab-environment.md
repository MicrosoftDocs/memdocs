---
title: Evaluate in a lab environment
titleSuffix: Configuration Manager
description: Create a lab environment to evaluate Configuration Manager for use in your organization.
ms.date: 02/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Evaluate Configuration Manager by building your own lab environment

*Applies to: Configuration Manager (current branch)*

 Learn how to create a lab environment to evaluate Configuration Manager for use in your organization.  

 Configuration Manager is a complex and powerful tool to manage your users, devices, and software. It's a good idea to thoroughly evaluate Configuration Manager before full deployment, so that you can marry conceptual understanding with hands-on exercises.  

 This guide is primarily meant for admins who are evaluating the use of Configuration Manager in corporate environments:  

-   Admins who want a solution to fully manage PCs, servers, and mobile devices  

-   Admins in high-security industries that require the security of on-premises device management with the flexibility of cloud-based device management  

-   Admins who want to manage the scaling-up of their on-premises server architecture  

## What this lab does  
 The main goal of creating this lab environment is to give you the general knowledge to start working with Configuration Manager, and to enhance your understanding of Configuration Manager. You'll walk through an expedited assembly of the current version of Configuration Manager, by using two servers:  

-   One that hosts Active Directory, the domain controller, and the DNS server  

-   One that hosts Configuration Manager and all associated SQL Server components  

Client machines are installed within Hyper-V. The lab itself can also be run as a fully virtualized system on a single server.  

## What this lab does not do  
 This lab will not take you through all Configuration Manager scenarios. It is not designed to be immediately migrated into an active environment.  

 When you build this lab, you will have a functional environment to work in. But this environment will not be optimized for factors like system performance, hard disk space management, and SQL Server storage.  

##  <a name="BKMK_EvalRec"></a> Recommended reading before you build the lab  
 There is a wealth of content available in [Documentation for Configuration Manager](/sccm/). We recommend that you read the following topics from this library before you start to build the lab:  

-   Learn core concepts about the Configuration Manager console, end-user portals, and example scenarios in [Introduction to Configuration Manager](../../core/understand/introduction.md).  

-   Learn about the primary management capabilities of Configuration Manager in [Features and capabilities of Configuration Manager](../../core/plan-design/changes/features-and-capabilities.md).  

-   Bolster your knowledge with [Fundamentals of Configuration Manager](../../core/understand/fundamentals.md).  

-   Learn the importance of security roles in [Fundamentals of role-based administration for Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

-   Learn about content management in [Concepts for content management](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

-   Learn how to successfully support daily tasks throughout your deployment in [Understand how clients find site resources and services for Configuration Manager](../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).