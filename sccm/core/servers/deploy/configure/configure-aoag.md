---
title: "Configure Availability Groups"
titleSuffix: "Configuration Manager"
description: "Set up and manage SQL Server Always On Availability groups with SCCM."
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid:  7e4ec207-bb49-401f-af1b-dd705ecb465d
caps.latest.revision: 0
author: mstewart
ms.author: mstewart
manager: angrobe

---
# Configure SQL Server Always On availability groups for Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Use the information in this topic to configure and manage the availability groups you use with Configuration Manager.

Before you start:  
-   Be familiar with the information from [Prepare to use SQL Server Always On availability groups with Configuration Manager](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).
-   Be familiar with SQL Server documentation that covers the use of availability groups and related procedures. That information is required to complete the following scenarios.

> [!TIP]  
>  Links from this topic for SQL Server go to content for SQL Server 2016. If you do not use that version of SQL Server, consult the documentation for the version you use.

## Create and configure an availability group
Use the following procedure to create an availability group and then move a copy of the site database to that availability group.

To complete this procedure, the account you use must be:
-   A member of the **Local Administrators** group on each computer that is in the availability group.
-   A **sysadmin** on each instance of SQL Server that hosts the site database.

### To create and configure an availability group for Configuration Manager  
1.	Use the following command to stop the Configuration Manager site:
**Preinst.exe /stopsite**. For more information about using Preinst.exe, see [Hierarchy Maintenance Tool](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe).

2.	Change the backup model for the site database from **SIMPLE** to **FULL**.
See [View or Change the Recovery Model of a Database](/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server) in the SQL Server documentation. (Availability groups only support FULL).

3.	Use SQL Server to create a full backup of your site database. Then, do one of the following, depending on whether the server that hosts your site database will be a replica member of the new availability group or not:
    -   **Will be member of your availability group:**  
        If you use this server as the initial primary replica member of the availability group, you do not need to restore a copy of the site database to this or another server in the group. The database will already be in place on the primary replica, and SQL Server will replicate the database to the secondary replicas during a later step.  

	  -    **Will not be a member of the availability group:**   
    Restore a copy of the site database to the server that will host the primary replica of the group.

    For information on how to complete this step, see [Create a Full Database Backup](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server) and [Restore a Database Backup using SSMS](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)in the SQL Server documentation.

4.	On the server that will host the initial primary replica of the group, use the [New Availability Group Wizard](/sql/database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio) to create the availability group. In the wizard:
	  -    On the **Select Database** page, select the database for your Configuration Manager site.  

	  -    On the **Specify Replicas** page, configure:
    	  -    **Replicas:** Specify the servers that will host secondary replicas.

    	  -    **Listener:** Specify the **Listener DNS Name** as a full DNS name,  like **&lt;Listener_Server>.fabrikam.com**. This is used when you configure Configuration Manager to use the database in the availability group.

	  -    On the **Select Initial Data Synchronization** page, select **Full**. After the wizard creates the availability group, the wizard will back up the primary database and transaction log. Then the wizard restores them on each server that hosts a secondary replica. (If you do not use this step, you will need to restore a copy of the site database to each server that hosts a secondary replica, and manually join that database to the group.)   

5.	Check the configuration on each replica:   
  1.	Ensure the computer account of the site server is a member of the **Local Administrators** group on each computer that is a member of the availability group.  

  2.  Run the [verification script](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#prerequisites) from the prerequisites to confirm that the site database on each replica is correctly configured.

  3.	If it’s necessary to set configurations on secondary replicas, you must manually failover the primary replica to the secondary replica before continuing. You can only configure the database of a primary replica. For more information, see [Perform a Planned Manual Failover of an Availability Group](/sql/database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server) in the SQL Server documentation.

6.	After all replicas meet the requirements, the availability group is ready to be used with Configuration Manager.

## Configure a site to use the database in the availability group
After you [create and configure the availability group](#create-and-configure-an-availability-group), use Configuration Manager site maintenance to configure the site to use the database that is hosted by the availability group.

It is not supported to install a new site with its database in an availability group. For example, if you use the baseline 1702 media, you must install the site using a single instance of SQL Server. After the site installs, you can then move the site database to the availability group.

To complete this procedure, the account you use to run Configuration Manager Setup must be:
-   A member of the **Local Administrators** group on each computer that is a member of the availability group.
-   A **sysadmin** on each instance of SQL Server that hosts the site database.

> [!IMPORTANT]
> When you use Microsoft Intune with Configuration Manager in a hybrid configuration, moving the site database to or from an availability group triggers a resynchronization of data with the cloud. This resynchronization cannot be avoided.

### To configure a site to use the availability group
1.	Run **Configuration Manager Setup** from **&lt;*Configuration Manager site installation folder*>\BIN\X64\setup.exe**.

2.	On the **Getting Started** page, select **Perform site maintenance or reset this site**, and then click **Next**.

3.	Select the **Modify SQL Server configuration** option, and then click **Next**.

4.	Reconfigure the following for the site database:
    -   **SQL Server name:** Enter the virtual name for the availability group **listener** that you configured when creating the availability group. The virtual name should be a full DNS name, like **&lt;*endpointServer*>.fabrikam.com**.  

    -   **Instance:** This value must be blank to specify the default instance for the *listener* of the availability group. If the current site database runs on a named instance, the named instance is listed and must be cleared.

    -   **Database:** Leave the name as it appears. This is the name of the current site database.

5.	After you provide the information for the new database location, complete Setup with your normal process and configurations.



## Add or remove synchronous replica members  
When your site database is hosted in an availability group, use the following procedures to add or remove synchronous replica members. For information about the type and number of replicas that are supported, see **Availability group configurations** under [Prerequisites](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#prerequisites) in the prepare to use availability group topic.

To complete the following procedures, the account you use must be:
-   A member of the **Local Administrators** group on each computer that is a member of the availability group.
-   A **sysadmin** on each SQL Server that hosts or will host the site database.


### To add a new synchronous replica member  
The process to add secondary replica to an availability group you use with Configuration Manager can be complex, dynamic, and require steps and procedures that change based on individual environments. We are working on improvements for Configuration Manager to simplify this process. In the meantime, if you need to add secondary replicas, refer to the following blog on TechNet for guidance
-   [ConfigMgr 1702: Adding a new node (Secondary Replica) to an existing SQL AO AG](https://blogs.technet.microsoft.com/umairkhan/2017/07/17/configmgr-1702-adding-a-new-node-secondary-replica-to-an-existing-sql-ao-ag/)

### To remove a replica member
For this procedure, use the information in [Remove a Secondary Replica from an Availability Group](/sql/database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server) from the SQL Server documentation.  


## Configure an asynchronous commit replica
Beginning with Configuration Manager version 1706, you can add an asynchronous replica to an availability group you use with Configuration Manager. To do so, you do not need to run the configuration scripts required to configure a synchronous replica. (This is because there is no support to use that asynchronous replica as the site database.) See the [SQL Server documentation](https://msdn.microsoft.com/library/hh213247(v=sql.120).aspx(d=robot))  for information on how to add secondary replicas to availability groups.

## Use the asynchronous replica to recover your site
With Configuration Manager version 1706 and later, you can use an asynchronous replica to recover your site database. To do so, you must stop the active primary site to prevent additional writes to the site database. After you stop the site, you can use an asynchronous replica in place of using a [manually recovered database](/sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption).

To stop the site, you can use the [hierarchy maintenance tool](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe) to stop key services on the site server. Use the command line: **Preinst.exe /stopsite**   

Stopping the site is equivalent to stopping the Site Component Manager service (sitecomp) followed by the SMS_Executive service, on the site server.

<!-- For inclusion with passive primary site support:
> [!TIP]  
> If you use a primary passive replica (introduced in version [TBD],  you do not need to stop the passive replica. Only the active primary site must be stopped.
-->  

## Stop using an availability group
Use the following procedure when you no longer want to host your site database in an availability group. This involves moving the site database back to a single instance of SQL Server.

To complete this procedure, the account you use must be:
-   A member of the **Local Administrators** group on each computer that is a member of the availability group
-   A **sysadmin** on each instance of SQL Server that hosts the site database.

> [!IMPORTANT]  
> When you use Microsoft Intune with Configuration Manager in a hybrid configuration, moving the site database to or from an availability group triggers a resynchronization of data with the cloud. This cannot be avoided.

### To move the site database from an availability group back to a single instance SQL Server
1.	Stop the Configuration Manager site by using the following command: **Preinst.exe /stopsite**. For more information, see [Hierarchy Maintenance Tool](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe).

2.	Use SQL Server to create a full backup of your site database from the primary replica. For information on how to complete this step, see [Create a Full Database Backup](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server) in the SQL Server documentation.

3.	If the server that is the primary replica for the availability group will host the single instance of the site database, you can skip this step:  

    -   Use SQL Server to restore the site database backup to the server that will host the site database. See [Restore a Database Backup using SSMS](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms) in the SQL Server documentation.   <br />  <br />

4.	On the server that will host the site database (the primary replica, or the server where you restored the site database), change the backup model for the site database from **FULL** to **SIMPLE**. See [View or Change the Recovery Model of a Database](/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server) in the SQL Server documentation.  

5.	Run **Configuration Manager Setup** from **&lt;*Configuration Manager site installation folder>*\BIN\X64\setup.exe**.

6.	On the **Getting Started** page, select **Perform site maintenance or reset this site**, and then click **Next**.  

7.	Select the **Modify SQL Server configuration** option, and then click **Next**.  

8.	Reconfigure the following for the site database:
    -   **SQL Server name:** Enter the name of the server that now hosts the site database.

    -   **Instance:** Specify the named instance that hosts the site database, or leave this blank if the database is on the default instance.

    -   **Database:** Leave the name as it appears. This is the name of the current site database.    

9.	After you provide the information for the new database location, complete Setup with your normal process and configurations. When Setup completes, the site restarts and begins to use the new database location.    

10.	To clean up the servers that were members of the availability group, follow the guidance in [Remove an Availability Group](/sql/database-engine/availability-groups/windows/remove-an-availability-group-sql-server) in the SQL Server documentation.
