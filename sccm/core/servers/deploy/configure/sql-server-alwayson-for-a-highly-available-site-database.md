---
title: "SQL Server AlwaysOn | System Center Configuration Manager"
ms.custom: na
ms.date: 08/04/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
caps.latest.revision: 16
author: Brendunsms.author: brendunsmanager: angrobe

---
# SQL Server AlwaysOn for a highly available site database for System Center Configuration Manager


 Beginning with System Center Configuration Manager version 1602, you can use  SQL Server [AlwaysOn Availability Groups](https://msdn.microsoft.com/library/hh510230\(v=sql.120\).aspx) to host the site database at primary sites and the central administration site as a high-availability and disaster-recovery solution. The availability group can be hosted on-premises or in Microsoft Azure.  

 When you use Microsoft Azure to host the availability group, you can further increase availability of your site database by using SQL Server AlwaysOn Availability Groups with Azure Availability Sets. For more information on Azure Availability Sets, see [Manage the availability of virtual machines](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-manage-availability/).  

 The following are scenarios that are supported with availability groups:  

-   You can move your site database to the default instance of an availability group  

-   You can add or remove replica members from an availability group that hosts a site database  

-   You can move your site database from an availability group to a default or named instance of a standalone SQL Server  


> [!NOTE]  
>  Successful configuration and use of availability groups requires you to be comfortable with configuring SQL Server and SQL Server availability groups. The procedures for System Center Configuration Manager in this topic rely on additional documentation and procedures found in the SQL Server documentation library.  

 **Known issues when you use AlwaysOn availability groups with Configuration Manager:**  

-   **All replica servers require an identical file path at the time you set Configuration Manager to use the availability group:**  

    -   At the time you run Configuration Manager Setup to redirect the site to use the database in an availability group, each secondary replica server in the group must have a file path that is identical to the file path used to host the site database files on the current primary replica. If an identical path does not exist on secondary replicas, Setup will fail to add the availability groups instance as the new location of the site database.  

         Additionally, on each secondary replica server, the local SQL Server service account must have **Full Control** permission to this folder.  

         The secondary replica servers only require this file path while you are using Setup to specify the database instance in the availability group.  After Setup completes the change to use the site database in the availability group, you can delete the unused path from secondary replica severs.  

         For example, consider the following scenario:  

        -   You create an availability group that uses three SQL Servers  

        -   Your primary replica server is a new installation of SQL Server 2014.  By default, the database .MDF and .LDF files are stored in C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA  

        -   Both of your secondary replica servers were upgraded to SQL Server 2014 from previous versions, and retain the original file path to store database files of: C:\Program Files\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\DATA  

        -   Before you attempt to move the site database to this availability group, on each secondary replica server you must create the following file path even if the secondary replicas will not use this file location:  C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA (this is a duplicate of the path that is in use on the primary replica)  

        -   You then grant the SQL Server service account on each secondary replica full control access to the newly created file location on that server  

        -   You can now successfully run Configuration Manager Setup to direct the site to use the site database in the availability group  

-   **When Setup runs to direct the site database to use the availability group, errors similar to the following might be logged in ConfigMgrSetup.log:**  

    -   ERROR: SQL Server error: [25000][3906][Microsoft][SQL Server Native Client 11.0][SQL Server]Failed to update database "CM_AAA" because the database is read-only.   Configuration Manager Setup 1/21/2016 4:54:59 PM  7344 (0x1CB0)  

     These errors are logged when  Setup tries to process  database roles on secondary replicas of the availability group. These  errors can be safely ignored.
- **SQL servers that host additional availability groups:**

  Prior to installing version 1610, when you use an availability group and then run Configuration Manager setup or install an update for Configuration Manager, each replica in each additional availability group on the SQL Server that hosts the Configuration Manager availability group must have the following configurations:
    - **Manual Failover**
    - **allow any read-only connection**


##  <a name="bkmk_BnR"></a> Changes for Backup and Recovery when you use a SQL Server AlwaysOn availability group  
 **Backup:**  

 When a site database runs in an availability group, you should continue to run the built-in **Backup Site** server maintenance task to backup common Configuration Manager settings and files, but plan to not use the .MDF or .LDF files created by that backup. Instead, plan to make direct backups of the site database by using SQL Server.  

 Additionally, because the recovery model of the database is set to full, you must plan to monitor and maintain the size of the site database transaction log.  In the full recovery model, the transactions are not hardened until a full backup of the database or transaction log is made. A recovery model of full is a requirement of using the site database in an availability group and set when you configure the group for use with Configuration Manager. For more information about  SQL Server backup and restore, see [Back Up and Restore of SQL Server Databases](https://msdn.microsoft.com/library/ms187048\(v=sql.120\).aspx) in the SQL Server documentation.  

 **Recovery:**  

 During a site recovery, so long as one node of the availability group remains functional, you can use the site recovery option **Skip database recovery (Use this option if the site database was unaffected)**.  

 However, if all nodes of an availability group have been lost, before you can recover the site, you must recreate the availability group (System Center Configuration Manager cannot rebuild or restore the availability node.)  After the group has been recreated with a backup restored and reconfigured, you can then use the site recovery option **Skip database recovery (Use this option if the site database was unaffected)**.  

 For more information about backup and recovery, see [Backup and recovery for System Center Configuration Manager](../../../../protect/understand/backup-and-recovery.md).  

##  <a name="bkmk_create"></a> Configure an availability group for use with Configuration Manager  
 Before you start the following procedure, be familiar with the SQL Server procedures necessary to complete this configuration, and the following details that apply to availability groups you configure for use with  Configuration Manager.  

 **Requirements for AlwaysOn availability groups you use with System Center Configuration Manager:**  

-   Each node (or replica) in the availability group must run a version of SQL Server supported by System Center Configuration Manager  

-   The availability group must have one primary replica, and can have up to two synchronous secondary replicas  

-  After you add a database to an availability group, you must failover the primary replica to a secondary (making it the new primary replica), and then configure the database with the following:
    - Enable Trustworthy: equal to True
    - Enable the Service Broker: equal to True
    - Set the dbowner: equal to SA

    You can run the following script to configure these settings, where cm_ABC  is the name of your site database:  

    >     USE master  
    >     ALTER DATABASE cm_ABC SET NEW_BROKER   
    >     ALTER DATABASE cm_ABC SET ENABLE_BROKER  
    >     ALTER DATABASE cm_ABC SET TRUSTWORTHY ON;  
    >     USE cm_ABC  
    >     EXEC sp_changedbowner 'sa'  
    >     Exec sp_configure 'max text repl size (B)', 2147483647
    >     reconfigure



-   The availability group must have at least one **availability group listener**.  The virtual name of this listener is used when you configure Configuration Manager to use the site database in the availability group. Although an availability group can contain multiple listeners, Configuration Manager can only make use of one  

-   Each primary and secondary replica must:  
    - Be set to **allow any read-only connection**
    - Use the **default instance**
    - Be set for **Manual Failover**  

        > [!TIP]  
        >  System Center Configuration Manager supports using the availability group replicas when set to Automatic Failover. However, Manual Failover must be set when you run Setup to specify use of the site database in the availability group, and at the time you install any updates to Configuration Manager (not just updates that apply to the site database).  

  **LImitations for availability groups**
   - Availability groups are supported only for the site database, and not for the software update database or reporting database   
   - When you use an availability group, you must manually configure your reporting point to use the current primary replica, and not the availability group listener. If the primary replica fails over to another replica, you must then reconfigure the reporting point to use the new primary replica.  
   - Before installing updates, like version 1606, ensure the availability group is set to manual failover. After the site updates, you can restore failover to be automatic.



 **Required permissions to configure and use availability groups:**  

-   The computer account of the site server must be a member of the **Local Administrators** group on each computer that is a member of the availability group.  

#### To configure an availability group to host a site database  

1.  Use the following command to stop the Configuration Manager site:  
     **Preinst.exe /stopsite**  

     For more information about using Preinst.exe, see [Hierarchy Maintenance Tool (Preinst.exe) for System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

2.  Change the backup model for the site database from **SIMPLE** to **FULL**.  

     See [View or Change the Recovery Model of a Database](https://msdn.microsoft.com/library/ms189272\(v=sql.120\).aspx) in the SQL Server documentation. (Availability groups only support FULL).  

3.  Use SQL Server to create a full backup of your site database, and then:  

    -   If your current site database server will not be a member of the availability group, or will not be used as the initial primary replica for the availability group, restore a copy of the site database to the server that will host the primary replica of the group.  

    -   If the current site database server will be member of your availability group, plan to use this server as the primary replica member of the availability group. When you do so, you do not need to restore a copy of the site database to this, or another server.  

    For information on how to complete this step, see [Create a Full Database Backup](https://msdn.microsoft.com/library/ms187510\(v=sql.120\).aspx) and [Restore a Database Backup (SQL Server Management Studio)](https://msdn.microsoft.com/library/ms177429\(v=sql.120\).aspx)in the SQL Server documentation.  

4.  On the server that will host the primary replica of the group, use the **New Availability Group Wizard** to create the availability group. In the wizard:  

    -   On the **Select Database** page, select the database for you Configuration Manager site  

    -   On the **Specify Replicas** page, configure:  

        -   **Replicas**: Specify the servers that will host secondary replicas  

        -   **Listener**: Specify the **Listener DNS Name** as a full DNS name, like **&lt;Listener_Server>.fabrikam.com**. This is used when you configure Configuration Manager to use the database in the availability group.

    -   On the **Select Initial Data Synchronization** page, select **Full**. After the wizard creates the availability group, the wizard will backup the primary database and transaction log, and restore them on each server that hosts a secondary replica. If you do not use this step, you will need to restore a copy of the site database to each server that hosts a secondary replica, and manually join that database to the group.  

    For more information, see [Use the Availability Group Wizard](https://msdn.microsoft.com/library/hh403415\(v=sql.120\).aspx) in the SQL Server documentation.  

5.  After the availability group is configured, configure the site database on the primary replica with the **TRUSTWORTHY** property, and then **enable CLR integration**. For information on how to configure these, see [TRUSTWORTHY Database Property](https://msdn.microsoft.com/library/ms187861\(v=sql.120\).aspx) and  [Enabling CLR Integration](https://msdn.microsoft.com/library/ms131048\(v=sql.120\).aspx) in the SQL Server documentation.  

6.  Take the following actions to configure each secondary replica in the availability group:  

    1.  Manually failover the current primary replica to a secondary replica. See [Perform a Planned Manual Failover of an Availability Group](https://msdn.microsoft.com/library/hh231018\(v=sql.120\).aspx) in the SQL Server documentation.  

    2.  Configure the database on the new primary replica with the **TRUSTWORTHY** property, and then **enable CLR integration**.  

7.  After all replicas are promoted to primary replicas and the databases configured, the availability group is ready to be used with Configuration Manager.  





##  <a name="bkmk_direct"></a> Move a site database to an availability group  
 You can move a site database for a previously installed site to an availability group. You must first create the availability group and then configure the database for operation in the availability group.  

 To complete this procedure, the user account that runs Configuration Manager Setup must be a member of the **Local Administrators** group on each computer that is a member of the availability group.  

#### To move a site database to an availability group  

1.  Run **Configuration Manager Setup** from **&lt;Configuration Manager site installation folder\>\BIN\X64\setup.exe**.  

2.  On the **Getting Started** page, select **Perform site maintenance or reset this site**, and then click **Next**.  

3.  Select the **Modify SQL Server configuration** option, and then click **Next**.  

4.  Reconfigure the following for the site database:  

    -   **SQL Server name:** Enter the virtual name for the availability group listener that you configured when creating the availability group. The virtual name should be a full DNS name, like **&lt;endpointServer\>.fabrikam.com**  

    -   **Instance:** This value must be blank to specify the default instance for the availability group listener of the availability group.  If the current site database is installed on a named instance, the named instance will be listed and must be cleared  

    -   **Database:** Leave the name as it appears. This is the name of the current site database.  

5.  After you provide the information for the new database location, complete Setup with your normal process and configurations.  

##  <a name="bkmk_change"></a> Add or remove members of an active availability group  
 After Configuration Manager is using a site database hosted in an availability group you can remove a replica member or add an additional replica member (not to exceed one primary and two secondary nodes).  

#### To add a new replica member  

1.  Add the new server as a secondary replica to the availability group. See  [Add a Secondary Replica to an Availability Group (SQL Server)](https://msdn.microsoft.com/library/hh213247\(v=sql.120\).aspx)in the SQL Server documentation library.  

2.  Stop the Configuration Manager site by running **Preinst.exe /stopsite** See [Hierarchy Maintenance Tool (Preinst.exe) for System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

3.  Use SQL Server to create a backup of the site database from the primary replica, and then restore that backup to the new secondary replica server. See [Create a Full Database Backup](https://msdn.microsoft.com/library/ms187510\(v=sql.120\).aspx) and See [Restore a Database Backup (SQL Server Management Studio)](https://msdn.microsoft.com/library/ms177429\(v=sql.120\).aspx) in the SQL Server documentation library.  

4.  Configure each secondary replica. Perform the following actions for each secondary replica in the availability group:  

    1.  Manually failover the primary replica to the new secondary replica. See [Perform a Planned Manual Failover of an Availability Group](https://msdn.microsoft.com/library/hh231018\(v=sql.120\).aspx) in the SQL Server documentation.  

    2.  Configure the database on the new server to be Trustworthy, and enable CLR integration. See [TRUSTWORTHY Database Property](https://msdn.microsoft.com/library/ms187861\(v=sql.120\).aspx) and  [Enabling CLR Integration](https://msdn.microsoft.com/library/ms131048\(v=sql.120\).aspx)in the SQL Server documentation.  

5.  Restart the site by starting the Site Component Manager (**sitecomp**) and **SMS_Executive** services.  

#### To remove a replica member from the availability group  

-   Use the information in [Remove a Secondary Replica from an Availability Group](https://msdn.microsoft.com/library/hh213149\(v=sql.120\).aspx) from the SQL Server documentation.  

##  <a name="bkmk_remove"></a> Move the site database from an availability group back to a single instance SQL Server  
 Use the following procedure when you no longer want to host your site database in an availability group.  

#### To move the site database from an availability group back to a single instance SQL Server  

1.  Stop the Configuration Manager site by using the following command:  
     **Preinst.exe /stopsite**.  For more information, see [Hierarchy Maintenance Tool (Preinst.exe) for System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

2.  Use SQL Server to create a full backup of your site database from the primary replica. For information on how to complete this step, see [Create a Full Database Backup](https://msdn.microsoft.com/library/ms187510\(v=sql.120\).aspx) in the SQL Server documentation.  

3.  If the server that hosts the primary replica for the availability group will now host the single instance of the site database, you can skip this step:  

    -   Use SQL Server to restore the site database backup to the server that will host the site database.  See [Restore a Database Backup (SQL Server Management Studio)](https://msdn.microsoft.com/library/ms177429\(v=sql.120\).aspx) in the SQL Server documentation.  

4.  On the restored site database, change the backup model for the site database from **FULL** to **SIMPLE**.  See [View or Change the Recovery Model of a Database](https://msdn.microsoft.com/library/ms189272\(v=sql.120\).aspx) in the SQL Server documentation.  

5.  Run **Configuration Manager Setup** from **&lt;Configuration Manager site installation folder\>\BIN\X64\setup.exe**.  

6.  On the **Getting Started** page, select **Perform site maintenance or reset this site**, and then click **Next**.  

7.  Select the **Modify SQL Server configuration** option, and then click **Next**.  

8.  Reconfigure the following for the site database:  

    -   **SQL Server name:** Enter the name of the server that now hosts the site database.  

    -   **Instance:** Specify the named instance that hosts the site database, or leave this blank if the database is on the default instance.  

    -   **Database:** Leave the name as it appears. This is the name of the current site database.  

9. After you provide the information for the new database location, complete Setup with your normal process and configurations. When Setup completes, the site restarts and begins to use the new database location.  

10. To clean up the servers that were members of the availability group, follow the guidance in [Remove an Availability Group](https://msdn.microsoft.com/library/ff878113\(v=sql.120\).aspx) in the SQL Server documentation.
