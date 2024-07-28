---
title: Configure a remote content library
titleSuffix: Configuration Manager
description: Learn how to relocate the site server's content library to another storage location.
ms.date: 08/02/2021
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: how-to
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Configure a remote content library for the site server

*Applies to: Configuration Manager (current branch)*

<!--1357525-->

To configure [site server high availability](../../servers/deploy/configure/site-server-high-availability.md) or to free up hard drive space on your central administration or primary site servers, relocate the content library to another storage location. Move the content library to another drive on the site server, a separate server, or fault-tolerant disks in a storage area network (SAN). A SAN is recommended, because it's highly available, and provides elastic storage that grows or shrinks over time to meet your changing content requirements. For more information, see [High availability options](../../servers/deploy/configure/site-server-high-availability.md).

A remote content library is a prerequisite for [site server high availability](../../servers/deploy/configure/site-server-high-availability.md).

This action only moves the content library on the site server. It doesn't impact the location of the content library on distribution points.

> [!TIP]
> Also plan for managing package source content, which is external to the content library. Every software object in Configuration Manager has a package source on a network share. Consider centralizing all sources to a single share, but make sure this location is redundant and highly available.
>
> If you move the content library to the same storage volume as your package sources, you can't mark this volume for data deduplication. While the content library supports data deduplication, the package sources volume doesn't support it. For more information, see [Data deduplication](../configs/support-for-windows-features-and-networks.md#bkmmk_datadedup).<!--SCCMDOcs issue #831-->

## Prerequisites

- The site server computer account needs **Full control** permissions to the network path to which you're moving the content library. This permission applies to both the share and the file system. No components are installed on the remote system.

- The site server can't have the distribution point role. The distribution point also uses the content library, and this role doesn't support a remote content library. After moving the content library, you can't add the distribution point role to the site server.

  > [!NOTE]
  > The **Manage Content Library** option isn't available if the distribution point role exists on the site server. To enable the option, remove the distribution point role from the site server.

- The remote system for the content library needs to be in a trusted domain.

> [!IMPORTANT]
> Don't reuse a shared network location between multiple sites. For example, don't use the same path for both a central administration site and a child primary site. This configuration has the potential to corrupt the content library, and require you to rebuild it.<!--SCCMDocs-pr issue 2764-->

## Manage the content library

1. Create a folder in a network share as the target for the content library. For example, `\\server\share\folder`.

    > [!WARNING]
    > Don't reuse an existing folder with content. For example, don't use the same folder as your package sources. Before copying the content library, Configuration Manager removes any existing content from the location you specify.

1. In the Configuration Manager console, switch to the **Administration** workspace. Expand **Site Configuration**, select the **Sites** node, and select the site. On the **Summary** tab at the bottom of the details pane, notice a new column for the **Content Library**.

1. Select **Manage Content Library** on the ribbon.

1. In the Manage Content Library window, the **Current Location** field shows the local drive and path. Enter a valid network path for the **New Location**. This path is the location to which the site moves the content library. It must include a folder name that already exists on the share, for example, `\\server\share\folder`. Select **OK**.

1. Note the **Status** value in the Content Library column on the Summary tab of the details pane. It updates to show the site's progress in moving the content library.

    - While **In progress**, the **Move Progress (%)** value displays the percentage complete.

        > [!NOTE]
        > If you have a large content library, you may see `0%` progress in the console for a while. For example, with a 1 TB library, it has to copy 10 GB before it shows `1%`. Review **distmgr.log**, which shows the number of files and bytes copied. The log file also shows an estimated time remaining.

    - If there's an error state, the status displays the error. Common errors include **access denied** or **disk full**.

    - When complete it displays **Complete**.

    See the **distmgr.log** for details. For more information, see [Site server and site system server logs](log-files.md#BKMK_SiteSiteServerLog).

    > [!NOTE]
    > Starting in version 2010, you can enable verbose logging to troubleshoot the content library move process. Set the following registry key on the site server: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP, LibraryMoveVerboseLog = 1 (REG_DWORD)`.

For more information on this process, see [Flowchart - Manage content library](manage-content-library-flowchart.md).

The site actually *copies* the content library files to the remote location. This process doesn't delete the content library files at the original location on the site server. To free up space, an administrator must manually delete these original files.

If the original content library spans two drives, it's merged into a single folder at the new destination.

During the copy process, the **Despooler** and **Distribution manager** components don't process new packages. This action makes sure that content isn't added to the library while it's moving. Regardless, schedule this change during a system maintenance.

If you need to move the content library back to the site server, repeat this process, but enter a local drive and path for the **New Location**. It must include a folder name that already exists on the drive, for example, `D:\SCCMContentLib`. When the original content still exists, the process quickly moves the configuration to the location local to the site server.

> [!TIP]
> To move the content to another drive on the site server, use the **Content Library Transfer** tool. For more information, see the [Content Library Transfer tool](../../support/content-library-transfer.md).

## Support untrusted domains

<!-- 3766940 -->

If your environment has distribution points in untrusted domains, you need to make other configuration changes.

1. On the computer that will host the distribution point role in the untrusted domain:

    1. Create a local user account.

    1. When you [add the distribution point role](../../servers/deploy/configure/install-site-system-roles.md) to this computer, use this local account as the [site system installation account](accounts.md#site-system-installation-account). For example, `COMPUTER.UNTRUSTEDDOMAIN\LocalAccount`.

1. On the server that hosts the remote content library for the site, create a local user account. This account should have the same name and password as the account in the first step.

When the distribution manager component distributes content to the server in the untrusted domain, it will use the local user account. During content distribution, this component gets the files from the content library server in the context of the distribution point's local account. Since this same account exists on the content library server, distribution manager can authenticate to read the content files and copy to the remote distribution point.

## Next steps

[Flowchart - Manage content library](manage-content-library-flowchart.md)
