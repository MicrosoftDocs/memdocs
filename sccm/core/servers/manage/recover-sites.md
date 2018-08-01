---
title: Site recovery
titleSuffix: Configuration Manager
description: Learn to recover your sites in Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 19539f4d-1667-4b4c-99a1-9995f12cf5f7
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

#  Recover a Configuration Manager site

*Applies to: System Center Configuration Manager (Current Branch)*

Run a Configuration Manager site recovery after a site fails or data loss occurs in the site database. Repairing and resynchronizing data are the core tasks of a site recovery and are required to prevent interruption of operations.

The sections in this article can help you recover a Configuration Manager site. To create a backup, see [Backup for Configuration Manager](/sccm/core/servers/manage/backup-and-recovery).



## Considerations before recovering a site

> [!Important]  
> This information applies only to site recovery scenarios. When you're upgrading your on-premises infrastructure and not actively recovering a failed site, review the information in the following articles:
> - [Upgrade on-premises infrastructure](/sccm/core/servers/manage/upgrade-on-premises-infrastructure)
> -	[Modify your infrastructure](/sccm/core/servers/manage/modify-your-infrastructure)


#### Use the same version and edition of SQL Server   
For example, restoring a database from SQL Server 2014 to SQL Server 2016 isn't supported. Similarly, restoring a SQL Server 2016 site database from Standard edition to Enterprise edition isn't supported.
- SQL Server can't be set to **single-user mode**.
- Make sure the MDF and LDF files are valid. When you recover a site, there's no check for the state of the files.  

#### SQL Server Always On availability groups   
If you use SQL Server Always On availability groups to host the site database, modify your recovery plans as described in [Prepare to use SQL Server Always On](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#changes-for-site-recovery).

#### Database replicas  
After you restore a site database that you configured for database replicas, reconfigure each replica. Before you can use the database replicas, recreate both the publications and subscriptions.



## Determine your recovery options

There are two main areas to consider for Configuration Manager primary site server and central administration site recovery: the **site server** and the **site database**.
The following sections can help you select the best options for your recovery scenario.

> [!NOTE]   
> When Configuration Manager setup detects an existing site on the server, you can start a site recovery, but the recovery options for the site server are limited. For example, if you run Setup on an existing site server, when you choose recovery, you can recover the site database server, but the option to recover the site server is disabled.


### Site server recovery options

Start Configuration Manager setup from a copy of the **CD.Latest** folder that you created outside of the Configuration Manager installation folder.  

-   If you run setup from the **Start** menu on the site server, the **Recover a site** option isn't available.  

-   If you installed any updates from within the Configuration Manager console before you made your backup, you can't reinstall the site by using setup from the following locations: 
    - Installation media
    - The Configuration Manager installation path 

Then select the **Recover a site** option. You have the following recovery options for the failed site server:  

#### Recover the site server using an existing backup
Use this option when you have a Configuration Manager backup of the site server from before the site failure. The site creates this backup as part of the **Backup Site Server** maintenance task. The site is reinstalled, and the site settings are configured based on the site that was backed up.  

#### Reinstall the site server
Use this option when you don't have a backup of the site server. The site server is reinstalled, and you must specify the site settings as you would during an initial installation.  

-   Use the same site code and site database name that you used when the failed site was first installed.  

-   You can reinstall the site on a new computer that runs a new OS version.  

-   The server must use the same hostname and fully qualified domain name (FQDN) of the original site server.   


### Site database recovery options

When you run Configuration Manager setup, you have the following recovery options for the site database:  

#### Recover the site database using a backup set
Use this option when you have a Configuration Manager backup of the site database from before the database failure. The site creates this backup as part of the **Backup Site Server** maintenance task. In a hierarchy, when restoring a primary site, the recovery process retrieves from the central administration site any changes made to the site database after the last backup. When restoring the central administration site, the recovery process retrieves these changes from a reference primary site. When you recover the site database for a standalone primary site, you lose site changes after the last backup.  

When you recover the site database for a site in a hierarchy, the recovery behavior is different for a central administration site and primary site. The behavior is also different when the last backup is inside or outside of the SQL Server change tracking retention period. For more information, see the [Site database recovery scenarios](#site-database-recovery-scenarios) section in this article.  

> [!NOTE]   
> If you select to restore the site database by using a backup set, but the site database already exists, the recovery fails.   

#### Create a new database for this site
Use this option when you don't have a backup of the site database. In a hierarchy, the recovery process creates a new site database. When restoring a child primary site, it recovers the data by replicating from the central administration site. When restoring the central administration site, it replicates data from a reference primary site. This option isn't available when you're recovering a standalone primary site or a central administration site that doesn't have primary sites.  

#### Use a site database that has been manually recovered
Use this option when you've already recovered the Configuration Manager site database, but need to complete the recovery process.  

- Configuration Manager can recover the site database from any of the following processes:  

    - The Configuration Manager backup maintenance task  
    - A site database backup using Data Protection Manager (DPM)  
    - Another backup process   

    After you restore the site database by using a method outside Configuration Manager, run Setup, and select this option to complete the site database recovery.  

    > [!NOTE]   
    > When you use DPM to back up your site database, use the DPM procedures to restore the site database to a specified location before you continue the restore process in Configuration Manager. For more information about DPM, see the [Data Protection Manager](https://docs.microsoft.com/system-center/dpm) documentation library.    

- In a hierarchy, when you recover a primary site database, the recovery process retrieves from the central administration site any changes made to the site database after the last backup. When restoring the central administration site, the recovery process retrieves these changes from a reference primary site. When you recover the site database for a standalone primary site, you lose site changes after the last backup.   

#### Skip database recovery
Use this option when no data loss has occurred on the Configuration Manager site database server. This option is only valid when the site database is on a different computer than the site server that you're recovering.  


### SQL Server change tracking retention period

Configuration Manager enables change tracking for the site database in SQL Server. Change tracking lets Configuration Manager query for information about the changes made to database tables after a previous point in time. The retention period specifies how long change tracking information is kept. By default, the site database is configured to have a retention period of five days. When you recover a site database, the recovery process proceeds differently if your backup is inside or outside the retention period. For example, if your SQL server fails, and your last backup is seven days old, it's outside the retention period.

For more information about SQL Server change tracking internals, see the following blog posts from the SQL Server team: [Change Tracking Cleanup - part 1](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-1/) and [Change Tracking Cleanup - part 2](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-2).


### Reinitialization of site or global data

The process to reinitialize site or global data replaces existing data in the site database with data from another site database. For example, when site ABC reinitializes data from site XYZ, the following steps occur:
- The data is copied from site XYZ to site ABC.
- The existing data for site XYZ is removed from the site database on site ABC.
- The copied data from site XYZ is inserted into the site database for site ABC.

#### Example scenario 1: The primary site reinitializes the global data from the central administration site  
The recovery process removes the existing global data for the primary site in the primary site database and replaces the data with the global data copied from the central administration site.

#### Example scenario 2: The central administration site reinitializes the site data from a primary site 
The recovery process removes the existing site data for that primary site in the central administration site database. It replaces the data with the site data copied from the primary site. The site data for other primary sites isn't affected.


### Site database recovery scenarios

After a site database is restored from a backup, Configuration Manager tries to restore the changes in site and global data after the last database backup. Configuration Manager starts the following actions after a site database is restored from backup:  

#### Recovered site is a central administration site
- Database backup within change tracking retention period  

     - **Global data**: The changes in global data after the backup are replicated from all primary sites.  

     - **Site data**: The changes in site data after the backup are replicated from all primary sites.  

- Database backup older than change tracking retention period  

     - **Global data**: The central administration site reinitializes the global data from the reference primary site if you specify it. Then all other primary sites reinitialize the global data from the central administration site. If you don't specify a reference site, all primary sites reinitialize the global data from the central administration site. This data is what you restored from backup.  

     - **Site data**: The central administration site reinitializes the site data from each primary site.  

#### Recovered site is a primary site
- Database backup within change tracking retention period  

     - **Global data**: The changes in global data after the backup are replicated from the central administration site.  

     - **Site data**: The central administration site reinitializes the site data from the primary site. Changes after the backup are lost. Clients regenerate most data when they send information to the primary site.  

- Database backup older than change tracking retention period  
     - **Global data**: The primary site reinitializes the global data from the central administration site.  

     - **Site data**: The central administration site reinitializes the site data from the primary site. Changes after the backup are lost. Clients regenerate most data when they send information to the primary site.  



## Site recovery procedures

Use one of the following procedures to help you recover your site server and site database:


### Start a site recovery in the setup wizard

1.	Copy the [CD.Latest folder](/sccm/core/servers/manage/the-cd.latest-folder) to a location outside the Configuration Manager installation folder. From the copy of the CD.Latest folder, run the Configuration Manager setup wizard.  

2.	On the **Getting Started** page, select **Recover a site**, and then click **Next**.  

3.	Complete the wizard by using the options that are appropriate for your site recovery.  

     - During the recovery, setup identifies the SQL Server Service Broker (SSB) port used by the SQL Server. Don't change this port setting during recovery or data replication won't work properly after the recovery completes.  

     - You can specify the original or a new path to use for the Configuration Manager installation in the setup wizard.  


### Start an unattended site recovery

1. Prepare the unattended installation script for the options that you require for the site recovery. For more information, see [Unattended site recovery](/sccm/core/servers/manage/unattended-recovery).  

2. Run Configuration Manager setup by using the `/script` command-line option. For example, you create a setup initialization file **ConfigMgrUnattend.ini**. You save it in the `C:\Temp` directory of the computer on which you're running setup. Use the following command:  

    `setup.exe /script C:\temp\ConfigMgrUnattend.ini`  


> [!NOTE]   
>  After you recover a central administration site, replication of some site data from child sites can fail to be established. This data can include hardware inventory, software inventory, and status messages.
>
>  If this issue occurs, reinitialize the **ConfigMgrDRSSiteQueue** for database replication. Use **SQL Server Manager** to run the following query against the site database for the central administration site:
>
> ``` SQL
> IF EXISTS (SELECT * FROM sys.service_queues WHERE name = 'ConfigMgrDRSSiteQueue' AND is_receive_enabled = 0)  
>  
> ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON
> ```



## Post-recovery tasks

After you recover your site, there are several post-recovery tasks to consider before your site recovery is complete. Use the following sections to help you complete your site recovery process.


### Reenter user account passwords

After a site server recovery, reenter the passwords for any user accounts in the site. These passwords are reset during the site recovery. The accounts are listed on the **Finished** page of the setup wizard after site recovery is completed. The list is also saved to `C:\ConfigMgrPostRecoveryActions.html` on the recovered site server.

#### Reenter user account passwords after site recovery
1. Open the Configuration Manager console and connect to the recovered site.  

2. Go to the **Administration** workspace, expand **Security**, and then click **Accounts**.  

3. For each account, do the following steps to reenter the password:  

     1. Select the account from the list identified after site recovery.  

     2. Click **Properties** in the ribbon.  

     3. On the **General** tab, click **Set**, and then reenter the password for the account.  

     4. Click **Verify**, select the appropriate data source for the selected user account, and then click **Test connection**. This step tests that the user account can connect to the data source, and verifies the credentials.  

     5. Click **OK** to save the password changes, and then click **OK** to close the account properties page.  


### Reenter sideloading keys

After a site server recovery, reenter Windows sideloading keys specified for the site. These keys are reset during site recovery. After you reenter the sideloading keys, the site resets the count in the **Activations used** column for Windows sideloading keys. 

For example, before the site failure the **Total activations** count shows as **100**. The number of keys that devices have used, or **Activations used**, is **90**. After the site recovery, the **Total activations** still displays **100**, but the **Activations used** column incorrectly displays **0**. After 10 new devices use a sideloading key, there are no more sideloading keys, and the 11th device fails to apply a sideloading key.


### Recreate the Microsoft Intune subscription

If you recover a Configuration Manager site server after the site server is reimaged, the Microsoft Intune subscription isn't restored. Reconnect your subscription after you recover the site. Don't create a new APN request. Instead upload the current valid PEM file. Use the same file that you uploaded the last time you configured or renewed iOS management. For more information, see [Configuring the Microsoft Intune subscription](/sccm/mdm/deploy-use/configure-intune-subscription).


### Configure SSL for site system roles that use IIS

When you recover site systems that run IIS and you configured for HTTPS, reconfigure IIS to use the web server certificate.


### Reinstall hotfixes 

After a site recovery, you must reinstall any hotfixes that were applied to the site server. After site recovery, view the list of the previously installed hotfixes on the **Finished** page of the setup wizard. This list is also saved to `C:\ConfigMgrPostRecoveryActions.html` on the recovered site server.


### Recover custom reports 

Some customers create custom reports in SQL Server Reporting Services. When this component fails, recover the reports from a backup of the report server. For more information about restoring your custom reports in Reporting Services, see [Backup and Restore Operations for Reporting Services](https://docs.microsoft.com/sql/reporting-services/install-windows/backup-and-restore-operations-for-reporting-services).


### Recover content files

The site database tracks where the site server stores the content files. The content files themselves aren't backed up or restored as part of the backup and recovery process. To fully recover content files, restore the content library and package source files to the original location. There are several methods for recovering your content files. The easiest method is to restore the files from a file system backup of the site server.

If you don't have a file system backup for the package source files, manually copy or download them. This process is similar to when you originally created the package. Run the following query in SQL Server to find the package source location for all packages and applications: `SELECT * FROM v_Package`. Identify the package source site by looking at the first three characters of the package ID. For example, if the package ID is CEN00001, the site code for the source site is CEN. When you restore the package source files, they must be restored to the same location in which they were before the failure.

If you don't have a file system backup that includes the content library, you have the following restore options:  

- **Import a prestaged content file**: In a Configuration Manager hierarchy, you can create a prestaged content file with all packages and applications from another location. Then import the prestaged content file to recover the content library on the site server.  

- **Update content**: Configuration Manager copies the content from the package source to the content library. For this action to finish successfully, the package source files must be available in the original location. Perform this action on each package and application.


### Recover custom software updates

When you've included System Center Updates Publisher database files in your backup plan, you can recover the databases if the Updates Publisher computer fails. For more information about Updates Publisher, see [System Center Updates Publisher](/sccm/sum/tools/updates-publisher).

#### Restore the Updates Publisher database
1. Reinstall Updates Publisher on the recovered computer.  

2. Copy the database file **Scupdb.sdf** from your backup destination to `%USERPROFILE%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\` on the computer that runs Updates Publisher.  

3. When more than one user runs Updates Publisher on the computer, copy each database file to the appropriate user profile location.  


### User State Migration data

As part of the state migration point properties, you specify the folders that store user state data. After you recover a state migration point, manually restore the user state data on the server. Restore it to the same folders that stored the data before the failure.


### Regenerate the certificates for distribution points

After you restore a site, the **distmgr.log** might list the following entry for one or more distribution points: `Failed to decrypt cert PFX data`. This entry indicates that the distribution point certificate data can't be decrypted by the site. To resolve this issue, regenerate or reimport the certificate for affected distribution points. Use the [Set-CMDistributionPoint](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmdistributionpoint) PowerShell cmdlet.


### Update certificates used for cloud-based distribution points

Configuration Manager requires an Azure management certificate for the site server to communicate with cloud-based distribution points. After a site recovery, update the certificates for cloud-based distribution points.



## Recover a secondary site

Configuration Manager doesn't support the backup of the database at a secondary site, but does support recovery by reinstalling the secondary site. Secondary site recovery is required when a Configuration Manager secondary site fails.


### Requirements

- The server must meet all secondary site prerequisites and have appropriate security rights configured.  

- Use the same installation path that was used for the failed site.  

- Use a server with the same configuration as the failed server. This configuration includes its fully qualified domain name (FQDN).  

- The server must have the same SQL Server configuration as the failed site.  

     - During a secondary site recovery, Configuration Manager doesn't install SQL Server Express if it's not already installed on the computer.  

     - Use the same version of SQL Server and the same instance of SQL Server that you used for the secondary site database before the failure.  


### Procedure

Use the **Recover Secondary Site** action from the **Sites** node in the Configuration Manager console. Unlike with other types of sites, recovery for a secondary site doesn't use a backup file. This process reinstalls the secondary site files on the failed server. After the site reinstalls, the secondary site data is reinitialized from the parent primary site.

During the recovery process, Configuration Manager verifies if the content library exists on the secondary site server. It also checks that the appropriate content is available. The secondary site uses the existing content library, if it includes the appropriate content. Otherwise, to recover the content library of a secondary site, redistribute or prestage the content to the server.

When you have a distribution point that isn't on the secondary site server, you aren't required to reinstall the distribution point during a recovery of the secondary site. After the secondary site recovery, the site automatically synchronizes with the distribution point.

You can verify the status of the secondary site recovery by using the **Show Install Status** action from the **Sites** node in the Configuration Manager console.
