---
title: Add site system roles
titleSuffix: Configuration Manager
description: Understand Configuration Manager site system roles and how to add them to extend the functionality and capacity of your site.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b90de2d9-494e-43ad-b269-c8ed589f37d3
author: mestew
ms.author: mstewart
manager: dougeby
---

# Add site system roles for Configuration Manager

*Applies to: Configuration Manager (current branch)*

Each Configuration Manager site supports multiple site system roles. Each role extends the functionality and capacity of your site to provide services to the site and to manage devices and users. Each site system role on a site system server must be from the same site.

Configuration Manager doesn't support site system roles for multiple sites on a single site system server.

> [!TIP]
> If you're not familiar with the basics for site system roles or the difference between the site server, site system servers, and site system roles, see [Fundamentals of Configuration Manager](../../../understand/fundamentals.md).

The following articles detail procedures and related details for installing site system roles:

- [Install site system roles](install-site-system-roles.md): Basic guidance about how to use the two in-console wizards to install new site system roles.

- [Install cloud-based distribution points](install-cloud-based-distribution-points-in-microsoft-azure.md): Use Microsoft Azure to host content that you deploy to clients.

- [Install site system roles for on-premises mobile device management (MDM)](../../../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md): Set up your site system roles to support managing modern devices by using Configuration Manager on-premises MDM.

- [Configuration options for site system roles](configuration-options-for-site-system-roles.md): Some site system roles support configurations that require more details than the user interface can explain.

- [Remove a site system role](../install/uninstall-sites-and-hierarchies.md#bkmk_role): Guidance and procedures to remove roles from site system servers.
