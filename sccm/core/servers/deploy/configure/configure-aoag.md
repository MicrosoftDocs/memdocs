---
title: Configure availability groups
titleSuffix: Configuration Manager
description: Set up and manage SQL Server Always On availability groups with Configuration Manager
ms.date: 09/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7e4ec207-bb49-401f-af1b-dd705ecb465d
author: mestew
ms.author: mstewart
manager: dougeby


---

# Configure SQL Server Always On availability groups for Configuration Manager

*Applies to: Configuration Manager (current branch)*

Use the information in this article to configure and manage the availability groups you use with Configuration Manager.

Before you start:  

- Be familiar with the information from [Prepare to use SQL Server Always On availability groups with Configuration Manager](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).
- Be familiar with SQL Server documentation that covers the use of availability groups and related procedures. That information is required to complete the following scenarios.


## <a name="bkmk_create"></a> Create and configure an availability group

Use the following procedure to create an availability group and then move a copy of the site database to that availability group.

1. Use the following command to stop the Configuration Manager site:

    `preinst.exe /stopsite`

    For more information, see [Hierarchy maintenance tool](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe).

2. Change the backup model for the site database from **SIMPLE** to **FULL**:

    ```sql
    ALTER DATABASE [CM_xxx] SET RECOVERY FULL;
    ```

    Availability groups only support the FULL backup model. For more information, see [View or change the recovery model of a database](https://docs.microsoft.com/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server).

3. Use SQL Server to create a full backup of your site database. Choose one of the following options:

    - **Will be member of your availability group**: If you use this server as the initial primary replica member of the availability group, you don't need to restore a copy of the site database to this server or another in the group. The database is already in place on the primary replica. SQL Server replicates the database to the secondary replicas during a later step.  

    - **Will not be a member of the availability group**: Restore a copy of the site database to the server that will host the primary replica of the group.

    For more information, see the following articles in the SQL Server documentation:

    - [Create a full database backup](https://docs.microsoft.com/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server)
    - [Restore a database backup using SSMS](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)

    > [!NOTE]  
    > If you plan to move from an availability group to standalone on an existing replica, first remove the database from the availability group.

4. On the server that will host the initial primary replica of the group, use the [New availability group wizard](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio) to create the availability group. In the wizard:

    - On the **Select Database** page, select the database for your Configuration Manager site.  

    - On the **Specify Replicas** page, configure:

        - **Replicas:** Specify the servers that will host secondary replicas.

        - **Listener:** Specify the **Listener DNS Name** as a full DNS name, for example `<listener_server>.fabrikam.com`. When you configure Configuration Manager to use the database in the availability group, it uses this name.

    - On the **Select Initial Data Synchronization** page, select **Full**. After the wizard creates the availability group, the wizard backs up the primary database and transaction log. Then the wizard restores them on each server that hosts a secondary replica.

        > [!Note]  
        > If you don't use this step, restore a copy of the site database to each server that hosts a secondary replica. Then manually join that database to the group.

5. Check the configuration on each replica:

    1. Make sure the computer account of the site server is a member of the local **Administrators** group on each computer that's a member of the availability group.  

    2. Run the [verification script](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#prerequisites) to confirm that the site database on each replica is correctly configured.

    3. If it's necessary to set configurations on secondary replicas, before you continue, manually fail over the primary replica to the secondary replica. You can only configure the database of a primary replica. For more information, see [Perform a planned manual failover of an availability group](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server) in the SQL Server documentation.

6. After all replicas meet the requirements, the availability group is ready to be used with Configuration Manager.


## <a name="bkmk_configure"></a> Configure a site to use the availability group

After you [create and configure the availability group](#bkmk_create), use Configuration Manager site maintenance to configure the site to use the database that the availability group hosts.

It's not supported to install a new site with its database in an availability group. For example, if you use baseline media, install the site using a single instance of SQL Server. After the site installs, then move the site database to the availability group.

1. Run **Configuration Manager Setup**: `\BIN\X64\setup.exe` from the Configuration Manager site installation folder.

2. On the **Getting Started** page, select **Perform site maintenance or reset this site**, and then select **Next**.

3. Select **Modify SQL Server configuration**, and then select **Next**.

4. Reconfigure the following settings for the site database:

    - **SQL Server name**: Enter the virtual name for the availability group *listener*. You configured the listener when you created the availability group. The virtual name should be a full DNS name, like `<Listener_Server>.fabrikam.com`.  

    - **Instance:** To specify the default instance for the *listener* of the availability group, this value must be blank. If the current site database runs on a named instance, clear the current named instance.

    - **Database:** Leave the name as it appears. This name is the current site database.

5. After you provide the information for the new database location, complete setup with your normal process and configurations.


## <a name="bkmk_sync"></a> Synchronous replica members  

When your site database is hosted in an availability group, use the following procedures to add or remove synchronous replica members. For more information about the supported type and number of replicas, see [Availability group configurations](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#availability-group-configurations).

### <a name="bkmk_sync-add"></a> Add a new synchronous replica member

<!--3127336-->
Starting in version 1906, run Configuration Manager setup to add a new synchronous replica member.

1. Add a secondary replica using the SQL Server procedures.

    1. [Add a secondary replica to an Always On Availability Group](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server).

    1. Watch the status in SQL Management Studio. Wait for the availability group to return to full health.

1. Run Configuration Manager setup, and select the option to modify the site.

1. Specify the availability group listener name as the database name. If the listener uses a non-standard network port, specify that as well. This action causes setup to make sure each node is appropriately configured. It also starts a database recovery process.

Configuration Manager setup uses the SQL database move operation, and makes sure the nodes are correctly configured.

For more information on how to do this process manually in version 1902 or earlier, see [ConfigMgr 1702: Adding a new node (Secondary Replica) to an existing SQL AO AG](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-1702-adding-a-new-node-secondary-replica-to-an/ba-p/339960).

### Remove a replica member

Starting in version 1906, you can use Configuration Manager setup to remove a replica member. Use the same process to [Add a new synchronous replica member](#bkmk_sync-add).

For more information on how to do this process manually in version 1902 or earlier, see [Remove a secondary replica from an availability group](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server).  


## <a name="bkmk_async"></a> Asynchronous replicas

You can use an asynchronous replica in the availability group that you use with Configuration Manager. You don't need to run the configuration scripts required to configure a synchronous replica, because an asynchronous replica isn't supported for the site database.

### Configure an asynchronous commit replica

For more information, see [Add a secondary replica to an availability group](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server).

### Use the asynchronous replica to recover your site

Use the asynchronous replica to recover your site database.

1. Stop the active primary site to prevent additional writes to the site database. To stop the site, use the [Hierarchy maintenance tool](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe): `preinst.exe /stopsite`

1. After you stop the site, use the asynchronous replica instead of a [manually recovered database](/sccm/core/servers/manage/recover-sites#use-a-site-database-that-has-been-manually-recovered).


## <a name="bkmk_stop"></a> Stop using an availability group

Use the following procedure when you no longer want to host your site database in an availability group. With this process, you'll move the site database back to a single instance of SQL Server.

1. Stop the Configuration Manager site by using the following command: `preinst.exe /stopsite`. For more information, see [Hierarchy maintenance tool](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe).

2. Use SQL Server to create a full backup of your site database from the primary replica. For more information, see [Create a full database backup](https://docs.microsoft.com/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server).

3. Use SQL Server to restore the site database backup to the server that will host the site database. For more information, see [Restore a database backup using SSMS](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms).

    > [!Note]  
    > If the primary replica server for the availability group will host the single instance of the site database, skip this step.

4. On the server that will host the site database, change the backup model for the site database from **FULL** to **SIMPLE**. For more information, see [View or change the recovery model of a database](https://docs.microsoft.com/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server).

5. Run **Configuration Manager Setup**: `\BIN\X64\setup.exe` from the Configuration Manager site installation folder.

6. On the **Getting Started** page, select **Perform site maintenance or reset this site**, and then select **Next**.  

7. Select **Modify SQL Server configuration**, and then select **Next**.  

8. Reconfigure the following settings for the site database:

    - **SQL Server name:** Enter the name of the server that now hosts the site database.

    - **Instance:** Specify the named instance that hosts the site database. If the database is on the default instance, leave this field blank.

    - **Database:** Leave the name as it appears. This name is the current site database.

9. After you provide the information for the new database location, complete setup with your normal process and configurations. When setup completes, the site restarts, and begins to use the new database location.

10. To clean up the servers that were members of the availability group, follow the guidance in [Remove an availability group](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/remove-an-availability-group-sql-server).
