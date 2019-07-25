---
title: Data transfers
titleSuffix: Configuration Manager
description: Learn how Configuration Manager moves data between sites, and how you can manage the transfer of the data across your network.
ms.date: 07/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: dc526e8d-fac3-4bb5-b206-03ad29b0ae11
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
---

# Data transfers between sites in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Configuration Manager uses *file-based replication* and *database replication* to transfer different types of information between sites. Learn about how Configuration Manager moves data between sites, and how you can manage the transfer of data across your network.  


## <a name="bkmk_fileroute"></a> File-based replication

Configuration Manager uses file-based replication to transfer file-based data between sites in your hierarchy. This data includes applications and packages that you want to deploy to distribution points in child sites. It also includes unprocessed discovery data records that are transferred to parent sites and then processed.  

File-based communication between sites uses the *server message block** (SMB) protocol on TCP/IP port 445. To control the amount of data transferred across the network, specify bandwidth throttling and pulse mode. You can also use schedules to control when to send data across the network.  

### <a name="bkmk_routes"></a> File replication routes

The following information can help you set up and use file replication routes.  

#### File replication route

Each file replication route identifies a destination site to which file-based data can transfer. Each site supports one file replication route to a specific destination site.  

To manage a file replication route, in the **Administration** workspace, expand **Hierarchy Configuration**, and then select the **File Replication** node.  

You can change the following settings for file replication routes:  

##### File Replication Account

This account connects to the destination site, and writes data to that site's **SMS_Site** share. The receiving site processes the data written to this share. By default, when you add a site to the hierarchy, Configuration Manager assigns the new site server's computer account as its file replication account. It then adds this account to the destination site's **SMS_SiteToSiteConnection_&lt;Sitecode\>** group. This group is local on the computer that grants access to the SMS_Site share. You can change this account to be a Windows user account. If you change the account, make sure you add it to the destination site's **SMS_SiteToSiteConnection_&lt;Sitecode\>** group.  

> [!NOTE]  
> Secondary sites always use the computer account of the secondary site server as the **File Replication Account**.  

##### Schedule

To restrict the type of data and time when data can transfer to the destination site, set the schedule for each file replication route.

##### Rate limits

To control the network bandwidth that the site uses when it transfers data to the destination site, specify rate limits for each file replication route:

- **Pulse mode**: Specify the size of the data blocks that the site sends to the destination site. You also can specify a time delay between sending each data block. Use this option when you must send data across a low-bandwidth network connection to the destination site.

    For example, you have constraints to send 1 KB of data every five seconds, but not 1 KB every three seconds, whatever of the speed of the link or its usage at a given time.

- **Limited to maximum transfer rates by hour**: The site sends data to a destination site by using only the percentage of time that you specify. When you use this option, Configuration Manager doesn't identify the network's available bandwidth. Instead, it divides the time it can send data into slices of time. It then sends data in a short block of time, which is followed by blocks of time when it doesn't send data.

    For example, you set the maximum rate to **50%**. Configuration Manager transmits data for an amount of time followed by an equal period of time when it doesn't send any data. It doesn't manage the actual size amount of data, or the size of the data block. It only manages the amount of time during which it sends data.  

    > [!CAUTION]  
    > By default, a site can use up to three **concurrent sendings** to transfer data to a destination site. When you enable rate limits for a file replication route, it limits the **concurrent sendings** to that site to one. This behvaior applies even when the **Limit available bandwidth (%)** is set to **100%**. For example, if you use the default settings for the sender, this reduces the transfer rate to the destination site to be one-third of the default capacity.  

##### Secondary sites

You can configure a file replication route between two secondary sites to route file-based content between those sites.  


#### Sender

Each site has one sender. The sender manages the network connection from one site to a destination site, and can establish connections to multiple sites at the same time. To connect to a site, the sender uses the file replication route to the site to identify the account to use to establish the network connection. The sender also uses this account to write data to the destination site's SMS_Site share.  

By default, the sender writes data to a destination site by using multiple **concurrent sendings**, typically referred to as a thread. Each concurrent sending, or thread, can transfer a different file-based object to the destination site. By default, when the sender begins to send an object, the sender continues to write blocks of data for that object until the entire object is sent. After all the data for the object has been sent, a new object can begin to send on that thread.  

To manage the sender for a site, go to the **Administration** workspace, and expand the **Site Configuration** node. Select the **Sites** node, and then select **Properties** for the site you want to manage. Switch to the **Sender** tab to change the sender settings.  

You can change the following settings for a sender:  

##### Maximum concurrent sendings

By default, each site uses five concurrent sendings. Three threads are available for use when it sends data to any one destination site. When you increase this number, you can increase the throughput of data between sites because Configuration Manager can transfer more files at the same time. Increasing this number also increases the demand for network bandwidth between sites.  

##### Retry settings

By default, each site retries a problem connection two times, with a one-minute delay between connection attempts. You can modify the number of connection attempts the site makes, and how long to wait between attempts.  


## <a name="bkmk_dbrep"></a> Database replication

Configuration Manager database replication uses SQL Server to transfer data, and to merge changes that are made in a site database with the information stored in the database at other sites in the hierarchy.

In a hierarchy:

- All sites share the same information.  
- When you install a site in a hierarchy, Configuration Manager automatically establishes database replication between the new site and its parent site.  
- When the site installation finishes, database replication automatically starts.  

When you add a new site to a hierarchy, Configuration Manager creates a generic database at the new site. Next, the parent site creates a snapshot of the relevant data in its database, and then transfers the snapshot to the new site by file-based replication. The new site then uses the SQL Server Bulk Copy Program (BCP) to load the information into its local copy of the Configuration Manager database. After the snapshot loads, each site conducts database replication with the other site.  

To replicate data between sites, Configuration Manager uses its own database replication service. The database replication service uses SQL Server change tracking to monitor the local site database for changes. It then replicates the changes to other sites by using SQL Server Service Broker (SSB). By default, this process uses TCP/IP port 4022.  

### Replication groups

Configuration Manager groups data that replicates by database replication into different replication groups. Each replication group has a separate, fixed replication schedule. The site uses this schedule to determine how frequently it replicates changes to other sites.  

For example, a change to a role-based administration configuration replicates quickly to other sites. This behavior makes sure that other sites can quickly enforce these changes. A lower-priority configuration change, such as a request to install a new secondary site, replicates with less urgency. It can take several minutes for a new site request to reach the destination primary site.  

### Settings for database replication

You can modify the following settings for database replication:  

- **Database replication links**: Control when specific traffic traverses the network.  

- **Distributed views**: When a central administration site (CAS) requests selected site data, it can access the data directly from the database at a child primary site.  

- **Schedules**: Specify when a replication link is used, and when different types of site data replicate.  

- **Summarization**: Settings for data summarization about network traffic that traverses replication links. By default, summarization occurs every 15 minutes. It's used in reports for database replication.  

- **Database replication thresholds**: Define when Configuration Manager reports links as degraded or failed. You also can configure when it raises alerts about replication links that have a degraded or failed status.  

### Types of data

Configuration Manager primarily classifies the data that it replicates as either *global data* or *site data*. When database replication occurs, the site transfers changes to global and site data across the database replication link. Global data replicates to a parent or child site. Site data replicates only to a parent site. A third data type, *local data*, doesn't replicate to other sites. Local data is information that other sites don't require.

#### Global data

Global data is administrator-created objects that replicate to all sites throughout the hierarchy. Secondary sites only receive a subset of global data, as global proxy data. You create global data at the CAS and primary sites. This type includes the following data:

- Software deployments
- Software updates
- Collection definitions
- Role-based administration security scopes

#### Site data

Site data is operational information created by Configuration Manager primary sites and their assigned clients. Site data replicates to the CAS, but not to other primary sites. Site data is only viewable at the CAS, and at the primary site where the data originates. You can only modify site data at the primary site where you created it. This type includes the following data:

- Hardware inventory
- Status messages
- Alerts
- The results of query-based collections

All site data replicates to the CAS. The CAS does administration and reporting for the entire site hierarchy.  

### <a name="bkmk_Dblinks"></a> Database replication links

When you install a new site in a hierarchy, Configuration Manager automatically creates a database replication link between the parent site and the new site. It creates a single link to connect the two sites.  

To help you control the transfer of data across the database replication link, change settings for each link. Each replication link supports separate configurations. Each database replication link includes the following controls:  

- Stop the replication of selected site data from a primary site to the CAS. Then the CAS can access this data directly from the database of the primary site.  
- Schedule selected site data to transfer from a child primary site to the CAS.
- Define the settings that determine when a database replication link has a degraded or failed status.
- Specify when to raise alerts for a failed replication link.
- Specify how frequently Configuration Manager summarizes data about the replication traffic that uses the replication link. This data is used in reports.

To configure a database replication link, in the Configuration Manager console, on the **Database Replication** node, open the **Properties** for the link. This node appears both in the **Monitoring** workspace, and in the **Administration** workspace on the **Hierarchy Configuration** node. You can edit a replication link from either the parent site or the child site.

> [!TIP]  
> You can edit database replication links from the **Database Replication** node in either workspace. However, when you use the **Database Replication** node in the **Monitoring** workspace, you also can view the status of database replication. It also provides access to the [Replication Link Analyzer](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA) tool. Use this tool to help investigate problems with database replication.  

For more information about how to configure replication links, see [Site database replication controls](#BKMK_DBRepControls). For more information about how to monitor replication, see [How to monitor database replication links and replication status](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_MonitorRepLinksAndStatuss).

### <a name="bkmk_distviews"></a> Distributed views

Through distributed views, when you make a request at the CAS for selected site data, it directly accesses the database at the child primary site. The direct access replaces the need to replicate that site data from the primary site to the CAS. Because each replication link is independent from other replication links, you can use distributed views on only the replication links that you choose. You can't use distributed views between a primary site and a secondary site.  

Distributed views provide the following benefits:  

- Reduce the CPU load to process database changes at the CAS and primary sites
- Reduce the amount of data that transfers across the network to the CAS
- Improve the performance of the SQL server that hosts the CAS database
- Reduce the disk space used by the CAS database

Consider using distributed views when a primary site is closely located to the CAS on the network, the two sites are always on, and always connected. Distributed views replace the replication of the selected data between the sites with direct connections between the SQL servers at each site. The CAS makes a direct connection each time you request this data.

The site requests distributed view data in the following example scenarios:

- When you run reports or queries
- When you view information in Resource Explorer
- Collection evaluation for collections that include site data-based rules

By default, distributed views are turned off for each replication link. When you turn on distributed views, you select site data that won't replicate to the CAS across that link. The CAS accesses this data directly from the database of the child primary site that shares the link. You can configure the following types of site data for distributed views:  

- **Hardware inventory** data from clients
- **Software inventory and software metering** data from clients
- **Status messages** from clients, the primary site, and all secondary sites

When you view data in the Configuration Manager console or in reports, distributed views are operationally invisible to you. When you request data that's enabled for distributed views, the CAS site database server directly accesses the child primary site's database to retrieve the information.

For example, you use a Configuration Manager console at the CAS to request hardware inventory information from primary site ABC and primary size XYZ. You enable hardware inventory for a distributed view at site ABC. The site retrieves XYZ client inventory information from the CAS database. It retrieves ABC client inventory information from the ABC site database. This information appears in the Configuration Manager console or in a report without identifying the source.  

As long as a replication link has a type of data enabled for distributed views, the child primary site doesn't replicate the data to the CAS. When you turn off distributed views for a type of data, the child primary site resumes the replication of the data to the CAS as part of normal data replication. Before this data is available at the CAS, the replication groups that have this data must reinitialize between the primary site and the CAS. Similarly, after you uninstall a primary site that has distributed views turned on, before you can access this data on the CAS, it must complete reinitialization of its data.  

> [!IMPORTANT]  
> When you use distributed views on any replication link in the site hierarchy, before you uninstall any primary site, turn off distributed views for all replication links. For more information, see [Uninstall a primary site that is configured with distributed views](/sccm/core/servers/deploy/install/uninstall-sites-and-hierarchies#BKMK_UninstallPrimaryDistViews).  

#### Prerequisites and limitations for distributed views  

- You can only use distributed views on replication links between a CAS and a primary site.

- The CAS must use an *Enterprise* edition of SQL Server. The primary site doesn't have this requirement.

- The CAS can have only one instance of the SMS Provider installed. Install that one instance on the site database server. This requirement supports Kerberos authentication. The SQL server at the CAS requires Kerberos to access the SQL server at the child primary site. There are no limitations on the SMS Provider at the child primary site.

- The CAS can have only one instance of SQL Server Reporting Services. Install the reporting services point on the site database server. This requirement supports Kerberos authentication. The SQL server at the CAS requires Kerberos to access the SQL server at the child primary site.

- You can't host the site database on a [SQL Server cluster](/sccm/core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database).

- In version 1902 and earlier, you can't host the site database on a [SQL Server Always On availability group](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database). To support this configuration, update to version 1906 or later.<!-- SCCMDocs-pr#3792 -->

- The CAS database server's computer account requires **Read** permissions on the primary site database.

> [!IMPORTANT]  
> Distributed views and [schedules](#BKMK_schedules) for when data can replicate are mutually exclusive settings for a database replication link.  

### <a name="BKMK_schedules"></a> Schedule transfers of site data on database replication links

To help you control the network bandwidth that's used to replicate site data from a child primary site to its CAS, schedule when a replication link is used. You can also specify when different types of site data replicate. You can control when the primary site replicates status messages, inventory, and metering data. Database replication links from secondary sites don't support schedules for site data. You can't schedule the transfer of global data.  

When you configure a database replication link schedule, you can restrict the transfer of selected site data from the primary site to the CAS. You can also configure different times to replicate different types of site data.  

> [!IMPORTANT]  
> [Distributed views](#bkmk_distviews) and schedules for when data can replicate are mutually exclusive configurations for a database replication link.  

### <a name="BKMK_SummarizeDBReplication"></a> Summarization of database replication traffic

Each site periodically summarizes data about the network traffic that traverses database replication links for the site. The site uses summarized data in reports for database replication. Both sites on a replication link summarize the network traffic that traverses the replication link. The site database server summarizes the data. After it summarizes data, the information replicates to other sites as global data.  

By default, summarization occurs every 15 minutes. To modify the frequency of summarization for network traffic, edit the **Summarization interval** in the properties of the database replication link. The frequency of summarization affects the information that you view in reports about database replication. You can choose an interval from 5 to 60 minutes. When you increase the frequency of summarization, you increase the processing load on the SQL server at each site on the replication link.  

### <a name="BKMK_DBRepThresholds"></a> Database replication thresholds

Database replication thresholds define when the site reports the status of a database replication link as either degraded or failed. By default, it sets a link to *degraded* status when any one replication group fails to complete replication for 12 consecutive attempts. It sets the link to *failed* status when any replication group fails to replicate in 24 consecutive attempts.  

You can specify custom values for degraded or failed status. If you adjust these values, you can more accurately monitor the health of database replication across the links.  

It's possible for one or more replication groups to fail to replicate while other replication groups continue to replicate successfully. Plan to review the replication status of a link when it first reports a degraded status. If there are recurring delays for specific replication groups, and their delay doesn't present a problem, or where the network link between sites has low available bandwidth, consider modifying the retry values for the degraded or failed status of the link. When you increase the number of retries before the link is set to degraded or failed, you can eliminate false warnings for known issues and more accurately track the status of the link.  

Also consider the sync interval for each replication group to understand how frequently replication of that group occurs. To view the **Synchronization Interval** for replication groups, in the **Monitoring** workspace, on the **Database Replication** node, select the **Replication Detail** tab of a replication link.  

For more information about how to monitor database replication, including how to view the replication status, see [How to monitor database replication links and replication status](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_MonitorRepLinksAndStatuss).  

For more information about configuring database replication thresholds, see [Site database replication controls](#BKMK_DBRepControls).  


## <a name="BKMK_DBRepControls"></a> Site database replication controls

To help you control the network bandwidth used for database replication, change the settings for each site database. The settings only apply to the site database in which you configure them. The settings are always used when the site replicates any data by database replication to any other site.  

You can modify the following replication controls for each site database:  

- The SSB port
- The period of time to wait before replication failures trigger the site to reinitialize its copy of the site database
- Compress the data that it replicates by database replication. The data is compressed only for transfer between sites, and not for storage in the site database at either site.  

To change the settings for the replication controls for a site database, in the Configuration Manager console, on the **Database Replication** node, edit the properties of the site database. This node appears under the **Hierarchy Configuration** node in the **Administration** workspace, and also appears in the **Monitoring workspace**. To edit the properties of the site database, select the replication link between the sites, and then open either **Parent Database Properties** or **Child Database Properties**.  

> [!TIP]  
> You can configure database replication controls from the **Database Replication** node in either workspace. However, when you use the **Database Replication** node in the **Monitoring** workspace, you also can view the status of database replication. It also provides access to the [Replication Link Analyzer](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA) tool. Use this tool to help investigate problems with database replication.  
