---
title: Backup sites
titleSuffix: Configuration Manager
description: Learn to back up your sites before the event of failure or data loss in Configuration Manager.
ms.date: 10/08/2020
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

# Back up a Configuration Manager site

*Applies to: Configuration Manager (current branch)*

Prepare backup and recovery approaches to avoid data loss. For Configuration Manager sites, a backup and recovery approach can help you to recover sites and hierarchies more quickly, and with the least data loss.  

The sections in this article can help you back up your sites. To recover a site, see [Recovery for Configuration Manager](recover-sites.md).  

<!--/SCCMdocs/issues/2108-->
> [!WARNING]
> The two backup methods supported for Configuration Manager site recovery are:
>
> - A successful backup from the **Backup Site Server** maintenance task
> - A manually recovered site database backup

## Considerations before creating a backup  

- If you use a SQL Server Always On availability group to host the site database: Modify your backup and recovery plans as described in [Prepare to use an availability group](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#changes-for-site-backup).  

- Configuration Manager can recover the site database from the Configuration Manager backup task. It can also use a backup of the site database that you create with another process.

    For example, you can restore the site database from a backup that's created as part of a SQL Server maintenance plan. You can also use a backup that's created by using Data Protection Manager to back up your site database.  

- You can also install an additional site server in *passive* mode. The site server in passive mode is in addition to your existing site server in *active* mode. A site server in passive mode is available for immediate use, when needed. For more information, see [Site server high availability](../deploy/configure/site-server-high-availability.md). While this role doesn't remove the need to plan for and practice backup and recovery operations, it significantly reduces the effort to recover a site when necessary.

### Using Data Protection Manager to back up your site database

You can use System Center Data Protection Manager (DPM) to back up your Configuration Manager site database.

Create a new protection group in DPM for the site database computer. On the **Select Group Members** page of the Create New Protection Group Wizard, you select the SMS Writer service from the data source list. Then select the site database as an appropriate member. For more information about using DPM, see the [Data Protection Manager](/system-center/dpm) documentation library.  

> [!IMPORTANT]  
> Configuration Manager doesn't support DPM backup for a SQL Server Always On failover cluster instance that uses a named instance. It does support DPM backup on a failover cluster instance that uses the default instance of SQL Server.

After you restore the site database, follow the steps in setup to recover the site. To use the site database that you backed up with Data Protection Manager, select the recovery option to **Use a site database that has been manually recovered**.

## Backup maintenance task

You can automate backup for Configuration Manager sites by scheduling the predefined Backup Site Server maintenance task. This task has the following features:

- Runs on a schedule
- Backs up the site database
- Backs up specific registry keys
- Backs up specific folders and files
- Backs up the [CD.Latest folder](the-cd.latest-folder.md)

Plan to run the default site backup task at a minimum of every five days. This schedule is because Configuration Manager uses a *SQL Server change tracking retention period* of five days. For more information, see [SQL Server change tracking retention period](recover-sites.md#sql-server-change-tracking-retention-period).

To simplify the backup process, you can create an **AfterBackup.bat** file. This script automatically runs post-backup actions after the backup task completes successfully. Use the AfterBackup.bat file to archive the backup snapshot to a secure location. You can also use the AfterBackup.bat file to copy files to your backup folder, or to start other backup tasks.  

You can back up a central administration site and primary site. Secondary sites or site system servers don't have backup tasks.

When the Configuration Manager backup service runs, it follows the instructions defined in the backup control file: `<ConfigMgrInstallationFolder>\Inboxes\Smsbkup.box\Smsbkup.ctl`. You can modify the backup control file to change the behavior of the backup service.  
> [!NOTE]
> Modifications of **Smsbkup.ctl** will apply after a restart of the service SMS_SITE_VSS_WRITER on the Site Server.

Site backup status information is written to the **Smsbkup.log** file. This file is created in the destination folder that you specify in the properties of the Backup Site Server maintenance task.  

### To enable the site backup maintenance task

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node.

1. Select the site for which you want to enable the site backup maintenance task.

1. Select **Site Maintenance Tasks** in the ribbon.

1. Select the **Backup Site Server** task, and select **Edit**.

1. Select the option to **Enable this task**. Select **Set Paths** to specify the backup destination. You have the following options:

    > [!IMPORTANT]
    >  To help prevent tampering of the backup files, store the files in a secure location. The most secure backup path is to a local drive, so you can set NTFS file permissions on the folder. Configuration Manager doesn't encrypt the backup data that's stored in the backup path.

    - **Local drive on site server for site data and database**: Specifies that the task stores the backup files for the site and site database in the specified path on the local disk drive of the site server. Create the local folder before the backup task runs. The Local System account on the site server must have **Write** NTFS file permissions to the local folder for the site server backup. The Local System account on the computer that's running SQL Server must have **Write** NTFS permissions to the folder for the site database backup.

    - **Network path (UNC name) for site data and database**: Specifies that the task stores the backup files for the site and site database in the specified network path. Create the share before the backup task runs. The computer account of the site server must have **Write** NTFS and share permissions to the shared network folder. If SQL Server is installed on another computer, the computer account of the SQL Server must have the same permissions.

    - **Local drives on site server and SQL Server**: Specifies that the task stores the backup files for the site in the specified path on the local drive of the site server. The task stores the backup files for the site database in the specified path on the local drive of the site database server. Create the local folders before the backup task runs. The computer account of the site server must have **Write** NTFS permissions to the folder that you create on the site server. The computer account of the SQL Server must have **Write** NTFS permissions to the folder that you create on the site database server. This option is available only when the site database isn't installed on the site server.

    > [!NOTE]
    > The option to browse to the backup destination is only available when you specify the network path of the backup destination.
    >
    > The folder name or share name that's used for the backup destination doesn't support the use of Unicode characters.

1. Configure a schedule for the site backup task. Consider a backup schedule that's outside active working hours. If you have a hierarchy, consider a schedule that runs at least two times a week. If the site fails, this schedule ensures maximum data retention.

    When you run the Configuration Manager console on the same site server that you're configuring for backup, the backup task uses local time for the schedule. When you run the Configuration Manager console from another computer, the backup task uses Coordinated Universal Time (UTC) for the schedule.

1. Choose whether to create an alert if the site backup task fails. When selected, Configuration Manager creates a critical alert for the backup failure. You can review these alerts in the **Alerts** node of the **Monitoring** workspace.

#### Verify that the Backup Site Server maintenance task is running

- Check the timestamp on the files in the backup destination folder that the task created. Verify that the timestamp updates to the time when the task was last scheduled to run.

- Go to the **Component Status** node of the **Monitoring** workspace. Review the status messages for **SMS_SITE_BACKUP**. When site backup completes successfully, you see message ID **5035**. This message indicates that the site backup completed without any errors.

- When you configure the backup task to create an alert when it fails, look for backup failure alerts in the **Alerts** node of the **Monitoring** workspace.

- Open Windows Explorer on the site server and browse to `<ConfigMgrInstallationFolder>\Logs`. Review **Smsbkup.log** for warnings and errors. When site backup completes successfully, the log shows `Backup completed` with message ID `STATMSG: ID=5035`.

    > [!TIP]
    > When the backup maintenance task fails, restart the backup task by stopping and restarting the **SMS_SITE_BACKUP** Windows service.

## Archive the backup snapshot

The backup task creates a backup snapshot the first time it runs. You can use this snapshot to recover your site server if it fails. When the backup task runs again on schedule, it creates a new backup snapshot that overwrites the previous snapshot. As a result, the site has only a single backup snapshot, and you've no way of retrieving an earlier backup snapshot.

Keep multiple archives of the backup snapshot for the following reasons:

- It's common for backup media to fail, get misplaced, or include only a partial backup. Recovering a failed stand-alone primary site from an older backup is better than recovering without any backup. For a site server in a hierarchy, the backup must be in the SQL Server change tracking retention period, or the backup isn't required.

- A corruption in the site can go undetected for several backup cycles. You might have to use a backup snapshot from before the site became corrupted. This reason applies to a stand-alone primary site and to sites in a hierarchy where the backup is in the SQL Server change tracking retention period.

- The site might have no backup snapshot at all. For example, if the Backup Site Server maintenance task fails. Because the backup task removes the previous backup snapshot before it starts to back up the current data, there won't be a valid backup snapshot.

## Use the AfterBackup.bat file

After successfully backing up the site, the backup task automatically tries to run a script named **AfterBackup.bat**. Manually create the AfterBackup.bat file on the site server in `<ConfigMgrInstallationFolder>\Inboxes\Smsbkup.box`. If an AfterBackup.bat file exists in the correct folder, it automatically runs after the backup task completes.

The AfterBackup.bat file lets you archive the backup snapshot at the end of every backup operation. It can automatically perform other post-backup tasks that aren't part of the Backup Site Server maintenance task. The AfterBackup.bat file integrates the archive and the backup operations, thereby ensuring that every new backup snapshot is archived.

If the AfterBackup.bat file isn't present, the backup task skips it without effect on the backup operation. To verify that the backup task successfully ran this script, go to the **Component Status** node in the **Monitoring** workspace, and review the status messages for **SMS_SITE_BACKUP**. When the task successfully starts the AfterBackup.bat command file, you see message ID **5040**.

> [!TIP]
> To archive your site server backup files with AfterBackup.bat, you must use a copy command tool in the batch file. One such tool is [Robocopy](/windows-server/administration/windows-commands/robocopy) in Windows Server. For example, create the AfterBackup.bat file with the following command: `Robocopy E:\ConfigMgr_Backup \\ServerName\ShareName\ConfigMgr_Backup /MIR`

Although the intended use of the AfterBackup.bat is to archive backup snapshots, you can create an AfterBackup.bat file to run additional tasks at the end of every backup operation.

## Supplemental backup tasks

The Backup Site Server maintenance task provides a backup snapshot for the site server files and site database. There are other items not backed up that you must consider when you create your backup strategy. Use these sections to help you complete your Configuration Manager backup strategy.

### Back up custom reports

If you modify predefined or created custom reports in SQL Server Reporting Services, create a backup for the report server database files. The report server backup must include the following components:

- The source files for reports and models
- Encryption keys
- Custom assemblies or extensions
- Configuration files
- Custom SQL Server views used in custom reports
- Custom stored procedures  

> [!IMPORTANT]
> When Configuration Manager updates to a newer version, the predefined reports might be overwritten by new reports. If you modify a predefined report, make sure to back up the report and then restore it in Reporting Services.

For more information about backing up your custom reports in Reporting Services, see [Backup and Restore Operations for Reporting Services](/sql/reporting-services/install-windows/backup-and-restore-operations-for-reporting-services).

### Back up content files

The content library in Configuration Manager is the location where all content files are stored for all software deployments. The content library is located on the site server and on each distribution point. The Backup Site Server maintenance task doesn't back up the content library or package source files. When a site server fails, the information about the content library is restored to the site database, but you must restore the content library and package source files.  

- The content library must be restored before you can redistribute content to distribution points. When you start content redistribution, Configuration Manager copies the files from the site server's content library to the distribution points. For more information, see [The content library](../../plan-design/hierarchy/the-content-library.md).

- The package source files must be restored before you can update content on distribution points. When you start a content update, Configuration Manager copies new or modified files from the package source to the content library. It then copies the files to associated distribution points. Run the following SQL query against the site database to find the package source location for all packages and applications: `SELECT * FROM v_Package`. You can identify the package source site by looking at the first three characters of the package ID. For example, if the package ID is CEN00001, the site code for the source site is CEN. When you restore the package source files, they must be restored to the same location where they were before the failure.

Verify that you include both the content library and package source files in your file system backup for the site server.

### Back up custom software updates

System Center Updates Publisher is a stand-alone tool that lets you manage custom software updates. Updates Publisher uses a local database for its software update repository. When you use Updates Publisher to manage custom software updates, determine whether you should include the Updates Publisher database in your backup plan. For more information, see [System Center Updates Publisher](../../../sum/tools/updates-publisher.md).

Use the following procedure to back up the Updates Publisher database.

#### Back up the Updates Publisher database

1. On the computer that runs Updates Publisher, browse to the Updates Publisher database file **Scupdb.sdf** in `%USERPROFILE%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\`. There's a different database file for each user that runs Updates Publisher.

1. Copy the database file to your backup destination. For example, if your backup destination is `E:\ConfigMgr_Backup`, you could copy the Updates Publisher database file to `E:\ConfigMgr_Backup\SCUP`.

    > [!TIP]
    > When there's more than one database file on a computer, consider storing the file in a subfolder that indicates the user profile associated with the database file. For example, you could have one database file in `E:\ConfigMgr_Backup\SCUP\User1` and another database file in `E:\ConfigMgr_Backup\SCUP\User2`.

## User state migration data

You can use Configuration Manager task sequences to capture and restore the user state data in OS deployment scenarios. The properties of the state migration point list the folders that store the user state data. This data isn't backed up as part of the Site Server Backup maintenance task. As part of your backup plan, you must manually back up the folders that you specify to store the user state migration data.

### Determine the folders used to store user state migration data

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Servers and Site System Roles** node.

1. Select the site system that hosts the state migration role. Then select **State migration point** in the **Site System Roles** pane.

1. Select **Properties** in the ribbon.

1. The folders that store the user state migration data are listed in the **Folder details** section on the **General** tab.

## About the SMS Writer service

The SMS Writer is a service that interacts with the Windows Volume Shadow Copy Service (VSS) during the backup process. The SMS Writer service must be running for the Configuration Manager site back up to complete successfully.

### Process

1. SMS Writer registers with the VSS service and binds to its interfaces and events.

1. When VSS broadcasts events, or if it sends specific notifications to the SMS Writer, the SMS Writer responds to the notification and takes the appropriate action.

1. The SMS Writer reads the backup control file **smsbkup.ctl** located in `<ConfigMgrInstallationPath>\inboxes\smsbkup.box`, and determines the files and data to back up.

1. The SMS Writer builds metadata, which consists of various components including specific data from the SMS registry key and subkeys.

    1. It sends the metadata to VSS when it's requested.

    1. VSS then sends the metadata to the requesting application, the Configuration Manager Backup Manager.

1. Backup Manager selects the data to back up, and sends this data to the SMS Writer via VSS.

1. The SMS Writer takes the appropriate steps to prepare for the backup.

1. Later, when VSS is ready to take the snapshot:

    1. It sends an event

    1. The SMS Writer stops all Configuration Manager services

    1. It ensures that the Configuration Manager activities are frozen while the snapshot is created.

1. After the snapshot is complete, the SMS Writer restarts services and activities.

The SMS Writer service is installed automatically. It must be running when the VSS application requests a backup or restore.

### Writer ID

The writer ID for the SMS Writer is **03ba67dd-dc6d-4729-a038-251f7018463b**.

### Permissions

The SMS Writer service must run under the Local System account.

### Volume Shadow Copy service

The VSS is a set of COM APIs that implements a framework to allow volume backups to be performed while applications on a system continue to write to the volumes. The VSS provides a consistent interface that allows coordination between user applications that update data on disk (the SMS Writer service) and those that back up applications (the Backup Manager service). For more information, see the [Volume Shadow Copy Service](/windows-server/storage/file-server/volume-shadow-copy-service).

## Next steps

After you create a backup, practice [site recovery](recover-sites.md) with that backup. This practice can help you become familiar with the recovery process before you need to rely on it. It can also help confirm the backup was successful for its intended purpose.
