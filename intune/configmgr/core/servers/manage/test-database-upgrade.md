---
title: Test database update
titleSuffix: Configuration Manager
description: Test upgrade the site database when installing updates for Configuration Manager.
ms.date: 02/16/2022
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: how-to
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Test the database upgrade when installing an update

*Applies to: Configuration Manager (current branch)*

If necessary, you can run a test database upgrade before you install an in-console update for the current branch of Configuration Manager.

> [!IMPORTANT]
> The test upgrade is no longer a required or recommend step for most sites.
>
> If your database is suspect, or is modified by customizations not explicitly supported by Configuration Manager, continue to use this process.

## Do I need to run a test upgrade?

The deprecation of this upgrade test is made possible because of changes that are introduced with Configuration Manager current branch. These changes simplify the process and speed by which setup can update a production environment to a newer version. This redesign was done to help you stay current with less risk, and less operational overhead when installing each new update.

The changes are to how updates install, including logic that automatically rolls back a failed update without the need to run a site recovery. These changes enable the use of the console to manage update installations, and include an option to [retry installation of a failed update](post-in-console-updates.md#retry-installation-of-a-failed-update).

> [!TIP]
> When you upgrade to Configuration Manager current branch from an older product, like System Center 2012 Configuration Manager, [test database upgrades remain a recommended step](../deploy/install/upgrade-to-configuration-manager.md#test-the-site-database-upgrade).

If you still plan to test the upgrade of a site database when you install an in-console update, the following information supplements the [guidance on installing an in-console update](install-in-console-updates.md).

## Prepare to run a test database upgrade

To run the upgrade test, use the Configuration Manager Setup from the [CD.Latest folder](the-cd.latest-folder.md). Use the same version of the source files as the version of Configuration Manager to which you're updating.

For example, to test the database update for version YYMM:

- You need at least one site on version YYMM from which you can get that CD.Latest folder.

- If you don't have a site that runs the required version, consider installing a site in a lab environment. Then update that site to the new version. This process creates the CD.Latest folder with the correct version of source files.

The upgrade test runs against a backup of your site database that you restore to a separate instance of SQL Server. After the test upgrade completes, discard the upgraded database. It can't be used by a Configuration Manager site.

## Run the test upgrade

1. Use Configuration Manager Setup and the source files from the **CD.Latest** folder of a site that runs the version that you plan to update to.

1. Copy the **CD.Latest** folder to a location on the SQL Server instance that you'll use to run the test database upgrade.

1. Create a backup of the site database that you want to test upgrade. Then restore a copy of that database to an instance of SQL Server that doesn't host a Configuration Manager site. The SQL Server instance needs to be the same edition of SQL Server as your site database. For more information, see [Quickstart: Backup and restore a SQL Server database on-premises](/sql/relational-databases/backup-restore/quickstart-backup-restore-database).

1. After you restore the database copy, run **Setup** from the CD.Latest folder. When you run Setup, use the `/TESTDBUPGRADE` command-line option. If the SQL Server instance that hosts the database copy isn't the default instance, provide the [command-line options](../deploy/install/command-line-options-for-setup.md#testdbupgrade) to identify the instance that hosts the site database copy.

    For example, you have a site database with the database name `CM_ABC`. You restore a copy of this site database to a supported instance of SQL Server with the instance name `DBTest`. To test an upgrade of this copy of the site database, use the following command line: `setup.exe /TESTDBUPGRADE DBtest\CM_ABC`

    You can find Setup.exe in the following location on the source media for Configuration Manager: `SMSSETUP\BIN\X64`

1. On the instance of SQL Server where you run the upgrade test, monitor the **ConfigMgrSetup.log** in the root of the system drive for progress and success.

    If the test upgrade fails, fix any issues related to the site database upgrade failure. Then, create a new backup of the site database and retest the upgrade of the new copy of the database.

## Next steps

After the test database update completes successfully, discard the updated database. It can't be used by a Configuration Manager site. You can then return to your active site and [begin the update installation](install-in-console-updates.md).

If an update install fails, you shouldn't need to recover the site. Instead, you can retry the update installation from within the console.
