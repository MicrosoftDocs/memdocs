---
title: "Backup and recovery | System Center Configuration Manager"
description: "Learn to back up and recover your sites in the event of failure or data loss in System Center Configuration Manager."
ms.custom: na
ms.date: 04/13/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7832d83-9ae2-4530-8a77-790e0845e12f
caps.latest.revision: 22
author: Brendunsms.author: brendunsmanager: angrobe

---
# Backup and recovery for System Center Configuration Manager
Prepare backup and recovery approaches to avoid data loss. For Configuration Manager sites a backup and recovery approach can help recover sites and hierarchies more quickly, and with the least data loss. The sections in this topic can help you back up your sites and recover a site in the event of failure or data loss.  

-   [Back up a Configuration Manager site](#BKMK_SiteBackup)  

    -   [Backup maintenance task](#BKMK_BackupMaintenanceTask)  

    -   [Using Data Protection Manager to back up your site database](#BKMK_DPMBackup)  

    -   [Archiving the backup snapshot](#BKMK_ArchivingBackupSnapshot)  

    -   [Using the AfterBackup.bat file](#BKMK_UsingAfterBackup)  

    -   [Supplemental backup tasks](#BKMK_SupplementalBackup)  

-   [Recover a Configuration Manager site](#BKMK_RecoverSite)  

    -   [Determine your recovery options](#BKMK_DetermineRecoveryOptions)  

        -   [Site server recovery options](#BKMK_SiteServerRecoveryOptions)  

        -   [Site database recovery options](#BKMK_SiteDatabaseRecoveryOption)  

        -   [SQL Server change tracking retention period](#bkmk_SQLretention)  

        -   [Process to reinitialize site or global data](#bkmk_reinit)  

        -   [Site database recovery scenarios](#BKMK_SiteDBRecoveryScenarios)  

    -   [Unattended site recovery script file keys](#BKMK_UnattendedSiteRecoveryKeys)  

    -   [Post-recovery tasks](#BKMK_PostRecovery)  

    -   [Recover a secondary site](#BKMK_RecoverSecondarySite)  

-   [SMS Writer service](#BKMK_SMSWriterService)  

> [!NOTE]  
>  If you use a SQL Server AlwaysOn availability group to host the site database, modify your backup and recovery plans as described in the [Changes for Backup and Recovery when you use a SQL Server AlwaysOn availability group](../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#bkmk_BnR) section of the [SQL Server AlwaysOn for a highly available site database for System Center Configuration Manager](../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md) topic.  

##  <a name="BKMK_SiteBackup"></a> Back up a Configuration Manager site  
 Configuration Manager has a backup maintenance task that:  

-   Runs on a schedule  

-   Backs up the site database  

-   Backs up specific registry keys  

-   Backs up specific folders and files  

-   Backs up the **CD.Latest** folder  (See [The CD.Latest folder for System Center Configuration Manager](../../core/servers/manage/the-cd.latest-folder.md))  

 Plan to run the default site backup task at a minimum of every 5 days. This is because Configuration Manager uses a [SQL Server change tracking retention period](#bkmk_SQLretention) period of 5 days.  

 To simplify the backup process, you can create an **AfterBackup.bat** file to perform post-backup actions automatically after the backup maintenance task runs successfully. The AfterBackup.bat file is usually used to archive the backup snapshot to a secure location. You can also use the AfterBackup.bat file to copy files to your backup folder and start other, supplemental backup tasks.

Use the following sections to help you create your Configuration Manager backup strategy.  

> [!NOTE]  
>  Configuration Manager can recover the site database from the Configuration Manager backup maintenance task or from a site database backup that you created with another process. For example, you can restore the site database from a backup that is created as part of a Microsoft SQL Server maintenance plan. You can restore the site database from a backup that is created by using System Center 2012 Data Protection Manager (DPM). For more information, see [Using Data Protection Manager to back up your site database](#BKMK_DPMBackup).  

###  <a name="BKMK_BackupMaintenanceTask"></a> Backup maintenance task  
 You can automate backup for Configuration Manager sites by scheduling the predefined Backup Site Server maintenance task. You can back up a central administration site and primary site, but there is no backup support for secondary sites or site system servers. When the Configuration Manager backup service runs, it follows the instructions defined in the backup control file (**<ConfigMgrInstallationFolder\>\Inboxes\Smsbkup.box\Smsbkup.ctl**). You can modify the backup control file to change the behavior of the backup service. Site backup status information is written to the **Smsbkup.log** file. This file is created in the destination folder that you specify in the Backup Site Server maintenance task properties.  


##### To enable the site backup maintenance task  

1.  In the Configuration Manager console, open **Administration** > **Site Configuration**  

     \> **Sites**.  

2.  Select the site in which you want to enable the site backup maintenance task.  

3.  On the **Home** tab, in the **Settings** group, choose **Site Maintenance Tasks**.  

4.  Choose **Backup Site Server**  >  **Edit**.  

5.  Choose **Enable this task** > **Set Paths** to specify the backup destination. You have the following options:  

    > [!IMPORTANT]  
    >  To help prevent tampering of the backup files, store the files in a secure location. The most secure backup path is to a local drive so you can set NTFS file system permissions on the folder. Configuration Manager does not encrypt the backup data that is stored in the backup path.  

    -   **Local drive on site server for site data and database**: Specifies that the backup files for the site and site database are stored in the specified path on the local disk drive of the site server. You must create the local folder before the backup task runs.   The Local System account on the site server must have **Write** NTFS file system permissions to the local folder for the site server backup. The Local System account on the computer that is running SQL Server must have **Write** NTFS permissions to the folder for the site database backup.  

    -   **Network path (UNC name) for site data and database**: Specifies that the backup files for the site and site database are stored in the specified UNC path. You must create the share before the backup task runs.The computer account of the site server and the computer account of the SQL Server, if SQL Server is installed on another computer, must have **Write** NTFS and share permissions to the shared network folder.  

    -   **Local drives on site server and SQL Server**: Specifies that the backup files for the site are stored in the specified path on the local drive of the site server, and the backup files for the site database are stored in the specified path on the local drive of the site database server. You must create the local folders before the backup task runs. The computer account of the site server must have **Write** NTFS permissions to the folder that you create on the site server. The computer account of the SQL Server must have **Write** NTFS permissions to the folder that you create on the site database server. This option is available only when the site database is not installed on the site server.  

    > [!NOTE]  
    >	 - The option to browse to the backup destination is only available when you specify the UNC path of the backup destination.

    >- The folder name or share name that is used for the backup destination does not support the use of Unicode characters.  


6.  Configure a schedule for the site backup task. As a best practice, consider a backup schedule that is outside active working hours. If you have a hierarchy, consider a schedule that runs at least two times a week to ensure maximum data retention in the event of site failure.  

    When you run the Configuration Manager console on the same site server that you are configuring for backup, the Backup Site Server maintenance task uses local time for the schedule. When the Configuration Manager console is run from a computer remote from the site that you are configuring for backup, the Backup Site Server maintenance task uses UTC for the schedule.  

7.  Choose whether to create an alert if the site backup task fails, click **OK**, and then click **OK**. When selected, Configuration Manager creates a critical alert for the backup failure that you can review in the **Alerts** node in the **Monitoring** workspace.  

 Next, verify that the Backup Site Server maintenance task is running, to ensure that backups are being created.  

##### To verify that the Backup Site Server maintenance task is running  

-   Verify that the Site Backup maintenance task is running by reviewing any of the following:  

    -   Check the timestamp on the files in the backup destination folder that the task created. Verify that the timestamp has been updated with a time that matches the time when the task was last scheduled to run.  

    -   In the **Component Status** node in the **Monitoring** workspace, review the status messages for SMS_SITE_BACKUP. When site backup is completed successfully, you see message ID 5035, which indicates that the site backup was completed without any errors.  

    -   When the Backup Site Server maintenance task is configured to create an alert if backup fails, you can check the **Alerts** node in the **Monitoring** workspace for backup failures.  

    -   In <*ConfigMgrInstallationFolder*>\Logs, review Smsbkup.log for warnings and errors. When site backup is completed successfully, you see `Backup completed` with a timestamp and message ID `STATMSG: ID=5035`.  

    > [!TIP]  
    >  When the backup maintenance task fails, you can restart the backup task by stopping and restarting the SMS_SITE_BACKUP service.  

###  <a name="BKMK_DPMBackup"></a> Using Data Protection Manager to back up your site database  
 You can use System Center 2012 Data Protection Manager (DPM) to back up your site database. You must create a new protection group in DPM for the site database computer. On the **Select Group Members** page of the Create New Protection Group Wizard, you select the SMS Writer service from the data source list, and then select the site database as an appropriate member. For more information about using DPM to back up your site database, see the [Data Protection Manager Documentation Library](http://go.microsoft.com/fwlink/?LinkId=272772) on TechNet.  

> [!IMPORTANT]  
>  Configuration Manager does not support DPM backup for a SQL Server cluster that uses a named instance, but does support DPM backup on a SQL Server cluster that uses the default instance of SQL Server.  

 After you restore the site database, follow the steps in Setup to recover the site. Select the **Use a site database that has been manually recovered** recovery option to use the site database that you recovered with Data Protection Manager.  

###  <a name="BKMK_ArchivingBackupSnapshot"></a> Archiving the backup snapshot  
 The first time the Backup Site Server maintenance task runs, it creates a backup snapshot, which you can use to recover your site server in case of a failure. When the backup task runs again during subsequent cycles, it creates a new backup snapshot that overwrites the previous snapshot. As a result, the site has only a single backup snapshot, and you have no way of retrieving an earlier backup snapshot.  

 As a best practice, keep multiple archives of the backup snapshot for the following reasons:  

-   It is common for backup media to fail, get misplaced, or contain only a partial backup. Recovering a failed stand-alone primary site from an older backup is better than recovering without any backup. For a site server in a hierarchy, the backup must be in the SQL Server change tracking retention period, or the backup is not required.  

-   A corruption in the site can go undetected for several backup cycles. You might have to use a backup snapshot from before the site became corrupted. This applies to a stand-alone primary site and to sites in a hierarchy where the backup is in the SQL Server change tracking retention period.  

-   The site might have no backup snapshot at all if, for example, the Backup Site Server maintenance task fails. Because the backup task removes the previous backup snapshot before it starts to back up the current data, there will not be a valid backup snapshot.  

###  <a name="BKMK_UsingAfterBackup"></a> Using the AfterBackup.bat file  
 After successfully backing up the site, the Backup Site Server task automatically attempts to run a file that is named AfterBackup.bat. You must manually create the AfterBackup.bat file in <*ConfigMgrInstallationFolder*>\Inboxes\Smsbkup. If an AfterBackup.bat file exists, and is stored in the correct folder, it automatically runs after the backup task is completed. The AfterBackup.bat file lets you archive the backup snapshot at the end of every backup operation, and automatically perform other post-backup tasks that are not part of the Backup Site Server maintenance task. The AfterBackup.bat file integrates the archive and the backup operations, thereby ensuring that every new backup snapshot is archived. When the AfterBackup.bat file is not present, the backup task skips it without effect on the backup operation. To verify that the site backup task successfully ran the AfterBackup.bat file, see the **Component Status** node in the **Monitoring** workspace and review the status messages for SMS_SITE_BACKUP. When the task successfully started the AfterBackup.bat command file, you see message ID 5040.  

> [!TIP]  
>  To create the AfterBackup.bat file to archive your site server backup files, you must use a copy command tool, such as Robocopy, in the batch file. For example, you could create the AfterBackup.bat file, and on the first line, you could add something similar to: `Robocopy E:\ConfigMgr_Backup \\ServerName\ShareName\ConfigMgr_Backup /MIR`. For more information about Robocopy, see the [Robocopy](http://go.microsoft.com/fwlink/p/?LinkId=228408) command-line reference webpage.  

 Although the intended use of the AfterBackup.bat is to archive backup snapshots, you can create an AfterBackup.bat file to perform additional tasks at the end of every backup operation.  

###  <a name="BKMK_SupplementalBackup"></a> Supplemental backup tasks  
 The Backup Site Server maintenance task provides a backup snapshot for the site server files and site database, but there are other items not backed up that you must consider when you create your backup strategy. Use the following sections to help you complete your Configuration Manager backup strategy.  

#### Back up custom Reporting Services reports  
 When you have modified predefined or created custom Reporting Services reports, creating a backup for the report server database files is an important part of your backup strategy. The report server backup must include a backup of the source files for reports and models, encryption keys, custom assemblies or extensions, configuration files, custom SQL Server views used in custom reports, custom stored procedures, and so on.  

> [!IMPORTANT]  
>  When Configuration Manager updates to a newer version, the predefined reports might be overwritten by new reports. If you modify a predefined report, back up the report, and then restore it in Reporting Services.  

 For more information about backing up your custom reports in Reporting Services, see [Backup and Restore Operations for a Reporting Services Installation](https://technet.microsoft.com/library/ms155814\(v=sql.120\).aspx) in the SQL Server 2014 Books Online.  

#### Backup content files  
 The content library in Configuration Manager is the location where all content files are stored for software updates, applications, operating system deployment, and so on. The content library is located on the site server and on each distribution point. The Backup Site Server maintenance task does not include a backup for the content library or the package source files. When a site server fails, the information about the content library files is restored to the site database, but you must restore the content library and package source files on the site server.  

-   **Content library**: The content library must be restored before you can redistribute content to distribution points. When you start content redistribution, Configuration Manager copies the files from the content library on the site server to the distribution points. The content library for the site server is in the SCCMContentLib folder, which is typically located on the drive with the most free disk space at the time when the site was installed.  

-   **Package source files**: The package source files must be restored before you can update content on distribution points. When you start a content update, Configuration Manager copies new or modified files from the package source to the content library, which in turn copies the files to associated distribution points. You can run the following query in SQL Server to find the package source location for all packages and applications: `SELECT * FROM v_Package`. You can identify the package source site by looking at the first three characters of the package ID. For example, if the package ID is CEN00001, the site code for the source site is CEN. When you restore the package source files, they must be restored to the same location where they were before the failure.  

 Verify that you include both the content library and package source locations in your file system backup for the site server.  

#### Back up custom software updates  
     System Center Updates Publisher 2011 is a stand-alone tool that lets you publish custom software updates to Windows Server Update Services (WSUS), synchronize the software updates to Configuration Manager, assess software updates compliance, and deploy the custom software updates to clients. Updates Publisher uses a local database for its software update repository. When you use Updates Publisher to manage custom software updates, determine whether you have to include the Updates Publisher database in your backup plan. For more information about Updates Publisher, see [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkId=228726) in the System Center TechCenter Library.  

 Use the following procedure to back up the Updates Publisher database.  

###### To back up the Updates Publisher 2011 database  

1.  On the computer that runs Updates Publisher, browse to the Updates Publisher database file (Scupdb.sdf) in %*USERPROFILE*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\\. There is a different database file for each user that runs Updates Publisher.  

2.  Copy the database file to your backup destination. For example, if your backup destination is E:\ConfigMgr_Backup, you could copy the Updates Publisher database file to E:\ConfigMgr_Backup\SCUP2011.  

    > [!TIP]  
    >  When there is more than one database file on a computer, consider storing the file in a subfolder that indicates the user profile associated with the database file. For example, you could have one database file in E:\ConfigMgr_Backup\SCUP2011\User1 and another database file in E:\ConfigMgr_Backup\SCUP2011\User2.  

### User state migration data  
 You can use Configuration Manager task sequences to capture and restore the user state data in operating system deployment scenarios where you want to retain the user state of the current operating system. The folders that store the user state data are listed in the properties for the state migration point. This user state migration data is not backed up as part of the Site Server Backup maintenance task. As part of your backup plan, you must manually back up the folders that you specify to store the user state migration data.   

##### To determine the folders used to store user state migration data  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, expand **Site Configuration**, and choose **Servers and Site System Roles**.  

3.  Select the site system that hosts the state migration role, and choose **State migration point** in **Site System Roles**.  

4.  On the **Site Role** tab, in the **Properties** group, click **Properties**.  

5.  The folders that store the user state migration data are listed in the **Folder details** section on the **General** tab.  

##  <a name="BKMK_RecoverSite"></a> Recover a Configuration Manager site  
 A Configuration Manager site recovery is required whenever a Configuration Manager site fails or data loss occurs in the site database. Repairing and resynchronizing data are the core tasks of a site recovery and are required to prevent interruption of operations.  

> [!IMPORTANT]  
>  When you recover the database for a site:  
>   
>  -   You must use the same version and edition of SQL Server. For example, restoring a database that ran on SQL Server 2012 to SQL Server 2014 is not supported. Similarly, restoring a site database that ran on a Standard edition of SQL Server 2014 to an Enterprise edition of SQL Server 2014 is not supported.  
> -   SQL Server must not be set to **single-user mode**.  
> -   Ensure the .MDF and .LDF files are valid. When you recover a site, there is not check for the state of the files you are restoring.  


 Site recovery is started by running the Configuration Manager Setup Wizard from the CD.Latest folder.  You can also configure  the unattended installation script and then use the Setup command **/script** option to run setup from this same CD.Latest folder. Your recovery options vary depending on whether you have a backup of the Configuration Manager site database. For more information, see [The CD.Latest folder for System Center Configuration Manager](../../core/servers/manage/the-cd.latest-folder.md).  

> [!IMPORTANT]  
>  If you run Configuration Manager Setup from the **Start** menu on the site server, the **Recover a site** option is not available.  
>   
>  If you have installed any updates from within the Configuration Manager console before making your backup, you cannot successfully reinstall the site by using Setup from installation media or the Configuration Manager installation path.  

> [!NOTE]  
>  After you restore a site database that was configured for database replicas, before you can use the database replicas you must reconfigure each database replica, recreating both the publications and subscriptions.  

###  <a name="BKMK_DetermineRecoveryOptions"></a> Determine your recovery options  
 There are two main areas that you have to consider for Configuration Manager primary site server and central administration site recovery; the site server and the site database. Use the following sections to help you determine the options that you have to select for your recovery scenario.  

> [!NOTE]  
>  When a previous site recovery failed or when you are trying to recover a site that it is not completely uninstalled, you must select **Uninstall a Configuration Manager site** from Setup before you have the option to recover the site. If the failed site has child sites, and you have to uninstall the site, you must manually delete the site database from the failed site before you select the **Uninstall a Configuration Manager site** option or the uninstall process will fail.  

####  <a name="BKMK_SiteServerRecoveryOptions"></a> Site server recovery options  
 You must start Setup from a copy of the CD.Latest folder that you create outside of the Configuration Manager installation folder. You then select the **Recover a site** option. When you run Setup, you have the following recovery options for the failed site server:  

-   **Recover the site server using an existing backup**: Use this option when you have a backup of the Configuration Manager site server that was created on the site server as part of the **Backup Site Server** maintenance task before the site failure. The site is reinstalled, and the site settings are configured, based on the site that was backed up.  

-   **Reinstall the site server**: Use this option when you do not have a backup of the site server. The site server is reinstalled, and you must specify the site settings, just as you would during an initial installation. You must use the same site code and site database name that you used when the failed site was first installed to successfully recover the site.  

> [!NOTE]  
>  When Setup detects an existing Configuration Manager site on the server, you can start a site recovery, but the recovery options for the site server are limited. For example, if you run Setup on an existing site server, when you choose recovery, you can recover the site database server, but the option to recover the site server is disabled.  

####  <a name="BKMK_SiteDatabaseRecoveryOption"></a> Site database recovery options  
 When you run Setup, you have the following recovery options for the site database:  

-   **Recover the site database using a backup set**: Use this option when you have a backup of the Configuration Manager site database that was created as part of the **Backup Site Server** maintenance task run on the site before the site database failure. When you have a hierarchy, the changes that were made to the site database after the last site database backup are retrieved from the central administration site for a primary site, or from a reference primary site for a central administration site. When you recover the site database for a stand-alone primary site, you lose site changes after the last backup.  

     When you recover the site database for a site in a hierarchy, the recovery behavior is different for a central administration site and primary site, and when the last backup is inside or outside of the SQL Server change tracking retention period. For more information, see the [Site database recovery scenarios](#BKMK_SiteDBRecoveryScenarios) section in this topic.  

    > [!NOTE]  
    >  The recovery fails if you select to restore the site database by using a backup set, but the site database already exists.  

-   **Create a new database for this site**: Use this option when you do not have a backup of the Configuration Manager site database. When you have a hierarchy, a new site database is created, and the data is recovered by using replicated data from the central administration site for a primary site, or a reference primary site for a central administration site. This option is not available when you are recovering a stand-alone primary site or a central administration site that does not have primary sites.  

-   **Use a site database that has been manually recovered**: Use this option when you have already recovered the Configuration Manager site database but have to complete the recovery process. Configuration Manager can recover the site database from the Configuration Manager backup maintenance task or from a site database backup that you perform by using DPM or another process. After you restore the site database by using a method outside Configuration Manager, you must run Setup and select this option to complete the site database recovery. When you have a hierarchy, the changes that were made to the site database after the last site database backup are retrieved from the central administration site for a primary site, or from a reference primary site for a central administration site. When you recover the site database for a stand-alone primary site, you lose site changes after the last backup.  

    > [!NOTE]  
    >  When you use DPM to back up your site database, use the DPM procedures to restore the site database to a specified location before you continue the restore process in Configuration Manager. For more information about DPM, see the [Data Protection Manager Documentation Library](http://go.microsoft.com/fwlink/?LinkId=272772) on TechNet.  

-   **Skip database recovery**: Use this option when no data loss has occurred on the Configuration Manager site database server. This option is only valid when the site database is on a different computer than the site server that you are recovering.  

####  <a name="bkmk_SQLretention"></a> SQL Server change tracking retention period  
 Change tracking is enabled for the site database in SQL Server. Change tracking lets Configuration Manager query for information about the changes that have been made to database tables after a previous point in time. The retention period specifies how long change tracking information is retained. By default, the site database is configured to have a retention period of 5 days. When you recover a site database, the recovery process proceeds differently if your backup is inside or outside the retention period. For example, if your site database server fails, and your last backup is 7 days old, it is outside the retention period.  

####  <a name="bkmk_reinit"></a> Process to reinitialize site or global data  
 The process to reinitialize site or global data replaces existing data in the site database with data from another site database. For example, when site ABC reinitializes data from site XYZ, the following steps occur:  

-   The data is copied from site XYZ to site ABC.  

-   The existing data for site XYZ is removed from the site database on site ABC.  

-   The copied data from site XYZ is inserted into the site database for site ABC.  

##### Example scenario 1  
 **The primary site reinitializes the global data from the central administration site**: The recovery process removes the existing global data for the primary site in the primary site database and replaces the data with the global data copied from the central administration site.  

##### Example scenario 2  
 **The central administration site reinitializes the site data from a primary site**: The recovery process removes the existing site data for that primary site in the central administration site database and replaces the data with the site data copied from the primary site. The site data for other primary sites is not affected.  

####  <a name="BKMK_SiteDBRecoveryScenarios"></a> Site database recovery scenarios  
 After a site database is restored from a backup, the Configuration Manager attempts to restore the changes in site and global data after the last database backup. The following  describe the actions that Configuration Manager starts after a site database is restored from backup.  

 **Recovered site is a central administration site:**  

-   **Database backup within change tracking retention period**  

    -   **Global data:** The changes in global data after the backup are replicated from all primary sites.  

    -   **Site data:** The changes in site data after the backup are replicated from all primary sites.  

-   **Database backup older than change tracking retention period**  

    -   **Global data:** The central administration site reinitializes the global data from the reference primary site, if you specify it. Then all other primary sites reinitialize the global data from the central administration site. If no reference site is specified, all primary sites reinitialize the global data from the central administration site (the data that was restored from backup).  

    -   **Site data:** The central administration site reinitializes the site data from each primary site.  

 **Recovered site is a primary site:**  

-   **Database backup within change tracking retention period**  

    -   **Global data:** The changes in global data after the backup are replicated from the central administration site.  

    -   **Site data:** The central administration site reinitializes the site data from the primary site. Changes after the backup are lost, but most data is regenerated by clients that send information to the primary site.  

-   **Database backup older than change tracking retention period**  

    -   **Global data:** The primary site reinitializes the global data from the central administration site.  

    -   **Site data:** The central administration site reinitializes the site data from the primary site. Changes after the backup are lost, but most data is regenerated by clients that send information to the primary site.  

### Site recovery procedures  
 Use one of the following procedures to help you recover your site server and site database.  

##### To start a site recovery in the Setup Wizard  

1.  Copy the CD.Latest folder to a location outside the Configuration Manager Installation folder. (See [The CD.Latest folder for System Center Configuration Manager](../../core/servers/manage/the-cd.latest-folder.md))  

     From the copy of the CD.Latest folder, run the Configuration Manager Setup Wizard.  

2.  On the **Getting Started** page, select **Recover a site**, and then click **Next**.  

3.  Complete the wizard by using the options that are appropriate for your site recovery.  

    > [!IMPORTANT]  
    >  During the recovery, Setup identifies the SQL Server Service Broker (SSB) port used by the SQL Server. Do not change this port setting during recovery or data replication will not work properly after the recovery completes.  

    > [!NOTE]  
    >  You can specify the original, or a new  path to use for the Configuration Manager installation in the Setup Wizard.  

##### To start an unattended site recovery  

1.  Prepare the unattended installation script for the options that you require for the site recovery.  

2.  Run Configuration Manager Setup by using the command **/script** option. For example, if you named your setup initialization file ConfigMgrUnattend.ini and saved it in the C:\Temp directory of the computer on which you are running Setup, the command would be as follows: **Setup /script C:\temp\ConfigMgrUnattend.ini**.  

> [!NOTE]  
>  After you recover a central administration site, replication of some site data from child sites can fail to be established. This can include hardware inventory, software inventory, and status messages.  
>   
>  If this occurs, you must reinitialize the **ConfigMgrDRSSiteQueue** for database replication.  To do so, use **SQL Server Manager** to run the following query on the Configuration Manager site database on the central administration site:  
>   
>  **IF EXISTS (SELECT \* FROM sys.service_queues WHERE name = 'ConfigMgrDRSSiteQueue' AND is_receive_enabled = 0)**  
>   
>  **ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON**  

###  <a name="BKMK_UnattendedSiteRecoveryKeys"></a> Unattended site recovery script file keys  
 To perform an unattended recovery of a Configuration Manager central administration site or primary site, you can create an unattended installation script and use Setup with the /script command option. The script provides the same type of information that the Setup Wizard prompts for, except that there are no default settings. All values must be specified for the setup keys that apply to the type of recovery you are using.  

 You can run Configuration Manager Setup unattended by using an initialization file with the /script Setup command-line option. Unattended setup is supported for recovery of a Configuration Manager central administration site and primary site. To use the /script setup command-line option, you must create an initialization file and specify the initialization file name after the /script setup command-line option. The name of the file is unimportant as long as it has the .ini file name extension. When you reference the setup initialization file from the command line, you must provide the full path to the file. For example, if your setup initialization file is named setup.ini, and it is stored in the C:\setup folder, your command line would be:  

 **setup /script c:\setup\setup.ini**.  

> [!IMPORTANT]  
>  You must have Administrator rights to run Setup. When you run Setup with the unattended script, start the Command Prompt in an Administrator context by using **Run as administrator**.  

 The script contains section names, key names, and values. Required section key names vary depending on the recovery type that you are scripting. The order of the keys within sections, and the order of sections within the file, is not important. The keys are not case sensitive. When you provide values for keys, the name of the key must be followed by an equals sign (=) and the value for the key.  

 Use the following sections to help you to create your script for unattended site recovery. The tables list the available setup script keys, their corresponding values, whether they are required, which type of installation they are used for, and a short description for the key.  

#### Recover a central administration site unattended  
 Use the following information to configure an unattended Setup script file to recover a central administration sitee.  

 **Identification**  

-   **Key name:** Action  

    -   **Required:** Yes  

    -   **Values:** RecoverCCAR  

    -   **Details:** Recovers a central administration site  

 **RecoveryOptions**  

-   **Key name:** ServerRecoveryOptions  

    -   **Required:** Yes  

    -   **Values:** 1, 2, or 4  

         1 = Recovery site server and SQL Server.  

         2 = Recover site server only.  

         4 = Recover SQL Server only.  

    -   **Details:** Specifies whether Setup will recover the site server, SQL Server, or both. The associated keys are required when you set the following value for the ServerRecoveryOptions setting:  

        -   **Value = 1** You have the option to specify a value for the **SiteServerBackupLocation** key to recover the site by using a site backup. If you do not specify a value, the site is reinstalled without restoring it from a backup set.  

             The **BackupLocation** key is required when you configure a value of **10** for the **DatabaseRecoveryOptions** key, which is to restore the site database from backup.  

        -   **Value = 2** You have the option to specify a value for the **SiteServerBackupLocation** key to recover the site by using a site backup. If you do not specify a value, the site is reinstalled without restoring it from a backup set.  

        -   **Value = 4** The **BackupLocation** key is required when you configure a value of **10** for the **DatabaseRecoveryOptions** key, which is to restore the site database from backup.  

-   **Key name:** DatabaseRecoveryOptions  

    -   **Required:** Maybe  

    -   **Values:** 10, 20, 40, 80  

         10 = Restore the site database from backup.  

         20 = Use a site database that has been manually recovered by using another method.  

         40 = Create a new database for the site. Use this option when there is no site database backup available. Global and site data is recovered through replication from other sites.  

         80 = skip database recovery.  

    -   **Details:** Specifies how Setup will recover the site database in SQL Server. This key is required when the **ServerRecoveryOptions** setting has a value of **1** or **4**.  

-   **Key name:** ReferenceSite  

    -   **Required:** Maybe  

    -   **Values:** <ReferenceSiteFQDN\>  

    -   **Details:** Specifies the reference primary site that the central administration site uses to recover global data if the database backup is older than the change tracking retention period or when you recover the site without a backup.  

         When you do not specify a reference site and the backup is older than the change tracking retention period, all primary sites are reinitialized with the restored data from the central administration site.  

         When you do not specify a reference site and the backup is within the change tracking retention period, only changes since the backup are replicated from primary sites. When there are conflicting changes from different primary sites, the central administration site uses the first one that it receives.  

         This key is required when the **DatabaseRecoveryOptions** setting has a value of **40**.  

-   **Key name:** SiteServerBackupLocation  

    -   **Required:** No  

    -   **Values:** <PathToSiteServerBackupSet\>  

    -   **Details:** Specifies the path to the site server backup set. This key is optional when the **ServerRecoveryOptions** setting has a value of **1** or **2**. Specify a value for the **SiteServerBackupLocation** key to recover the site by using a site backup. If you do not specify a value, the site is reinstalled without restoring it from a backup set.  

-   **Key name:** BackupLocation  

    -   **Required:** Maybe  

    -   **Values:** <PathToSiteDatabaseBackupSet\>  

    -   **Details:** Specifies the path to the site database backup set. The **BackupLocation** key is required when you configure a value of **1** or **4** for the **ServerRecoveryOptions** key, and configure a value of **10** for the **DatabaseRecoveryOptions** key.  

 **Options**  

-   **Key name:** ProductID  

    -   **Required:** Yes  

    -   **Values:**  

         xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  

         Eval  

    -   **Details:** The Configuration Manager installation product key, including the dashes. Enter **Eval** can install the evaluation version of Configuration Manager.  

-   **Key name:** SiteCode  

    -   **Required:** Yes  

    -   **Values:** <Site code\>  

    -   **Details:** Three alpha-numeric characters that uniquely identifies the site in your hierarchy. You must specify the site code that was used by the site before the failure.  

-   **Key name:** SiteName  

    -   **Required:** Yes  

    -   **Values:** SiteName  

    -   **Details:** Description for this site.  

-   **Key name:** SMSInstallDir  

    -   **Required:** Yes  

    -   **Values:** <*ConfigMgrInstallationPath*>  

    -   **Details:** Specifies the installation folder for the Configuration Manager program files.  

        > [!NOTE]  
        >  You can specify the original path or a new  path to use for the Configuration Manager installation.  

-   **Key name:** SDKServer  

    -   **Required:** Yes  

    -   **Values:** <*FQDN of SMS Provider*>  

    -   **Details:** Specifies the FQDN for the server that will host the SMS Provider. You must specify the server that hosted the SMS Provider before the failure.  

         You can configure additional SMS Providers for the site after the initial installation.  

-   **Key name:** PrerequisiteComp  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = download  

         1 = already downloaded  

    -   **Details:** Specifies whether Setup prerequisite files have already been downloaded. For example, if you use a value of 0, Setup will download the files.  

-   **Key name:** PrerequisitePath  

    -   **Required:** Yes  

    -   **Values:** <*PathToSetupPrerequisiteFiles*>  

    -   **Details:** Specifies the path to the Setup prerequisite files. Depending on the **PrerequisiteComp** value, Setup uses this path to store downloaded files or to locate previously downloaded files.  

-   **Key name:** AdminConsole  

    -   **Required:** Maybe  

    -   **Values:** 0 or 1  

         0 = do not install  

         1 = install  

    -   **Details:** Specifies whether to install the Configuration Manager console. This key is required except when the **ServerRecoveryOptions** setting has a value of **4**.  

-   **Key name:** JoinCEIP  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = do not join  

         1 = join  

    -   **Details:** Specifies whether to join the Customer Experience Improvement Program.  

 **SQLConfigOptions**  

-   **Key name:** SQLServerName  

    -   **Required:** Yes  

    -   **Values:** *<SQLServerName\>*  

    -   **Details:** The name of the server, or clustered instance name, running SQL Server that will host the site database. You must specify the same server that hosted the site database before the failure.  

-   **Key name:** DatabaseName  

    -   **Required:** Yes  

    -   **Values:**  

         *<SiteDatabaseName\>*  

         or  

         *<InstanceName\>*\\*<SiteDatabaseName\>*  

    -   **Details:** The name of the SQL Server database to create or use to install the central administration site database. You must specify the same database name that was used before the failure.  

        > [!IMPORTANT]  
        >  You must specify the instance name and site database name if you do not use the default instance.  

-   **Key name:** SQLSSBPort  

    -   **Required:** No  

    -   **Values:** <*SSBPortNumber*>  

    -   **Details:** Specify the SQL Server Service Broker (SSB) port used by SQL Server. Typically, SSB is configured to use TCP port 4022, but other ports are supported. You must specify the same SSB port that was used before the failure.  

#### Recover a Primary Site Unattended  
 Use the following information to configure an unattended Setup script file to recover a central administration sitee.  

 **Identification**  

-   **Key name:** Action  

    -   **Required:** Yes  

    -   **Values:** RecoverPrimarySite  

    -   **Details:** Recovers a primary site  

 **RecoveryOptions**  

-   **Key name:** ServerRecoveryOptions  

    -   **Required:** Yes  

    -   **Values:** 1, 2, or 4  

         1 = Recovery site server and SQL Server.  

         2 = Recover site server only.  

         4 = Recover SQL Server only.  

    -   **Details:** Specifies whether Setup will recover the site server, SQL Server, or both. The associated keys are required when you set the following value for the ServerRecoveryOptions setting:  

        -   **Value = 1** You have the option to specify a value for the **SiteServerBackupLocation** key to recover the site by using a site backup. If you do not specify a value, the site is reinstalled without restoring it from a backup set.  

             The **BackupLocation** key is required when you configure a value of **10** for the **DatabaseRecoveryOptions** key, which is to restore the site database from backup.  

        -   **Value = 2** You have the option to specify a value for the **SiteServerBackupLocation** key to recover the site by using a site backup. If you do not specify a value, the site is reinstalled without restoring it from a backup set.  

        -   **Value = 4** The **BackupLocation** key is required when you configure a value of **10** for the **DatabaseRecoveryOptions** key, which is to restore the site database from backup.  

-   **Key name:** DatabaseRecoveryOptions  

    -   **Required:** Maybe  

    -   **Values:** 10, 20, 40, 80  

         10 = Restore the site database from backup.  

         20 = Use a site database that has been manually recovered by using another method.  

         40 = Create a new database for the site. Use this option when there is no site database backup available. Global and site data is recovered through replication from other sites.  

         80 = skip database recovery.  

    -   **Details:** Specifies how Setup will recover the site database in SQL Server. This key is required when the **ServerRecoveryOptions** setting has a value of **1** or **4**.  

-   **Key name:** SiteServerBackupLocation  

    -   **Required:** No  

    -   **Values:** <PathToSiteServerBackupSet\>  

    -   **Details:** Specifies the path to the site server backup set. This key is optional when the **ServerRecoveryOptions** setting has a value of **1** or **2**. Specify a value for the **SiteServerBackupLocation** key to recover the site by using a site backup. If you do not specify a value, the site is reinstalled without restoring it from a backup set.  

-   **Key name:** BackupLocation  

    -   **Required:** Maybe  

    -   **Values:** <PathToSiteDatabaseBackupSet\>  

    -   **Details:** Specifies the path to the site database backup set. The **BackupLocation** key is required when you configure a value of **1** or **4** for the **ServerRecoveryOptions** key, and configure a value of **10** for the **DatabaseRecoveryOptions** key.  

 **Options**  

-   **Key name:** ProductID  

    -   **Required:** Yes  

    -   **Values:**  

         xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  

         Eval  

    -   **Details:** The Configuration Manager installation product key, including the dashes. Enter **Eval** can install the evaluation version of Configuration Manager.  

-   **Key name:** SiteCode  

    -   **Required:** Yes  

    -   **Values:** <Site code\>  

    -   **Details:** Three alpha-numeric characters that uniquely identifies the site in your hierarchy. You must specify the site code that was used by the site before the failure.  

-   **Key name:** SiteName  

    -   **Required:** Yes  

    -   **Values:** SiteName  

    -   **Details:** Description for this site.  

-   **Key name:** SMSInstallDir  

    -   **Required:** Yes  

    -   **Values:** <*ConfigMgrInstallationPath*>  

    -   **Details:** Specifies the installation folder for the Configuration Manager program files.  

        > [!NOTE]  
        >  You can specify the original path or a new  path to use for the Configuration Manager installation.  

-   **Key name:** SDKServer  

    -   **Required:** Yes  

    -   **Values:** <*FQDN of SMS Provider*>  

    -   **Details:** Specifies the FQDN for the server that will host the SMS Provider. You must specify the server that hosted the SMS Provider before the failure.  

         You can configure additional SMS Providers for the site after the initial installation.  

-   **Key name:** PrerequisiteComp  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = download  

         1 = already downloaded  

    -   **Details:** Specifies whether Setup prerequisite files have already been downloaded. For example, if you use a value of 0, Setup will download the files.  

-   **Key name:** PrerequisitePath  

    -   **Required:** Yes  

    -   **Values:** <*PathToSetupPrerequisiteFiles*>  

    -   **Details:** Specifies the path to the Setup prerequisite files. Depending on the **PrerequisiteComp** value, Setup uses this path to store downloaded files or to locate previously downloaded files.  

-   **Key name:** AdminConsole  

    -   **Required:** Maybe  

    -   **Values:** 0 or 1  

         0 = do not install  

         1 = install  

    -   **Details:** Specifies whether to install the Configuration Manager console. This key is required except when the **ServerRecoveryOptions** setting has a value of **4**.  

-   **Key name:** JoinCEIP  

    -   **Required:** Yes  

    -   **Values:** 0 or 1  

         0 = do not join  

         1 = join  

    -   **Details:** Specifies whether to join the Customer Experience Improvement Program.  

 **SQLConfigOptions**  

-   **Key name:** SQLServerName  

    -   **Required:** Yes  

    -   **Values:** *<SQLServerName\>*  

    -   **Details:** The name of the server, or clustered instance name, running SQL Server that will host the site database. You must specify the same server that hosted the site database before the failure.  

-   **Key name:** DatabaseName  

    -   **Required:** Yes  

    -   **Values:**  

         *<SiteDatabaseName\>*  

         or  

         *<InstanceName\>*\\*<SiteDatabaseName\>*  

    -   **Details:** The name of the SQL Server database to create or use to install the central administration site database. You must specify the same database name that was used before the failure.  

        > [!IMPORTANT]  
        >  You must specify the instance name and site database name if you do not use the default instance.  

-   **Key name:** SQLSSBPort  

    -   **Required:** No  

    -   **Values:** <*SSBPortNumber*>  

    -   **Details:** Specify the SQL Server Service Broker (SSB) port used by SQL Server. Typically, SSB is configured to use TCP port 4022, but other ports are supported. You must specify the same SSB port that was used before the failure.  

 **Hierarchy ExpansionOption**  

-   **Key name:** CCARSiteServer  

    -   **Required:** Maybe  

    -   **Values:** <*SiteCodeForCentralAdministrationSite*>  

    -   **Details:** Specifies the central administration site that a primary site will attach to when it joins the Configuration Manager hierarchy. This setting is required if the primary site was attached to a central administration site before the failure. You must specify the site code that was used for the central administration site before the failure.  

-   **Key name:** CASRetryInterval  

    -   **Required:** No  

    -   **Values:** <*Interval*>  

    -   **Details:** Specifies the retry interval (in minutes) to attempt a connection to the central administration site after the connection fails. For example, if the connection to the central administration site fails, the primary site waits the number of minutes that you specify for CASRetryInterval, and then re-attempts the connection.  

-   **Key name:** WaitForCASTimeout  

    -   **Required:** No  

    -   **Values:** <*Timeout*>  

    -   **Details:** Specifies the maximum timeout value (in minutes) for a primary site to connect to the central administration site. For example, if a primary site fails to connect to a central administration site, the primary site retries the connection to the central administration site based on the CASRetryInterval until the WaitForCASTimeout period is reached. You can specify a value of 0 to 100.  

###  <a name="BKMK_PostRecovery"></a> Post-recovery tasks  
 After you recover your site, there are several post-recovery tasks that you must consider before your site recovery is completed. Use the following sections to help you complete your site recovery process.  

#### Re-enter user account passwords  
 After a site server recovery, passwords for the user accounts specified for the site must be re-entered because they are reset during the site recovery. The accounts are listed on the **Finished** page of the Setup Wizard after site recovery is completed and saved to C:\ConfigMgrPostRecoveryActions.html on the recovered site server.  

###### To re-enter user account passwords after site recovery  

1.  Open the Configuration Manager console and connect to the recovered site.  

2.  In the Configuration Manager console, click **Administration**.  

3.  In the **Administration** workspace, expand **Security**, and then click **Accounts**.  

4.  For each account in which you have to re-enter the password, do the following:  

    1.  Select the account from the list of accounts that were identified after site recovery. You can find this list in C:\ConfigMgrPostRecoveryActions.html on the recovered site server.  

    2.  On the **Home** tab, in the **Properties** group, click **Properties** to open the account properties.  

    3.  On the **General** tab, click **Set**, and then re-enter the passwords for the account.  

    4.  Click **Verify**, select the appropriate data source for the selected user account, and then click **Test connection** to verify that the user account can connect to the data source.  

    5.  Click **OK** to save the password changes, and then click **OK**.  

#### Re-enter sideloading keys  
 After a site server recovery, you must re-enter Windows sideloading keys specified for the site because they are reset during site recovery. After you re-enter the sideloading keys, the count in the **Activations used** column for Windows sideloading keys is reset in the Configuration Manager console. For example, let's say before the site failure you have a **Total activations** count set to **100** and **Activations used** is at **90** for the number of the keys that have been used by devices. After the site recovery, the **Total activations** column still displays **100**, but the **Activations used** column incorrectly displays **0**. However, after 10 new devices use a sideloading key, there will be no remaining sideloading keys, and the next device will fail to apply a sideloading key.  

#### Recreate the Microsoft Intune subscription  
 If you recover a Configuration Manager site server after the site server computer is  re-imaged, the Microsoft Intune subscription is not restored. You must recreate the subscription after you recover the site. For more information, see [Configuring the Microsoft Intune subscription](../../mdm/plan-design/hybrid-mobile-device-management.md#bkmk_witsub).  

#### Configure SSL for site system roles that use IIS  
 When you recover site systems that run IIS and that were configured for HTTPS before the failure, you must reconfigure IIS to use the web server certificate.  

#### Reinstall hotfixes in the recovered site server  
 After a site recovery, you must reinstall any hotfixes that were applied to the site server. A list of the previously installed hotfixes are listed on the **Finished** page of the Setup Wizard after site recovery and saved to **C:\ConfigMgrPostRecoveryActions.html** on the recovered site server.  

#### Recover custom reports on the computer running Reporting Services  
 When you have created custom Reporting Services reports, and Reporting Services fails, you can recover the reports when you have backed up the report server. For more information about restoring your custom reports in Reporting Services, see [Backup and Restore Operations for a Reporting Services Installation](http://go.microsoft.com/fwlink/p/?LinkId=228724) in the SQL Server 2008 Books Online.  

#### Recover content files  
 The site database contains information about where the content files are stored on the site server, but the content files are not backed up or restored as part of the backup and recovery process. To fully recover content files, you must restore the content library and package source files to the original location. There are several methods for recovering your content files, but the easiest method is to restore the files from a file system backup of the site server.  

 If you do not have a file system backup for the package source files, you have to manually copy or download them as you did originally when you first created the package. You can run the following query in SQL Server to find the package source location for all packages and applications: `SELECT * FROM v_Package`. You can identify the package source site by looking at the first three characters of the package ID. For example, if the package ID is CEN00001, the site code for the source site is CEN. When you restore the package source files, they must be restored to the same location in which they were before the failure.  

 If you do not have a file system backup that contains the content library, you have the following restore options:  

-   **Import a prestaged content file**: When you have a Configuration Manager hierarchy, you can create a prestaged content file with all packages and applications from another location, and then import the prestaged content file to recover the content library on the site server.  

-   **Update content**: When you start the update content action for a package or application deployment type, the content is copied from the package source to the content library. The package source files must be available in the original location for this action to finish successfully. You must perform this action on each package and application.  

#### Recover custom software updates on the computer running Updates Publisher  
 When you have included Updates Publisher database files in your backup plan, you can recover the databases in case of a failure on the computer on which Updates Publisher runs. For more information about Updates Publisher, see [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkId=228726) in the System Center TechCenter Library.  

 Use the following procedure to restore the Updates Publisher database.  

###### To restore the Updates Publisher 2011 database  

1.  Reinstall Updates Publisher on the recovered computer.  

2.  Copy the database file (Scupdb.sdf) from your backup destination to %*USERPROFILE*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\ on the computer that runs Updates Publisher.  

3.  When more than one user runs Updates Publisher on the computer, you must copy each database file to the appropriate user profile location.  

#### User State Migration data  
 As part of the state migration point site system properties, you specify the folders that store user state migration data. After you recover a server with a folder that stores user state migration data, you must manually restore the user state migration data on the server to the same folders that stored the data prior to the failure.  

#### Regenerate the certificates for distribution points  
 After you restore a site, the distmgr.log might contain the following entry for one or more distribution points: **Failed to decrypt cert PFX data**. This entry indicates that the distribution point certificate data cannot be decrypted by the site. To resolve this you must regenerate or re-import the certificate for affected distribution points. This can be done by using the [Set-CMDistributionPoint](https://technet.microsoft.com/library/jj821872\(v=sc.20\).aspx) PowerShell cmdlet.  

#### Update Certificates Used for Cloud-Based distribution points  
 Configuration Manager requires a management certificate that it uses for site server to cloud-based distribution point communication. After a site recovery, you must update the certificates for cloud-based distribution points.  

####  <a name="BKMK_RecoverSecondarySite"></a> Recover a secondary site  
 Configuration Manager does not support the backup of the database at a secondary site, but does support recovery by reinstalling the secondary site. Secondary site recovery is required when a Configuration Manager secondary site fails. You can recover a secondary site by using the **Recover Secondary Site** action from the **Sites** node in the Configuration Manager console. Unlike recovery for a central administration site or primary site, recovery for a secondary site does not use a backup file and instead reinstalls the secondary site files on the failed secondary site computer. Then,  the secondary site data is reinitialized with data from the parent primary site. During the recovery process, Configuration Manager verifies if the content library exists on the secondary site computer and that the appropriate content is available. The secondary site will use the existing content library, if it contains the appropriate content. Otherwise, to recover the content library of a recovered secondary site requires you to redistribute or prestage the content to that recovered site. When you have a distribution point that is not on the secondary site, you are not required to reinstall the distribution point during a recovery of the secondary site. After the secondary site recovery, the site automatically synchronizes with the distribution point.  

 You can verify the status of the secondary site recovery, by using the **Show Install Status** action from the **Sites** node in the Configuration Manager console.  

> [!IMPORTANT]  
>  You must use a computer with the same configuration as the failed computer, such as its FQDN, to successfully recover the secondary site. The computer must also meet all secondary site prerequisites and have appropriate security rights configured. Also, use the same installation path that was used for the failed site.  

> [!IMPORTANT]  
>  During a secondary site recovery, Configuration Manager does not install SQL Server Express if it is not installed on the computer. Therefore, before you recover a secondary site, you must manually install SQL Server Express or SQL Server. You must use the same version of SQL Server and the same instance of SQL Server that you used for the secondary site database before the failure.  

##  <a name="BKMK_SMSWriterService"></a> SMS Writer service  
 The SMS Writer is a service that interacts with the Volume Shadow Copy Service (VSS) during the backup process. The SMS Writer service must be running for the Configuration Manager site back up to successfully complete.  

### Purpose  
 SMS Writer registers with the VSS service and binds to its interfaces and events. When VSS broadcasts events, or if it sends specific notifications to the SMS Writer, the SMS Writer responds to the notification and takes the appropriate action. The SMS Writer reads the backup control file (smsbkup.ctl), located in the <*ConfigMgr Installation Path*>\inboxes\smsbkup.box, and determines the files and data that is to be backed up. The SMS Writer builds metadata, which consists of various components, based on this information as well as specific data from the SMS registry key and subkeys. It sends the metadata to VSS when it is requested. VSS then sends the metadata to the requesting application; Configuration Manager Backup Manager. Backup Manager selects the data that gets backed up and sends this data to the SMS Writer via VSS. The SMS Writer takes the appropriate steps to prepare for the backup. Later, when VSS is ready to take the snapshot, it sends an event, the SMS Writer stops all Configuration Manager services and ensures that the Configuration Manager activities are frozen while the snapshot is created. After the snapshot is complete, the SMS Writer restarts services and activities.  

 The SMS Writer service is installed automatically. It must be running when the VSS application requests a backup or restore.  

### Writer ID  
 The writer ID for the SMS Writer is: 03ba67dd-dc6d-4729-a038-251f7018463b.  

### Permissions  
 The SMS Writer service must run under the Local System account.  

### Volume Shadow Copy service  
 The VSS is a set of COM APIs that implements a framework to allow volume backups to be performed while applications on a system continue to write to the volumes. The VSS provides a consistent interface that allows coordination between user applications that update data on disk (the SMS Writer service) and those that back up applications (the Backup Manager service). For more information about VSS, see the [Volume Shadow Copy Service](http://go.microsoft.com/fwlink/p/?LinkId=241968) topic in the Windows Server TechCenter.  
