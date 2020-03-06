---
title: Remove CAS
titleSuffix: Configuration Manager
description: Remove the central administration site (CAS) to simplify your Configuration Manager infrastructure to a single, standalone primary site.
ms.date: 03/20/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 16975644-8dfa-4f22-b45a-c54a9250dbd2
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Remove the central administration site

*Applies to: Configuration Manager (current branch)*

<!-- 3607277 -->

Starting in version 2002, if the hierarchy consists of the central administration site (CAS) and a single child primary site, you can remove the CAS. This action simplifies your Configuration Manager infrastructure to a single, standalone primary site. It removes the complexities of site-to-site replication, and focuses your management tasks to the single site.

> [!IMPORTANT]
> In this version of Configuration Manager, this feature is pre-release and not enabled by default. It's currently available for Microsoft Premier customers. In the future, this feature will be available to all customers.
>
> To enable this feature, contact your technical account manager for assistance:
>
> - Your TAM opens an advisory case, which will use your Microsoft Premier hours.
> - You can't change the case severity.
> - Microsoft Support will assist these advisory cases during normal, weekday business hours.

## Plan

- The hierarchy needs to consist of the CAS and a single child primary site. The primary site can have secondary sites. To remove other child primary sites from the hierarchy, review the planning steps and prerequisites to [Uninstall a primary site](/configmgr/core/servers/deploy/install/uninstall-sites-and-hierarchies#bkmk_primary).

- Make sure your child primary site meets the size and scale requirements for a [stand-alone primary site](/configmgr/core/plan-design/configs/size-and-scale-numbers#bkmk_pri).

- Move or retire any site roles at the CAS, except the service connection point and the software update point. Configuration Manager setup handles these two roles when you remove the CAS. The following roles are most common at the CAS that you need to retire or move to the child primary site:

  - Asset Intelligence sync point
  - Endpoint Protection point
  - Reporting services point
  - Data warehouse service point

- Turn off distributed views

- Configuration Manager automatically handles package source locations for built-in packages, like the Configuration Manager client. Review all other content source locations to make sure they aren't using a share on the CAS.

- Stop any active migration jobs and remove all configurations for migration. For more information, see [Stop active migration from another hierarchy](/configmgr/core/servers/deploy/install/prerequisites-for-installing-sites#stop-active-migration-from-another-hierarchy).

- If you use Configuration Manager or System Center Updates Publisher to manage [third-party software updates](/configmgr/sum/deploy-use/third-party-software-updates), export the WSUS signing certificate from the software update point on the CAS.

- Review any third-party software that might have a dependency on the CAS.

## Prerequisites

- The administrative user that runs Configuration Manager setup needs the following security rights:

  - Local **Administrator** rights on the CAS server

  - If the CAS database server is remote from the site server, local **Administrator** rights on the remote site database server for the CAS.

  - **Sysadmin** rights on the CAS site database

  - Local **Administrator** rights on the primary site server

  - If the primary site database server is remote from the primary site server, local **Administrator** rights on the remote site database server for the primary site.

  - **Sysadmin** rights on the primary site database

  - **Infrastructure Administrator** or **Full Administrator** security role on the CAS and primary site

- Only one child primary site in the hierarchy. For more information, see [Uninstall a primary site](/configmgr/core/servers/deploy/install/uninstall-sites-and-hierarchies#bkmk_primary).

## Process

1. Start Configuration Manager setup on the CAS server by using one of the following methods:

    - On the **Start** menu, select **Configuration Manager Setup**.

    - In the directory for the Configuration Manager *installation media*, open `\SMSSETUP\BIN\X64\setup.exe`. Make sure this version is the same as the site version.

    - In the directory where Configuration Manager is *installed*, open `\BIN\X64\setup.exe`.

1. Review the information on the **Before You Begin** page.

1. On the **Getting Started** page, select **Perform site maintenance or reset this site**.

1. On the **Site Maintenance** page, select **Remove central administration site**. <!-- or is it still "delete"? -->

1. On the **Reconfiguring Existing Site System Roles** page:

    - **Service Connection Point**: Enter the fully qualified domain name of the site system in the primary site to host this required role. For more information, see [About the service connection point](/configmgr/core/servers/deploy/configure/about-the-service-connection-point).

    - **Software Update Point**: Select an existing software update point in the primary site. Setup configures this software update point to synchronize the same as the CAS configuration.

    Setup checks that the specified servers meet the prerequisites. Select **Begin Install** when you're ready to continue.

If setup comes across an issue, use the wizard to retry the process.

When setup is complete, it resets the primary site. For more information, see [Run a site reset](/configmgr/core/servers/manage/modify-your-infrastructure#bkmk_reset).

### Monitor and verify

Review the following logs during the setup process:

- `C:\ConfigMgrSetup.log` on the CAS server

- **hman.log** in the Configuration Manager logs directory on the primary site server

Use the **Site Hierarchy** node in the **Monitoring** workspace to visualize the changes to the hierarchy.

<!-- add image examples -->

## Post-setup tasks

After you remove the CAS, review the following steps as they apply to your environment.

- Manually remove the CAS server computer account from the primary site local groups.

- The trusted root key changed, which can require additional actions:

  - Update OS deployment boot images to include the latest Configuration Manager binaries.

  - Recreate [OS deployment media](/configmgr/osd/deploy-use/create-task-sequence-media).

- If you connect Configuration Manager with [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm?context=configmgr/core/context/core-context), you need to reset the connection. The first step to resolve any issues is to [renew the secret key](/configmgr/core/servers/deploy/configure/azure-services-wizard#bkmk_renew). If that doesn't resolve the issue, recreate the connection.<!-- 5584635 -->

- In version 2002, if you enable synchronization of Surface drivers, reconfigure this feature after you remove the CAS. For more information, see [Include Microsoft Surface drivers and firmware updates](/configmgr/sum/get-started/configure-classifications-and-products#bkmk_Surface).<!-- 5728727 -->

- If you manage third-party software updates:

  1. Export the WSUS signing certificate from the software update point on the CAS, if you haven't already.

  1. Before you create any new deployments, remove the update from any existing deployments and software update packages.

  1. To recover software update metadata into a usable state, resynchronize subscribed catalogs. You can also wait for Configuration Manager to automatically resynchronize.

  1. Start or wait for a normal software update sync process to update Configuration Manager with the current status from WSUS. Optionally, use SCUP or WSUS PowerShell cmdlets to delete and readd updates.

  1. Republish content for updates that you need to deploy.
