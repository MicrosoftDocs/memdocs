---
title: Remove CAS
titleSuffix: Configuration Manager
description: Remove the central administration site (CAS) to simplify your Configuration Manager infrastructure to a single, standalone primary site.
ms.date: 03/20/2020
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 16975644-8dfa-4f22-b45a-c54a9250dbd2
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Remove the central administration site

*Applies to: Configuration Manager (current branch)*

Starting in version 2002, if the hierarchy consists of the central administration site (CAS) and a single child primary site, you can remove the CAS. This action simplifies your Configuration Manager infrastructure to a single, standalone primary site. It removes the complexities of site-to-site replication, and focuses your management tasks to the single site.

> [!IMPORTANT]
> Configuration Manager doesn't enable this feature by default. To enable this feature, contact Microsoft Support for assistance. <!-- what do they ask for? is a paid incident? are there specific days/hours? -->

## Plan



- Move roles. Setup handles SCP & SUP
- Turn off distributed views

## Prerequisites

- Admin rights on CAS and PRI SQL
- Only one child primary site in the hierarchy. For more information, see [Uninstall a primary site](/configmgr/core/servers/deploy/install/uninstall-sites-and-hierarchies#bkmk_primary).

## Process

1. Run setup on the CAS server.
1. On the **Getting Started** page, select **Perform site maintenance or reset this site**.
1. On the **Site Maintenance** page, select **Remove central administration site**. <!-- or is it still "delete"? -->
1. On the **Reconfiguring Existing Site System Roles** page:

    - **Service Connection Point**: Enter the fully qualified domain name of the site system in the primary site to host this required role. For more information, see [About the service connection point](/configmgr/core/servers/deploy/configure/about-the-service-connection-point).

    - **Software Update Point**: Select an existing software update point in the primary site.

    Setup checks that the specified servers meet the prerequisites. Select **Begin Install** when you're ready to continue.

Review `C:\ConfigMgrSetup.log` on the CAS server, as well as hman.log in the Configuration Manager logs directory.

Use the **Site Hierarchy** node in the **Monitoring** workspace