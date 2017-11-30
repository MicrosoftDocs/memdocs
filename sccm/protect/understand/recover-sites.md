---
title: "Site recovery"
titleSuffix: "Configuration Manager"
description: "Learn to recover your sites in System Center Configuration Manager."
ms.custom: na
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid:  19539f4d-1667-4b4c-99a1-9995f12cf5f7
caps.latest.revision:
author: mstewart
ms.author: mstewart
manager: angrobe
---

#  Recover a Configuration Manager site

*Applies to: System Center Configuration Manager (Current Branch)*

Run a Configuration Manager site recovery after a Configuration Manager site fails or data loss occurs in the site database. Repairing and resynchronizing data are the core tasks of a site recovery and are required to prevent interruption of operations.

The sections in this topic can help you recover a Configuration Manager site. To create a backup, see [Backup for Configuration Manager](/sccm/protect/understand/backup-and-recovery).

## Considerations before recovering a site
> [!Important]  
> This information applies only to site recovery scenarios.  When you are upgrading your on-premises infrastructure and not actively recovering a failed site, review the information in the following topics:
> - [Upgrade on-premises infrastructure](/sccm/core/servers/manage/upgrade-on-premises-infrastructure)
> -	[Modify your infrastructure](/sccm/core/servers/manage/modify-your-infrastructure)


**You must use the same version and edition of SQL Server:** For example, restoring a database that ran on SQL Server 2014 to SQL Server 2016 is not supported. Similarly, restoring a site database that ran on a Standard edition of SQL Server 2016 to an Enterprise edition of SQL Server 2016 is not supported.
- 	SQL Server must not be set to **single-user mode**.
- 	Ensure the .MDF and .LDF files are valid. When you recover a site, there is no check for the state of the files you are restoring.

**If you use a SQL Server Always On availability group to host the site database:** Modify your recovery plans as described in [Prepare to use SQL Server Always On](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#changes-for-site-recovery).

**When you use database replicas:** After you restore a site database that was configured for database replicas, before you can use the database replicas you must reconfigure each database replica, recreating both the publications and subscriptions.

## Determine your recovery options
There are two main areas to consider for Configuration Manager primary site server and central administration site recovery; the **site server** and the **site database**.
The following sections can help you select the best options for your recovery scenario.

> [!NOTE]   
> When Setup detects an existing Configuration Manager site on the server, you can start a site recovery, but the recovery options for the site server are limited. For example, if you run Setup on an existing site server, when you choose recovery, you can recover the site database server, but the option to recover the site server is disabled.

### Site server recovery options
Start Setup from a copy of the **CD.Latest** folder that you created outside of the Configuration Manager installation folder.
-   If you run Configuration Manager Setup from the **Start** menu on the site server, the **Recover a site** option is not available.
-   If you installed any updates from within the Configuration Manager console before you made your backup, you cannot successfully reinstall the site by using Setup from installation media or the Configuration Manager installation path.

Then select the **Recover a site** option. You have the following recovery options for the failed site server:

-   **Recover the site server using an existing backup:** Use this option when you have a backup of the Configuration Manager site server that was created on the site server as part of the **Backup Site Server** maintenance task before the site failure. The site is reinstalled, and the site settings are configured, based on the site that was backed up.
-   **Reinstall the site server:** Use this option when you do not have a backup of the site server. The site server is reinstalled, and you must specify the site settings, just as you would during an initial installation.
  -   You must use the same site code and site database name that you used when the failed site was first installed.
  -   You can reinstall the site on a new computer that runs a new operating system.
  -   The computer must use the same name, FQDN, of the original site server.   

### Site database recovery options
When you run Setup, you have the following recovery options for the site database:
- 	**Recover the site database using a backup set:** Use this option when you have a backup of the Configuration Manager site database that was created as part of the **Backup Site Server** maintenance task run on the site before the site database failure. When you have a hierarchy, the changes that were made to the site database after the last site database backup are retrieved from the central administration site for a primary site, or from a reference primary site for a central administration site. When you recover the site database for a stand-alone primary site, you lose site changes after the last backup.

   When you recover the site database for a site in a hierarchy, the recovery behavior is different for a central administration site and primary site, and when the last backup is inside or outside of the SQL Server change tracking retention period. For more information, see the [Site database recovery scenarios](##site-database-recovery-scenarios) section in this topic.
  > [!NOTE]   
  > The recovery fails if you select to restore the site database by using a backup set, but the site database already exists.  

-   **Create a new database for this site:** Use this option when you do not have a backup of the Configuration Manager site database. When you have a hierarchy, a new site database is created, and the data is recovered by using replicated data from the central administration site for a primary site, or a reference primary site for a central administration site. This option is not available when you are recovering a stand-alone primary site or a central administration site that does not have primary sites.

-   **Use a site database that has been manually recovered:** Use this option when you have already recovered the Configuration Manager site database but must complete the recovery process.
    -   Configuration Manager can recover the site database from the Configuration Manager backup maintenance task or from a site database backup that you perform by using DPM or another process. After you restore the site database by using a method outside Configuration Manager, you must run Setup and select this option to complete the site database recovery.

    > [!NOTE]   
    > When you use DPM to back up your site database, use the DPM procedures to restore the site database to a specified location before you continue the restore process in Configuration Manager. For more information about DPM, see the [Data Protection Manager Documentation Library]() on TechNet.    

    -   When you have a hierarchy, the changes that were made to the site database after the last site database backup are retrieved from the central administration site for a primary site, or from a reference primary site for a central administration site. When you recover the site database for a stand-alone primary site, you lose site changes after the last backup.     


-   **Skip database recovery:** Use this option when no data loss has occurred on the Configuration Manager site database server. This option is only valid when the site database is on a different computer than the site server that you are recovering.

### SQL Server change tracking retention period
Change tracking is enabled for the site database in SQL Server. Change tracking lets Configuration Manager query for information about the changes that have been made to database tables after a previous point in time. The retention period specifies how long change tracking information is retained. By default, the site database is configured to have a retention period of 5 days. When you recover a site database, the recovery process proceeds differently if your backup is inside or outside the retention period. For example, if your site database server fails, and your last backup is 7 days old, it is outside the retention period.

For more information about SQL Server change tracking internals, see the following blogs from the SQL Server team: [Change Tracking Cleanup - part 1](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-1/) and [Change Tracking Cleanup - part 2](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-2).

### Reinitialization of site or global data
The process to reinitialize site or global data replaces existing data in the site database with data from another site database. For example, when site ABC reinitializes data from site XYZ, the following steps occur:
- 	The data is copied from site XYZ to site ABC.
- 	The existing data for site XYZ is removed from the site database on site ABC.
- 	The copied data from site XYZ is inserted into the site database for site ABC.

#### Example scenario 1
**The primary site reinitializes the global data from the central administration site:** The recovery process removes the existing global data for the primary site in the primary site database and replaces the data with the global data copied from the central administration site.

#### Example scenario 2
**The central administration site reinitializes the site data from a primary site:** The recovery process removes the existing site data for that primary site in the central administration site database and replaces the data with the site data copied from the primary site. The site data for other primary sites is not affected.

### Site database recovery scenarios
After a site database is restored from a backup, the Configuration Manager attempts to restore the changes in site and global data after the last database backup. The following describe the actions that Configuration Manager starts after a site database is restored from backup.

**Recovered site is a central administration site:**
-   **Database backup within change tracking retention period**
    -   **Global data:** The changes in global data after the backup are replicated from all primary sites.
    -   **Site data:** The changes in site data after the backup are replicated from all primary sites.


-   **Database backup older than change tracking retention period**
    -   **Global data:** The central administration site reinitializes the global data from the reference primary site if you specify it. Then all other primary sites reinitialize the global data from the central administration site. If no reference site is specified, all primary sites reinitialize the global data from the central administration site (the data that was restored from backup).
    -   **Site data:** The central administration site reinitializes the site data from each primary site.


**Recovered site is a primary site:**
-   **Database backup within change tracking retention period**
    -   **Global data:** The changes in global data after the backup are replicated from the central administration site.
    -   **Site data:** The central administration site reinitializes the site data from the primary site. Changes after the backup are lost, but most data are regenerated by clients that send information to the primary site.


-   **Database backup older than change tracking retention period**
    -   **Global data:** The primary site reinitializes the global data from the central administration site.
    -   **Site data:** The central administration site reinitializes the site data from the primary site. Changes after the backup are lost, but most data are regenerated by clients that send information to the primary site.

## Site recovery procedures
Use one of the following procedures to help you recover your site server and site database.

### To start a site recovery in the Setup Wizard
1.	Copy the [CD.Latest folder](/sccm/core/servers/manage/the-cd.latest-folder) to a location outside the Configuration Manager Installation folder.
From the copy of the CD.Latest folder, run the Configuration Manager Setup Wizard.

2.	On the **Getting Started** page, select **Recover a site**, and then click **Next**.

3.	Complete the wizard by using the options that are appropriate for your site recovery.

  -   During the recovery, Setup identifies the SQL Server Service Broker (SSB) port used by the SQL Server. Do not change this port setting during recovery or data replication will not work properly after the recovery completes.

  -   You can specify the original, or a new path to use for the Configuration Manager installation in the Setup Wizard.

### To start an unattended site recovery
  1.	Prepare the unattended installation script for the options that you require for the site recovery.  See [Unattended site recovery script file keys](/sccm/protect/understand/unattended-site-recovery-script-file-keys).

  2.	Run Configuration Manager Setup by using the command **/script** option. For example, if you named your setup initialization file ConfigMgrUnattend.ini and saved it in the C:\Temp directory of the computer on which you are running Setup, the command would be as follows: **Setup /script C:\temp\ConfigMgrUnattend.ini**.

  > [!NOTE]   
  >  After you recover a central administration site, replication of some site data from child sites can fail to be established. This can include hardware inventory, software inventory, and status messages.
  >
  >  If this occurs, you must reinitialize the **ConfigMgrDRSSiteQueue** for database replication.  To do so, use **SQL Server Manager** to run the following query on the Configuration Manager site database on the central administration site:
  >
  >  **IF EXISTS (SELECT \* FROM sys.service_queues WHERE name = 'ConfigMgrDRSSiteQueue' AND is_receive_enabled = 0)**
  >
  >  **ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON**


## Post-recovery tasks
After you recover your site, there are several post-recovery tasks that you must consider before your site recovery is completed. Use the following sections to help you complete your site recovery process.

### Re-enter user account passwords
After a site server recovery, passwords for the user accounts specified for the site must be re-entered because they are reset during the site recovery. The accounts are listed on the **Finished** page of the Setup Wizard after site recovery is completed and saved to C:\ConfigMgrPostRecoveryActions.html on the recovered site server.

#### To re-enter user account passwords after site recovery

1.  Open the Configuration Manager console and connect to the recovered site.

2.  In the Configuration Manager console, click **Administration**.

3.  In the **Administration** workspace, expand **Security**, and then click **Accounts**.

4.  For each account in which you re-enter the password, do the following:

    1.  Select the account from the list of accounts that were identified after site recovery. You can find this list in C:\ConfigMgrPostRecoveryActions.html on the recovered site server.

    2.  On the **Home** tab, in the **Properties** group, click **Properties** to open the account properties.

    3.  On the **General** tab, click **Set**, and then re-enter the passwords for the account.

    4.  Click **Verify**, select the appropriate data source for the selected user account, and then click **Test connection** to verify that the user account can connect to the data source.

    5.  Click **OK** to save the password changes, and then click **OK**.

### Re-enter sideloading keys
After a site server recovery, you must re-enter Windows sideloading keys specified for the site because they are reset during site recovery. After you re-enter the sideloading keys, the count in the **Activations used** column for Windows sideloading keys is reset in the Configuration Manager console. For example, let's say before the site failure you have a **Total activations** count set to **100** and **Activations used** is at **90** for the number of the keys that have been used by devices. After the site recovery, the **Total activations** column still displays **100**, but the **Activations used** column incorrectly displays **0**. However, after 10 new devices use a sideloading key, there will be no remaining sideloading keys, and the next device will fail to apply a sideloading key.

### Recreate the Microsoft Intune subscription
 If you recover a Configuration Manager site server after the site server computer is re-imaged, the Microsoft Intune subscription is not restored. You must reconnect your subscription after you recover the site.  Do not create a new APN-request, but instead upload the current valid .pem-file that was uploaded the last time iOS management was configured or renewed. For more information, see [Configuring the Microsoft Intune subscription](/sccm/mdm/deploy-use/configure-intune-subscription).

### Configure SSL for site system roles that use IIS
When you recover site systems that run IIS and that were configured for HTTPS before the failure, you must reconfigure IIS to use the web server certificate.

### Reinstall hotfixes in the recovered site server
After a site recovery, you must reinstall any hotfixes that were applied to the site server. View the list of the previously installed hotfixes on the **Finished** page of the Setup Wizard after site recovery. This list is also saved to **C:\ConfigMgrPostRecoveryActions.html** on the recovered site server.

### Recover custom reports on the computer running Reporting Services
When you have created custom Reporting Services reports, and Reporting Services fails, you can recover the reports when you have backed up the report server. For more information about restoring your custom reports in Reporting Services, see [Backup and Restore Operations for a Reporting Services Installation](http://go.microsoft.com/fwlink/p/?LinkId=228724) in the SQL Server 2008 Books Online.

### Recover content files
 The site database contains information about where the content files are stored on the site server, but the content files are not backed up or restored as part of the backup and recovery process. To fully recover content files, you must restore the content library and package source files to the original location. There are several methods for recovering your content files, but the easiest method is to restore the files from a file system backup of the site server.

 If you do not have a file system backup for the package source files, you must manually copy or download them as you did originally when you first created the package. You can run the following query in SQL Server to find the package source location for all packages and applications: `SELECT * FROM v_Package`. You can identify the package source site by looking at the first three characters of the package ID. For example, if the package ID is CEN00001, the site code for the source site is CEN. When you restore the package source files, they must be restored to the same location in which they were before the failure.

 If you do not have a file system backup that contains the content library, you have the following restore options:

-   **Import a prestaged content file**: When you have a Configuration Manager hierarchy, you can create a prestaged content file with all packages and applications from another location, and then import the prestaged content file to recover the content library on the site server.

-   **Update content**: When you start the update content action for a package or application deployment type, the content is copied from the package source to the content library. The package source files must be available in the original location for this action to finish successfully. You must perform this action on each package and application.

### Recover custom software updates on the computer running Updates Publisher
When you have included Updates Publisher database files in your backup plan, you can recover the databases in case of a failure on the computer on which Updates Publisher runs. For more information about Updates Publisher, see [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkId=228726) in the System Center TechCenter Library.

Use the following procedure to restore the Updates Publisher database.

#### To restore the Updates Publisher 2011 database
1.  Reinstall Updates Publisher on the recovered computer.

2.  Copy the database file (Scupdb.sdf) from your backup destination to %*USERPROFILE*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\ on the computer that runs Updates Publisher.

3.  When more than one user runs Updates Publisher on the computer, you must copy each database file to the appropriate user profile location.

### User State Migration data
As part of the state migration point site system properties, you specify the folders that store user state migration data. After you recover a server with a folder that stores user state migration data, you must manually restore the user state migration data on the server to the same folders that stored the data prior to the failure.

### Regenerate the certificates for distribution points
After you restore a site, the distmgr.log might contain the following entry for one or more distribution points: **Failed to decrypt cert PFX data**. This entry indicates that the distribution point certificate data cannot be decrypted by the site. To resolve this, you must regenerate or re-import the certificate for affected distribution points. This can be done by using the [Set-CMDistributionPoint](https://technet.microsoft.com/library/jj821872\(v=sc.20\).aspx) PowerShell cmdlet.

### Update Certificates Used for Cloud-Based distribution points
 Configuration Manager requires a management certificate that it uses for site server to cloud-based distribution point communication. After a site recovery, you must update the certificates for cloud-based distribution points.

## Recover a secondary site
 Configuration Manager does not support the backup of the database at a secondary site, but does support recovery by reinstalling the secondary site. Secondary site recovery is required when a Configuration Manager secondary site fails.

### Requirements for reinstalling a secondary site
-   The computer must meet all secondary site prerequisites and have appropriate security rights configured.
-   You must use the same installation path that was used for the failed site.
-   You must use a computer with the same configuration as the failed computer, such as its FQDN, to successfully recover the secondary site.
-   The computer must have the same SQL Server configuration as the failed site.
  -   During a secondary site recovery, Configuration Manager does not install SQL Server Express if it is not already installed on the computer.
  -   You must use the same version of SQL Server and the same instance of SQL Server that you used for the secondary site database before the failure.

### To recover a secondary site:
To recover a secondary site, use the **Recover Secondary Site** action from the **Sites** node in the Configuration Manager console. Unlike recovery for a central administration site or primary site, recovery for a secondary site does not use a backup file and instead reinstalls the secondary site files on the failed secondary site computer. After the site reinstalls, the secondary site data is reinitialized with data from the parent primary site.

During the recovery process, Configuration Manager verifies if the content library exists on the secondary site computer and that the appropriate content is available. The secondary site will use the existing content library, if it contains the appropriate content. Otherwise, to recover the content library of a recovered secondary site requires you to redistribute or prestage the content to that recovered site.

When you have a distribution point that is not on the secondary site, you are not required to reinstall the distribution point during a recovery of the secondary site. After the secondary site recovery, the site automatically synchronizes with the distribution point.

You can verify the status of the secondary site recovery, by using the **Show Install Status** action from the **Sites** node in the Configuration Manager console.
