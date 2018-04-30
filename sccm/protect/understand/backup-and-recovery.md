---
title: "Backup sites"
titleSuffix: "Configuration Manager"
description: "Learn to back up your sites before the event of failure or data loss in System Center Configuration Manager."
ms.date: 6/5/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f7832d83-9ae2-4530-8a77-790e0845e12f
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Back up a Configuration Manager site

*Applies to: System Center Configuration Manager (Current Branch)*

Prepare backup and recovery approaches to avoid data loss. For Configuration Manager sites, a backup and recovery approach can help you to recover sites and hierarchies more quickly, and with the least data loss.  

The sections in this topic can help you back up your sites. To recover a site, see [Recovery for Configuration Manager](/sccm/protect/understand/recover-sites).  

## Considerations before creating a backup  
-   **If you use a SQL Server Always On availability group to host the site database:** Modify your backup and recovery plans as described in [Prepare to use SQL Server Always On](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#changes-for-site-backup).

-   Configuration Manager can recover the site database from the Configuration Manager backup maintenance task or from a site database backup that you create with another process.   

    For example, you can restore the site database from a backup that is created as part of a Microsoft SQL Server maintenance plan. You can also use a backup that is created by Using Data Protection Manager to back up your site database (DPM).

####  Using Data Protection Manager to back up your site database
You can use System Center 2012 Data Protection Manager (DPM) to back up your site database.

You must create a new protection group in DPM for the site database computer. On the **Select Group Members** page of the Create New Protection Group Wizard, you select the SMS Writer service from the data source list, and then select the site database as an appropriate member. For more information about using DPM to back up your site database, see the [Data Protection Manager Documentation Library](http://go.microsoft.com/fwlink/?LinkId=272772) on TechNet.  

> [!IMPORTANT]  
>  Configuration Manager does not support DPM back up for a SQL Server cluster that uses a named instance, but does support DPM back up on a SQL Server cluster that uses the default instance of SQL Server.  

 After you restore the site database, follow the steps in Setup to recover the site. Select the **Use a site database that has been manually recovered** recovery option to use the site database that you recovered with Data Protection Manager.  

## Backup maintenance task
You can automate backup for Configuration Manager sites by scheduling the predefined Backup Site Server maintenance task. This task:

-   Runs on a schedule
-   Backs up the site database
-   Backs up specific registry keys
-   Backs up specific folders and files
-   Backs up the [CD.Latest folder](/sccm/core/servers/manage/the-cd.latest-folder)   

Plan to run the default site backup task at a minimum of every 5 days. This is because Configuration Manager uses a *SQL Server change tracking retention period* of 5 days.  (See [SQL Server change tracking retention period](/sccm/protect/understand/recover-sites#bkmk_SQLretention) in the Recover sites topic.)

To simplify the backup process, you can create an **AfterBackup.bat** file to perform post-backup actions automatically after the backup maintenance task runs successfully. The AfterBackup.bat file is usually used to archive the backup snapshot to a secure location. You can also use the AfterBackup.bat file to copy files to your backup folder and start other, supplemental backup tasks.  

You can back up a central administration site and primary site, but there is no backup support for secondary sites or site system servers.

When the Configuration Manager backup service runs, it follows the instructions defined in the backup control file (**&lt;ConfigMgrInstallationFolder\>\Inboxes\Smsbkup.box\Smsbkup.ctl**). You can modify the backup control file to change the behavior of the backup service.  

Site backup status information is written to the **Smsbkup.log** file. This file is created in the destination folder that you specify in the Backup Site Server maintenance task properties.  

#### To enable the site backup maintenance task  

1.  In the Configuration Manager console, open **Administration** > **Site Configuration** > **Sites**.  

2.  Select the site in which you want to enable the site backup maintenance task.  

3.  On the **Home** tab, in the **Settings** group, choose **Site Maintenance Tasks**.  

4.  Choose **Backup Site Server**  >  **Edit**.  

5.  Choose **Enable this task** > **Set Paths** to specify the backup destination. You have the following options:  

    > [!IMPORTANT]  
    >  To help prevent tampering of the backup files, store the files in a secure location. The most secure backup path is to a local drive, so you can set NTFS file system permissions on the folder. Configuration Manager does not encrypt the backup data that is stored in the backup path.  

    -   **Local drive on site server for site data and database**: Specifies that the backup files for the site and site database are stored in the specified path on the local disk drive of the site server. You must create the local folder before the backup task runs. The Local System account on the site server must have **Write** NTFS file system permissions to the local folder for the site server backup. The Local System account on the computer that is running SQL Server must have **Write** NTFS permissions to the folder for the site database backup.  

    -   **Network path (UNC name) for site data and database**: Specifies that the backup files for the site and site database are stored in the specified UNC path. You must create the share before the backup task runs. The computer account of the site server and the computer account of the SQL Server, if SQL Server is installed on another computer, must have **Write** NTFS and share permissions to the shared network folder.  

    -   **Local drives on site server and SQL Server**: Specifies that the backup files for the site are stored in the specified path on the local drive of the site server, and the backup files for the site database are stored in the specified path on the local drive of the site database server. You must create the local folders before the backup task runs. The computer account of the site server must have **Write** NTFS permissions to the folder that you create on the site server. The computer account of the SQL Server must have **Write** NTFS permissions to the folder that you create on the site database server. This option is available only when the site database is not installed on the site server.  

    > [!NOTE]  
    >	The option to browse to the backup destination is only available when you specify the UNC path of the backup destination.

    > The folder name or share name that is used for the backup destination does not support the use of Unicode characters.  

6.  Configure a schedule for the site backup task. As a best practice, consider a backup schedule that is outside active working hours. If you have a hierarchy, consider a schedule that runs at least two times a week to ensure maximum data retention in the event of site failure.  

    When you run the Configuration Manager console on the same site server that you are configuring for backup, the Backup Site Server maintenance task uses local time for the schedule. When the Configuration Manager console is run from a computer remote from the site that you are configuring for backup, the Backup Site Server maintenance task uses UTC for the schedule.  

7.  Choose whether to create an alert if the site backup task fails, click **OK**, and then click **OK**. When selected, Configuration Manager creates a critical alert for the backup failure that you can review in the **Alerts** node in the **Monitoring** workspace.  

 Next, verify that the Backup Site Server maintenance task is running, to ensure that backups are being created.  

#### To verify that the Backup Site Server maintenance task is running  
Verify that the Site Backup maintenance task is running by reviewing any of the following:  

-   Check the timestamp on the files in the backup destination folder that the task created. Verify that the timestamp has been updated with a time that matches the time when the task was last scheduled to run.  

-   In the **Component Status** node in the **Monitoring** workspace, review the status messages for SMS_SITE_BACKUP. When site backup is completed successfully, you see message ID 5035, which indicates that the site backup was completed without any errors.  

-   When the Backup Site Server maintenance task is configured to create an alert if backup fails, you can check the **Alerts** node in the **Monitoring** workspace for backup failures.  

-   In &lt;*ConfigMgrInstallationFolder*>\Logs, review Smsbkup.log for warnings and errors. When site backup is completed successfully, you see `Backup completed` with a timestamp and message ID `STATMSG: ID=5035`.  

    > [!TIP]  
    >  When the backup maintenance task fails, you can restart the backup task by stopping and restarting the SMS_SITE_BACKUP service.  

## Archive the backup snapshot  
The first time the Backup Site Server maintenance task runs, it creates a backup snapshot, which you can use to recover your site server in case of a failure. When the backup task runs again during subsequent cycles, it creates a new backup snapshot that overwrites the previous snapshot. As a result, the site has only a single backup snapshot, and you have no way of retrieving an earlier backup snapshot.  

As a best practice, keep multiple archives of the backup snapshot for the following reasons:  

-   It is common for backup media to fail, get misplaced, or contain only a partial backup. Recovering a failed stand-alone primary site from an older backup is better than recovering without any backup. For a site server in a hierarchy, the backup must be in the SQL Server change tracking retention period, or the backup is not required.  

-   A corruption in the site can go undetected for several backup cycles. You might have to use a backup snapshot from before the site became corrupted. This applies to a stand-alone primary site and to sites in a hierarchy where the backup is in the SQL Server change tracking retention period.  

-   The site might have no backup snapshot at all if, for example, the Backup Site Server maintenance task fails. Because the backup task removes the previous backup snapshot before it starts to back up the current data, there will not be a valid backup snapshot.  

## Using the AfterBackup.bat file  
After successfully backing up the site, the Backup Site Server task automatically attempts to run a file that is named AfterBackup.bat. You must manually create the AfterBackup.bat file in &lt;*ConfigMgrInstallationFolder*>\Inboxes\Smsbkup. If an AfterBackup.bat file exists, and is stored in the correct folder, it automatically runs after the backup task is completed.

The AfterBackup.bat file lets you archive the backup snapshot at the end of every backup operation, and automatically perform other post-backup tasks that are not part of the Backup Site Server maintenance task. The AfterBackup.bat file integrates the archive and the backup operations, thereby ensuring that every new backup snapshot is archived.

When the AfterBackup.bat file is not present, the backup task skips it without effect on the backup operation. To verify that the site backup task successfully ran the AfterBackup.bat file, see the **Component Status** node in the **Monitoring** workspace and review the status messages for SMS_SITE_BACKUP. When the task successfully started the AfterBackup.bat command file, you see message ID 5040.  

> [!TIP]  
>  To create the AfterBackup.bat file to archive your site server backup files, you must use a copy command tool, like [Robocopy](http://go.microsoft.com/fwlink/p/?LinkId=228408), in the batch file. For example, you could create the AfterBackup.bat file, and on the first line, you could add something like: `Robocopy E:\ConfigMgr_Backup \\ServerName\ShareName\ConfigMgr_Backup /MIR`  

 Although the intended use of the AfterBackup.bat is to archive backup snapshots, you can create an AfterBackup.bat file to perform additional tasks at the end of every backup operation.  

##  Supplemental backup tasks  
The Backup Site Server maintenance task provides a backup snapshot for the site server files and site database, but there are other items not backed up that you must consider when you create your backup strategy. Use the following sections to help you complete your Configuration Manager backup strategy.  

### Back up custom Reporting Services reports  
When you have modified predefined or created custom Reporting Services reports, creating a backup for the report server database files is an important part of your backup strategy. The report server backup must include a backup of the source files for reports and models, encryption keys, custom assemblies or extensions, configuration files, custom SQL Server views used in custom reports, custom stored procedures, and so on.  

> [!IMPORTANT]  
>  When Configuration Manager updates to a newer version, the predefined reports might be overwritten by new reports. If you modify a predefined report, back up the report, and then restore it in Reporting Services.  

 For more information about backing up your custom reports in Reporting Services, see [Backup and Restore Operations for a Reporting Services Installation](https://technet.microsoft.com/library/ms155814\(v=sql.120\).aspx) in the SQL Server 2014 Books Online.  

### Back up content files  
The content library in Configuration Manager is the location where all content files are stored for software updates, applications, operating system deployment, and so on. The content library is located on the site server and on each distribution point. The Backup Site Server maintenance task does not include a backup for the content library or the package source files. When a site server fails, the information about the content library files is restored to the site database, but you must restore the content library and package source files on the site server.  

-   **Content library**: The content library must be restored before you can redistribute content to distribution points. When you start content redistribution, Configuration Manager copies the files from the content library on the site server to the distribution points. The content library for the site server is in the SCCMContentLib folder, which is typically located on the drive with the most free disk space at the time when the site was installed.  

-   **Package source files**: The package source files must be restored before you can update content on distribution points. When you start a content update, Configuration Manager copies new or modified files from the package source to the content library, which in turn copies the files to associated distribution points. You can run the following query in SQL Server to find the package source location for all packages and applications: `SELECT * FROM v_Package`. You can identify the package source site by looking at the first three characters of the package ID. For example, if the package ID is CEN00001, the site code for the source site is CEN. When you restore the package source files, they must be restored to the same location where they were before the failure.  

 Verify that you include both the content library and package source locations in your file system backup for the site server.  

### Back up custom software updates  
 System Center Updates Publisher 2011 is a stand-alone tool that lets you publish custom software updates to Windows Server Update Services (WSUS), synchronize the software updates to Configuration Manager, assess software updates compliance, and deploy the custom software updates to clients. Updates Publisher uses a local database for its software update repository. When you use Updates Publisher to manage custom software updates, determine whether you should include the Updates Publisher database in your backup plan. For more information about Updates Publisher, see [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkId=228726) in the System Center TechCenter Library.  

 Use the following procedure to back up the Updates Publisher database.  

#### To back up the Updates Publisher 2011 database  

1.  On the computer that runs Updates Publisher, browse to the Updates Publisher database file (Scupdb.sdf) in %*USERPROFILE*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\\. There is a different database file for each user that runs Updates Publisher.  

2.  Copy the database file to your backup destination. For example, if your backup destination is E:\ConfigMgr_Backup, you could copy the Updates Publisher database file to E:\ConfigMgr_Backup\SCUP2011.  

    > [!TIP]  
    >  When there is more than one database file on a computer, consider storing the file in a subfolder that indicates the user profile associated with the database file. For example, you could have one database file in E:\ConfigMgr_Backup\SCUP2011\User1 and another database file in E:\ConfigMgr_Backup\SCUP2011\User2.  

## User state migration data  
You can use Configuration Manager task sequences to capture and restore the user state data in operating system deployment scenarios where you want to retain the user state of the current operating system. The folders that store the user state data are listed in the properties for the state migration point. This user state migration data is not backed up as part of the Site Server Backup maintenance task. As part of your backup plan, you must manually back up the folders that you specify to store the user state migration data.   

### To determine the folders used to store user state migration data  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, expand **Site Configuration**, and choose **Servers and Site System Roles**.  

3.  Select the site system that hosts the state migration role, and choose **State migration point** in **Site System Roles**.  


4.  On the **Site Role** tab, in the **Properties** group, click **Properties**.  
5.  The folders that store the user state migration data are listed in the **Folder details** section on the **General** tab.  



## About the SMS Writer service  
The SMS Writer is a service that interacts with the Volume Shadow Copy Service (VSS) during the backup process. The SMS Writer service must be running for the Configuration Manager site back up to successfully complete.  

### Purpose  
SMS Writer registers with the VSS service and binds to its interfaces and events. When VSS broadcasts events, or if it sends specific notifications to the SMS Writer, the SMS Writer responds to the notification and takes the appropriate action. The SMS Writer reads the backup control file (smsbkup.ctl), located in the &lt;*ConfigMgr Installation Path*>\inboxes\smsbkup.box, and determines the files and data that is to be backed up. The SMS Writer builds metadata, which consists of various components, based on this information as well as specific data from the SMS registry key and subkeys. It sends the metadata to VSS when it is requested. VSS then sends the metadata to the requesting application; Configuration Manager Backup Manager. Backup Manager selects the data that gets backed up and sends this data to the SMS Writer via VSS. The SMS Writer takes the appropriate steps to prepare for the backup. Later, when VSS is ready to take the snapshot, it sends an event, the SMS Writer stops all Configuration Manager services and ensures that the Configuration Manager activities are frozen while the snapshot is created. After the snapshot is complete, the SMS Writer restarts services and activities.  

The SMS Writer service is installed automatically. It must be running when the VSS application requests a backup or restore.  

### Writer ID  
The writer ID for the SMS Writer is: 03ba67dd-dc6d-4729-a038-251f7018463b.  

### Permissions  
The SMS Writer service must run under the Local System account.  

### Volume Shadow Copy service  
The VSS is a set of COM APIs that implements a framework to allow volume backups to be performed while applications on a system continue to write to the volumes. The VSS provides a consistent interface that allows coordination between user applications that update data on disk (the SMS Writer service) and those that back up applications (the Backup Manager service). For more information, see the [Volume Shadow Copy Service](http://go.microsoft.com/fwlink/p/?LinkId=241968) topic in the Windows Server TechCenter.  

## Next steps
After you create a backup, practice [site recovery](/sccm/protect/understand/recover-sites) with that backup. This can help you become familiar with the recovery process before you need to rely on it and can help confirm the backup was successful for its intended purpose.  
