---
title: Upgrade to current branch
titleSuffix: Configuration Manager
description: Learn the steps for running a successful in-place upgrade from a site and hierarchy that runs System Center 2012 Configuration Manager.
ms.date: 04/11/2022
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# Upgrade to Configuration Manager current branch

*Applies to: Configuration Manager (current branch)*

> [!IMPORTANT]
> Starting in April 2022, this feature of Configuration Manager is [deprecated](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).<!-- 13846745 --> The baseline media for version 2203 is the last version of Configuration Manager current branch that will support upgrade from any version of System Center 2012 Configuration Manager. Current branch version 2303 media will only support new installs of current branch.

Do an in-place upgrade to Configuration Manager current branch from a site and hierarchy that runs System Center 2012 Configuration Manager. Before upgrading from System Center 2012 Configuration Manager, you must prepare the sites. This preparation requires you to remove specific configurations that can prevent a successful upgrade. Then follow the upgrade sequence when more than a single site is involved.

> [!TIP]
> When managing Configuration Manager site and hierarchy infrastructure, the terms *upgrade*, *update*, and *install* are used to describe three separate concepts. To learn how each term is used, see [About upgrade, update, and install](../../../understand/upgrade-update-install.md).

## In-place upgrade paths

The following options are the currently supported in-place upgrade paths:

### Upgrade to the latest current branch version

You can upgrade the following products to a *fully licensed*, baseline version of Configuration Manager:

- System Center 2012 Configuration Manager with Service Pack 2
- System Center 2012 R2 Configuration Manager with Service Pack 1

For more information, see [Frequently asked questions for Configuration Manager branches and licensing](../../../understand/product-and-licensing-faq.yml).

> [!TIP]
> When you upgrade from a System Center 2012 Configuration Manager version to current branch, you might be able to streamline your upgrade process. For more information, see the following:
>
> - [Baseline and update versions](../../manage/updates.md#bkmk_Baselines)
> - [The CD.Latest folder](../../manage/the-cd.latest-folder.md)

If you previously installed Configuration Manager _Evaluation_ version, you can use the upgrade process to convert the site to the full version. For more information, see [Upgrade an evaluation installation of Configuration Manager to a full installation](upgrade-an-evaluation-install-to-a-full-install.md).
### Unsupported paths

The following paths aren't supported:

- It's not supported to upgrade a technical preview branch to a fully licensed installation. A technical preview version can only upgrade to a later version of the technical preview.

- Migration from a technical preview to a fully licensed version isn't supported.

## Upgrade checklists

The following checklists can help you plan a successful upgrade to Configuration Manager.

### Before you upgrade

Review these steps before you upgrade to Configuration Manager.

#### Review your System Center 2012 Configuration Manager environment

Resolve issues as detailed in the following Microsoft Support article: [Configuration Manager clients reinstall every five hours because of a recurring retry task and may cause an inadvertent client upgrade](/troubleshoot/mem/configmgr/configmgr-clients-reinstall-every-five-hours).

#### Make sure your environment meets the supported configurations

- Review the server OS version in use to host site system roles:

  - Some older operating systems supported by System Center 2012 Configuration Manager aren't supported by Configuration Manager current branch. Before the upgrade, remove site system roles on those OS versions. For more information, see [Supported operating systems for site system servers](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md).

  - The prerequisite checker for Configuration Manager doesn't verify the prerequisites for site system roles on the site server or on remote site systems. For example, you need to manually verify that remote site systems have at least .NET version 4.6.2.<!-- 13846610 --> For more information, see [List of prerequisite checks for Configuration Manager](list-of-prerequisite-checks.md).

- Review required prerequisites for each computer that hosts a site system role. For example, to deploy an OS, Configuration Manager uses the Windows Assessment and Deployment Kit (ADK). Before you run Setup, download and install the Windows ADK on the site server and on each computer that runs an instance of the SMS Provider.

For more information about supported platforms and prerequisite configurations, see [Supported configurations](../../../plan-design/configs/supported-configurations.md).

For more information about using the Windows ADK with Configuration Manager, see [Infrastructure requirements for OS deployment](../../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md).

#### Review the site and hierarchy status and verify that there are no unresolved issues

Before you upgrade a site, resolve all operational issues for the following components:

- Site server
- Site database server
- Site system roles on remote computers

A site upgrade can fail because of existing operational problems.

#### Install all applicable critical updates for operating systems on computers that host the site, the site database server, and remote site system roles

Before you upgrade a site, install any critical software updates for each applicable site system. If an update that you install requires a restart, restart the applicable computers before you start the upgrade.

#### Uninstall the site system roles not supported by Configuration Manager

The following site system roles are no longer used in Configuration Manager. Uninstall them before you upgrade from System Center 2012 Configuration Manager:

- Out of Band Management point

- System Health Validator point

- Application catalog website point and web service point

#### Disable database replicas for management points at primary sites

Configuration Manager can't upgrade a primary site that has a database replica for management points. Disable database replication before you:

- Create a backup of the site database to test the database upgrade

- Upgrade the production site to Configuration Manager current branch

For more information, see the following articles:

- System Center 2012 Configuration Manager: [Configure database replicas for management points](../configure/database-replicas-for-management-points.md#BKMK_DBReplica_Config)

- Configuration Manager, current branch: [Database replicas for management points](../configure/database-replicas-for-management-points.md)

#### Reconfigure software update points that use NLB

Configuration Manager can't upgrade a site that uses a Network Load Balancing (NLB) cluster to host software update points.

If you use NLB clusters for software update points, use PowerShell to remove the NLB cluster. (Beginning with System Center 2012 Configuration Manager SP1, there was no option in the Configuration Manager console to configure an NLB cluster.)

#### Disable all site maintenance tasks at each site during its upgrade

Before you upgrade to Configuration Manager, disable any site maintenance tasks that might run during the time the upgrade process is active. This list includes but isn't limited to the following tasks:

- Backup Site Server
- Delete Aged Client Operations
- Delete Aged Discovery Data

If a site database maintenance task runs during the upgrade process, the site upgrade can fail.

Before you disable a task, record the schedule of the task so you can restore its configuration after the site upgrade completes.

For more information about site maintenance tasks, see the following articles:

- System Center 2012 Configuration Manager: [Planning for site operations](../../../plan-design/hierarchy/plan-for-the-site-database.md)

- Configuration Manager, current branch: [Reference for maintenance tasks](../../manage/reference-for-maintenance-tasks.md)

#### Run setup prerequisite checker

Before you upgrade a site, run the **Prerequisite Checker** independently from setup to validate that your site meets the prerequisites. Later, when you upgrade the site, prerequisite checker runs again.

The independent prerequisite check evaluates the site for upgrade to both the current branch and the long-term servicing branch (LTSB) of Configuration Manager. Because some features aren't supported by the LTSB, you might see entries in the **ConfigMgrPrereq.log** that are like the following examples:

- `INFO: The site is a LTSB edition.`
- `Unsupported site system role 'Asset Intelligence synchronization point' for the LTSB edition;    Error;    Configuration Manager has detected that the 'Asset Intelligence synchronization point' is installed. Asset Intelligence is not supported on the LTSB edition. You must uninstall the Asset Intelligence synchronization point site system role before you can continue.`

If you plan to upgrade to the current branch, errors for the LTSB edition can be safely ignored. They only apply if you plan to upgrade to the LTSB.

Later, when you run Configuration Manager setup to do the upgrade, the prerequisite check runs again. It evaluates your site based on the branch of Configuration Manager you choose to install (current branch, or LTSB). If you choose to upgrade to the current branch, it doesn't run the check for features that aren't supported by the LTSB.

For more information, see the [Prerequisite checker](prerequisite-checker.md) and [List of prerequisite checks](list-of-prerequisite-checks.md).

#### Download prerequisite files and redistributable files for Configuration Manager

Use **Setup Downloader** to download prerequisite redistributable files, language packs, and the latest product updates for Configuration Manager.

For information, see [Setup Downloader](setup-downloader.md).

#### Plan to manage server and client languages

When you upgrade a site, the site upgrade installs only the language pack versions you select during the upgrade.

- Setup reviews the current language configuration of your site. It then identifies the language packs that are available in the folder where you store previously downloaded prerequisite files.

- You can affirm the selection of the current server and client language packs, or change the selections to add or remove support for languages.

- Only language packs that are available when you run Setup can be selected.

> [!NOTE]
> You can't use the language packs from System Center 2012 Configuration Manager to enable languages for a Configuration Manager current branch site.

For more information about language packs, see [Language packs](language-packs.md).

#### Review considerations for site upgrades

When you upgrade a site, some features and configurations reset to a default configuration. To help you prepare for these and related changes, see [Considerations for upgrading](#considerations-for-upgrading).

#### Create a backup of the site database at the central administration site (CAS) and primary sites

Before you upgrade a site, back up the site database to make sure that you have a successful backup to use for disaster recovery.

For more information, see [Backup and recovery](../../manage/backup-and-recovery.md).

#### Back up a customized configuration.mof file

If you use a customized configuration.mof file to define data classes you use with hardware inventory, create a backup of this file. After the upgrade, restore this file to your site. For more information, see [How to extend hardware inventory](../../../clients/manage/inventory/extend-hardware-inventory.md).

#### Test the database upgrade process on a copy of the most recent site database backup

Before you upgrade a Configuration Manager CAS or primary site, test the site database upgrade process on a copy of the site database.

- Test the site database upgrade process. When you upgrade a site, the site database might be modified.

- Although testing the database upgrade isn't required, it can identify problems for the upgrade before your production database is affected.

- A failed site database upgrade can render your site database inoperable and might require a site recovery to restore functionality.

- Although the site database is shared between sites in a hierarchy, plan to test the database at each applicable site before you upgrade that site.

- If you use database replicas for management points at a primary site, disable replication before you create the backup of the site database.

Configuration Manager doesn't support the backup of secondary sites, or the test upgrade of a secondary site database.

It's not supported to run a test database upgrade on the production site database. Doing so upgrades the site database and could render your site inoperable.

For more information, see [Test the site database upgrade](#test-the-site-database-upgrade).

#### Restart the site server and each computer that hosts a site system role

Do this action to make sure there are no pending actions from a recent installation of updates or from prerequisites.

#### Start the upgrade

Starting at the top-level site in the hierarchy, run Setup.exe from the Configuration Manager source media.

After the top-level site upgrades, you can begin the upgrade of each child site. Complete the upgrade of each site before you begin to upgrade the next site.

Until all sites in your hierarchy upgrade to Configuration Manager, your hierarchy operates in a mixed version mode.

For information about how to run upgrade, see [Upgrade sites](#upgrade-sites).

### After you upgrade

Review these steps after you upgrade to Configuration Manager.

#### Upgrade stand-alone Configuration Manager consoles

By default, when you upgrade a CAS or primary site, the installation also upgrades the Configuration Manager console that's installed on the site server. Manually upgrade each console that's installed on a computer other than the site server.

> [!TIP]
> Close each open console before you start the upgrade.

For more information, see [Install Configuration Manager consoles](install-consoles.md).

#### Reconfigure database replicas for management points at primary sites

If you use database replicas for management points at primary sites, uninstall the database replicas before you upgrade the site. After you upgrade a primary site, reconfigure the database replica for management points.

For more information, see [Database replicas for management points](../configure/database-replicas-for-management-points.md).

#### Reconfigure any database maintenance tasks you disabled before the upgrade

If you disabled database [maintenance tasks](../../manage/reference-for-maintenance-tasks.md) at a site before the upgrade, reconfigure those tasks at the site using the same settings that were in place before the upgrade.

#### Upgrade clients

After all your sites upgrade to Configuration Manager, plan to upgrade clients.

When you upgrade a client, the current client software is uninstalled and the new client software version is installed. To upgrade clients, you can use any method that Configuration Manager supports.

> [!TIP]
> When you upgrade the top-level site of a hierarchy, the client installation package on each distribution point in the hierarchy is also updated. When you upgrade a primary site, the client upgrade package that's available from that primary site is updated.

For more information, see [How to upgrade clients for Windows computers](../../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md).

## Considerations for upgrading

### Automatic actions

When you upgrade to Configuration Manager, the following actions occur automatically:

- A site reset. This action includes a reinstallation of all site system roles.

- If the site is the top-level site of a hierarchy, it updates the client installation package on each distribution point in the hierarchy. The site also updates the default boot images to use the new Windows PE version for the same version of the Windows ADK. However, the upgrade doesn't upgrade existing media for use with image deployment.

- If the site is a primary site, it updates the client upgrade package for that site.

### Manual actions after an upgrade

After you upgrade a site, make sure that you do the following actions:

- Make sure that clients assigned to each primary site upgrade and install the new client version.

- Upgrade each Configuration Manager console that connects to the site and that runs on a computer that's remote from the site server.

- At primary sites where you use database replicas for management points, reconfigure the database replicas.

- After the site upgrades, manually upgrade physical media like ISO files for CDs, DVDs, or USB flash drives. It also includes prestaged media provided to hardware vendors. The site upgrade updates the default boot images, it can't upgrade these media files or devices used external to Configuration Manager.

- Plan to update custom boot images when you don't require the older version of Windows PE.

### Actions that affect configurations and settings

When a site upgrades to Configuration Manager, some configurations and settings don't persist after the upgrade. Some configurations are set to a new default. The following list includes some settings that don't persist or that change:

- **Software Center**: The following Software Center items are reset to their default values:

  - **Work information** is reset to business hours from **5:00am** to **10:00pm** Monday to Friday.

  - The value for **Computer maintenance** is set to **Suspend Software Center activities when my computer is in presentation mode**.

  - The value for **Remote control** is set to the value in the client settings that are assigned to the computer.

- **Software update summarization schedules**: Custom summarization schedules for software updates or software update groups are reset to the default value of one hour. After the upgrade finishes, reset custom summarization values to the required frequency.

## Test the site database upgrade

This process only applies when you're upgrading a prior version like System Center 2012 Configuration Manager to Configuration Manager current branch.

Before you upgrade a site, test a copy of that site's database for the upgrade.

To test the database for an upgrade, you first restore a copy of the site database to an instance of SQL Server that doesn't host a Configuration Manager site. The version of SQL Server that you use to host the database copy must be a version of SQL Server that Configuration Manager supports.  

After you restore the site database, on the SQL Server computer, run Configuration Manager Setup from the source media folder for Configuration Manager.

For more information including specific steps, see [Test the database upgrade](../../manage/test-database-upgrade.md).

## Upgrade sites

If you've completed the following tasks, you're ready to upgrade your Configuration Manager site:

- Pre-upgrade configurations for your site
- Test the upgrade of the site database on a database copy
- Download prerequisite files and language packs for the version that you plan to install

When you upgrade a site in a hierarchy, you upgrade the top-level site of the hierarchy first. This top-level site is either a CAS or a stand-alone primary site. After you complete the upgrade of a CAS, you can upgrade child primary sites in any order you want. After you upgrade a primary site, you can upgrade that site's secondary sites, or upgrade other primary sites before you upgrade any secondary sites.

Before you upgrade a site, close the Configuration Manager console on the site server until the upgrade successfully completes. Also close all remote consoles that run on other computers. After the site upgrade completes successfully, you can reconnect the console. Until you upgrade a console to the new version, that console can't display some objects and information that are available in new version.

### Upgrade a CAS or primary site

1. Verify that the user who runs Setup has the following security rights:

    - Local **Administrator** rights on the site server

    - If the site database server is remote from the site server, local **Administrator** rights on it

1. On the site server, run the following program from the Configuration Manager source media: `.\SMSSETUP\BIN\X64\Setup.exe`. This action starts the Configuration Manager Setup wizard.

1. Read the information on the **Before You Begin** page, and then select **Next**.

1. On the **Getting Started** page, select **Upgrade this Configuration Manager site**, and then select **Next**.

1. On the **Product Key** page:

    If you previously installed Configuration Manager Evaluation version, you can select **Install the licensed edition of this product**. Then enter your product key for the full installation of Configuration Manager. This action converts the site to the full version. For more information, see [Upgrade an evaluation installation of Configuration Manager to a full installation](upgrade-an-evaluation-install-to-a-full-install.md).

    You can specify the **Software Assurance expiration date** of your licensing agreement. This date is a convenient reminder for you of that date. If you don't enter this value during setup, you can specify it later in the console.

    > [!NOTE]
    > Microsoft doesn't validate this expiration date, and doesn't use this date for license validation. It's a reminder to you of your expiration date. Configuration Manager periodically checks for new software updates offered online. To be eligible to install these updates, your license status should be current.

    For more information, see [Licensing and branches](../../../understand/learn-more-editions.md).

1. On the **Microsoft Software License Terms** page, read and accept the license terms, and then select **Next**.

1. On the **Prerequisite Licenses** page, read and accept the license terms for the prerequisite software, and then select **Next**. Setup downloads and automatically installs the software on site systems or clients when it's required. Before you can continue to the next page, agree to all terms.

1. On the **Prerequisite Downloads** page, specify whether Setup downloads the latest content from the internet or uses previously downloaded files. This content includes prerequisite redistributable files, language packs, and the latest product updates. If you already used Setup Downloader, select **Use previously downloaded files** and specify the download folder. For more information, see [Setup Downloader](setup-downloader.md).

    > [!NOTE]
    > When you use previously downloaded files, verify that the path to the download folder contains the most recent version of the files.

1. On the **Server Language Selection** page, view the list of languages that are currently installed for the site. Select other languages that are available at this site for the Configuration Manager console and for reports. You can also clear languages that you no longer want to support at this site. By default, English is selected and can't be removed.

    > [!IMPORTANT]
    > Each version of Configuration Manager can't use language packs from a prior version. To enable support for a language at a site that you upgrade, use the version of the language pack for the new version. For example, during upgrade from System Center 2012 Configuration Manager to Configuration Manager current branch, if the current branch version of a language pack isn't available with the prerequisite files you download, you can't install support for that language.

1. On the **Client Language Selection** page, view the list of languages that are currently installed for the site. Select other languages that are available at this site for client computers, or clear languages that you no longer want to support at this site. Specify whether to enable all client languages for mobile device clients, and then select **Next**. By default, English is selected and can't be removed.

1. On the **Settings Summary** page, review the configuration. When you're ready, select **Next** to start the Prerequisite Checker. This tool verifies server readiness for the upgrade of the site. For more information, see [Prerequisite Checker](prerequisite-checker.md).

1. On the **Prerequisite Installation Check** page, if there are no problems listed, select **Next** to upgrade the site and site system roles.

    If the Prerequisite Checker finds a problem, select the item on the list for details about how to resolve it. Resolve all items in the list that have an **Error** status before you continue Setup. For items with a **Warning** status, resolve as many as possible in your environment. After you resolve the issues, select **Run Check** to restart prerequisite checking. For more detailed information, open the **ConfigMgrPrereq.log** file in the root of the system drive. The log file can contain additional information that's not displayed in the user interface. For a list of installation prerequisite rules and descriptions, see [Prerequisite checks](list-of-prerequisite-checks.md).

On the **Upgrade** page, Setup displays the overall progress status. When Setup completes the core site server and site system installation, you can close the wizard. Site configuration continues in the background.

### Upgrade a secondary site

1. Verify that the administrative user that runs Setup has the following security rights:

    - Local **Administrator** rights on the secondary site server

    - **Infrastructure Administrator** or **Full Administrator** security role on the parent primary site

    - System administrator (**SA**) rights on the site database of the secondary site

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and then select the **Sites** node.

1. Select the secondary site that you want to upgrade. On the **Home** tab of the ribbon, in the **Site** group, select **Upgrade**.

1. Select **Yes** to confirm the decision, and to start the upgrade of the secondary site.

The secondary site upgrade runs in the background. After the upgrade is complete, confirm the status in the Configuration Manager console. Select the secondary site server, then on the **Home** tab of the ribbon, in the **Site** group, select **Show Install Status**.

## Post-upgrade tasks

After you upgrade a site, you might have to complete other tasks to finish the upgrade or reconfigure the site. These tasks can include the following items:

- Upgrade Configuration Manager clients
- Upgrade Configuration Manager consoles
- Re-enable database replicas for management points
- Restore settings for Configuration Manager functionality that you use and that doesn't persist after the upgrade

## Next steps

[Scenarios to streamline your installation of Configuration Manager current branch](scenarios-to-streamline-your-installation.md)
