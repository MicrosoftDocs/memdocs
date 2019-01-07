---
title: "Test database update"
titleSuffix: "Configuration Manager"
description: "Test upgrade the site database when installing updates for Configuration Manager."
ms.date: 06/13/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: abb696f3-a816-4f12-a9f1-0503a81e1976
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Test the database upgrade when installing an update

*Applies to: System Center Configuration Manager (Current Branch)*

The information in this topic can help you run a test database upgrade before you install an in-console update for the current branch of Configuration Manager. However, the test upgrade is no longer a required or recommend step unless your database is suspect, or is modified by customizations not explicitly supported by Configuration Manager.

## Do I need to run a test upgrade?
The deprecation of this upgrade test is made possible due to changes that are introduced with System Center Configuration Manager. These changes simplify the process and speed by which a production environment can be updated to newer versions. This redesign was done to help customers stay current with less risk, and less operational overhead when installing each new update.

The changes are to how updates install, including logic that automatically rolls back a failed update without the need to run a site recovery. These changes enable the use of the console to manage update installations, and include an option to [retry installation of a failed update](/sccm/core/servers/manage/install-in-console-updates#bkmk_retry).

> [!TIP]
> When you upgrade to System Center Configuration Manager from an older product, like System Center 2012 Configuration Manager, [test database upgrades remain a recommended step](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager#a-namebkmktesta-test-the-site-database-upgrade).

If you still plan to test the upgrade of a site database when you install an in-console update, the following information supplements the [guidance on installing an in-console update](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates).

## Prepare to run a test database upgrade  
Before you install a new update in your hierarchy, like update 1702, you can test the upgrade of your site database.

To run the upgrade test, use the Configuration Manager Setup from the source files from [the CD.Latest folder](/sccm/core/servers/manage/the-cd.latest-folder) of a site that runs the version of Configuration Manager that you are updating to. This requirement means that to test the database update for update to 1702:
-   You must have at least one site that runs version 1702 from which you can get that CD.Latest folder.
-   If you do not have a site that runs the required version, consider installing a site in a lab environment, and then update that site to the new version. This creates the CD.Latest folder with the correct version of source files.

The upgrade test is run against a backup of your site database that you restored to a separate instance of SQL Server.  You run Setup from the **CD.Latest** folder with the **testdbupgrade** command-line switch to test upgrade that restored copy of the database. After the test upgrade completes, the upgraded database is discarded. It cannot be used by a Configuration Manager site.

If an update install fails, you should not need to recover the site. Instead, you can retry the update installation from within the console.

##  Run the test upgrade    
1. Use Configuration Manager Setup and the source files from the **CD.Latest** folder of a site that runs the version that you plan to update to.  

2. Copy the **CD.Latest** folder to a location on the SQL Server instance that you will use to run the test database upgrade.

3. Create a backup of the site database that you want to test upgrade. Next, restore a copy of that database to an instance of SQL Server that does not host a Configuration Manager site. The SQL Server instance must use the same edition of SQL Server as your site database.  

4. After you restore the database copy, run **Setup** from the CD.Latest folder that contains the source files from the version you are updating to. When you run Setup, use the **/TESTDBUPGRADE** command-line option. If the SQL Server instance that hosts the database copy is not the default instance, provide the command-line arguments to identify the instance that hosts the site database copy.   

   For example, you have a site database with the database name *SMS_ABC*. You restore a copy of this site database to a supported instance of SQL Server with the instance name *DBTest*. To test an upgrade of this copy of the site database, use the following command line: **Setup.exe /TESTDBUPGRADE DBtest\CM_ABC**.  

   You can find Setup.exe in the following location on the source media for System Center Configuration Manager: **SMSSETUP\BIN\X64**.  

5. On the instance of SQL Server where you run the upgrade test, monitor the *ConfigMgrSetup.log* in the root of the system drive for progress and success.  

    If the test upgrade fails, fix any issues related to the site database upgrade failure. Then, create a new backup of the site database and  test the upgrade of the new copy of the database.  



## Next steps
After the test database update completes successfully, discard the updated database. It cannot be used by a Configuration Manager site. You can then return to your active site and [begin the update installation](/sccm/core/servers/manage/install-in-console-updates).
