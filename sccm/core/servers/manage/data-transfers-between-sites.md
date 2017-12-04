---
title: "Data transfers"
titleSuffix: "Configuration Manager"
description: "Learn how Configuration Manager moves data between sites, and how you can manage the transfer of the data across your network."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dc526e8d-fac3-4bb5-b206-03ad29b0ae11
caps.latest.revision: 12
author: mestew
ms.author: mstewart
manager: angrobe

---
# Data transfers between sites in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager uses **file-based replication** and **database replication** to transfer different types of information between sites. Learn about how Configuration Manager moves data between sites, and how you can manage the transfer of data across your network.  


## <a name="bkmk_fileroute"></a> File-based replication  
Configuration Manager uses file-based replication to transfer file-based data between sites in your hierarchy. This data includes applications and packages that you want to deploy to distribution points in child sites, and unprocessed discovery data records that are transferred to parent sites and then processed.  

File-based communication between sites uses the **Server Message Block** (SMB) protocol on TCP/IP port 445. You can specify bandwidth throttling and pulse mode to control the amount of data transferred across the network, and you can use schedules to control when to send data across the network.  

### <a name="bkmk_routes"></a> File replication routes  
The following information can help you set up and use file replication routes.  

#### File replication route

Each file replication route identifies a destination site to which file-based data can transfer. Each site supports one file replication route to a specific destination site.  

You can change the following settings for file replication routes:  

-  **File Replication Account**. This account connects to the destination site, and writes data to that site's **SMS_Site** share. Data written to this share is processed by the receiving site. By default, when a site is added to the hierarchy, Configuration Manager assigns the computer account of the new site's site server as that sites File Replication Account. This account is then added to the destination site's **SMS_SiteToSiteConnection_&lt;Sitecode\>** group, a local group on the computer that grants access to the SMS_Site share. You can change this account to be a Windows user account. If you change the account, make sure you add the new account to the destination site's **SMS_SiteToSiteConnection_&lt;Sitecode\>** group.  

    > [!NOTE]  
    >  Secondary sites always use the computer account of the secondary site server as the **File Replication Account**.  

-  **Schedule**. You can set the schedule for each file replication route to restrict the type of data and time when data can transfer to the destination site.  
-  **Rate limits**. You can specify rate limits for each file replication route to control the network bandwidth that is used when the site transfers data to the destination site:  

    -  Use **Pulse mode** to specify the size of the data blocks that are sent to the destination site. You also can specify a time delay between sending each data block. Use this option when you must send data across a very low-bandwidth network connection to the destination site. For example, you might have constraints to send 1 KB of data every five seconds, but not 1 KB every three seconds, regardless of the speed of the link or its usage at a given time.
    -  Use **Limited to maximum transfer rates by hour** to have a site send data to a destination site by using only the percentage of time that you specify. When you use this option, Configuration Manager does not identify the network's available bandwidth, but instead divides the time it can send data into slices of time. Then, data is sent in a short block of time, which is followed by blocks of time when data is not sent. For example, if the maximum rate is set to **50%**, Configuration Manager transmits data for an amount of time followed by an equal period of time when no data is sent. The actual size amount of data, or the size of the data block, is not managed. Instead, only the amount of time during which data is sent is managed.  

        > [!CAUTION]  
        > By default, a site can use up to three **concurrent sendings** to transfer data to a destination site. When you enable rate limits for a file replication route, the **concurrent sendings** for sending data to that site are limited to one. This applies even when the **Limit available bandwidth (%)** is set to **100%**. For example, if you use the default settings for the sender, this reduces the transfer rate to the destination site to be one-third of the default capacity.  

-  You can configure a file replication route between two secondary sites to route file-based content between those sites.  

To manage a file replication route, in the **Administration** workspace, expand the **Hierarchy Configuration** node, and then select **File Replication**.  

#### Sender

Each site has one sender. The sender manages the network connection from one site to a destination site, and can establish connections to multiple sites at the same time. To connect to a site, the sender uses the file replication route to the site to identify the account to use to establish the network connection. The sender also uses this account to write data to the destination site's SMS_Site share.  

By default, the sender writes data to a destination site by using multiple **concurrent sendings**, typically referred to as a thread. Each concurrent sending, or thread, can transfer a different file-based object to the destination site. By default, when the sender begins to send an object, the sender continues to write blocks of data for that object until the entire object is sent. After all the data for the object has been sent, a new object can begin to send on that thread.  

You can change the following settings for a sender:  

-  **Maximum concurrent sendings**. By default, each site uses five concurrent sendings, with three available for use when it sends data to any one destination site. When you increase this number, you can increase the throughput of data between sites because Configuration Manager can transfer more files at the same time. Increasing this number also increases the demand for network bandwidth between sites.  

-  **Retry settings**. By default, each site retries a problem connection two times, with a one-minute delay between connection attempts. You can modify the number of connection attempts the site makes, and how long to wait between attempts.  

To manage the sender for a site, in the **Administration** workspace, expand the **Site Configuration** node, select the **Sites** node, and then select **Properties** for the site you want to manage. Select the **Sender** tab to change the sender settings.  

## <a name="bkmk_dbrep"></a> Database replication  
Configuration Manager database replication uses SQL Server to transfer data, and to merge changes that are made in a site database with the information stored in the database at other sites in the hierarchy. Note the following about database replication:

-  All sites share the same information.  
-  When you install a site in a hierarchy, database replication is automatically established between the new site and its designated parent site.  
-  When the site installation finishes, database replication automatically starts.  

When you add a new site to a hierarchy, Configuration Manager creates a generic database at the new site. Next, the parent site creates a snapshot of the relevant data in its database, and then transfers the snapshot to the new site by file-based replication. The new site then uses the SQL Server Bulk Copy Program (BCP) to load the information into its local copy of the Configuration Manager database. After the snapshot loads, each site conducts database replication with the other site.  

To replicate data between sites, Configuration Manager uses its own database replication service. The database replication service uses SQL Server change tracking to monitor the local site database for changes, and then replicates the changes to other sites by using SQL Server Service Broker (SSB). By default, this process uses TCP/IP port 4022.  

Configuration Manager groups data that replicates by database replication into different replication groups. Note the following about replication groups:

-  Each replication group has a separate, fixed replication schedule that determines how frequently changes to the data in the group is replicated to other sites.  

     For example, a change to a role-based administration configuration replicates quickly to other sites to ensure that these changes are enforced as soon as possible. Meanwhile, a lower-priority configuration change, such as a request to install a new secondary site, replicates with less urgency. It can take several minutes for a new site request to reach the destination primary site.  

-   You can modify the following settings for database replication:  

    -  **Database replication links**. Control when specific traffic traverses the network.  
    -  **Distributed views**. Change settings for replication links by which requests that are made at a central administration site for selected site data can access that site data directly from the database at a child primary site.  
    -  **Schedules**. Specify when a replication link is used, and when different types of site data replicates.  
    -  **Summarization**. Change settings for data summarization about network traffic that traverses replication links. Summarization occurs every 15 minutes, by default, and is used in reports for database replication.  
    -  **Database replication thresholds**. Define when links are reported as degraded or failed. You also can configure when Configuration Manager raises alerts about replication links that have a degraded or failed status.  

Configuration Manager classifies the data that it replicates by database replication as either **global data** or **site data**. When database replication occurs, changes to global data and site data are transferred across the database replication link. Global data can replicate to a parent or child site. Site data replicates only to a parent site. A third data type, local data, does not replicate to other sites. Local data is information that is not required by other sites. Note the following about data types:  

-  **Global data**. Global data refers to administrator-created objects that replicate to all sites throughout the hierarchy, although secondary sites receive only a subset of global data, as global proxy data. Global data includes software deployments, software updates, collection definitions, and role-based administration security scopes. Administrators can create global data at central administration sites and primary sites.  
-  **Site data**. Site data refers to operational information that Configuration Manager primary sites and the clients that report to primary sites create. Site data replicates to the central administration site but not to other primary sites. Site data includes hardware inventory data, status messages, alerts, and the results of query-based collections. Site data is only viewable at the central administration site and at the primary site where the data originates. Site data can be modified only at the primary site where it was created.  

     All site data replicates to the central administration site. The central administration site performs administration and reporting for the entire site hierarchy.  

The following sections detail settings that you can change to manage database replication.  

### <a name="bkmk_Dblinks"></a> Database replication links  
When you install a new site in a hierarchy, Configuration Manager automatically creates a database replication link between the parent site and the new site. A single link is created to connect the two sites.  

You can change settings for each database replication link to help you control the transfer of data across the replication link. Each replication link supports separate configurations. The controls for database replication links include the following:  

-  Stop the replication of selected site data from a primary site to the central administration site, so the central administration site can access this data directly from the database of the primary site.  
-  Schedule selected site data to transfer from a child primary site to the central administration site.
-  Define the settings that determine when a database replication link has a degraded status or has failed.
-  Specify when to raise alerts for a failed replication link.
-  Specify how frequently Configuration Manager summarizes data about the replication traffic that uses the replication link. This data is used in reports.

To configure a database replication link, in the Configuration Manager console, on the **Database Replication** node, edit the properties for the link. This node appears both in the **Monitoring** workspace and in the **Administration** workspace, on the **Hierarchy Configuration** node. You can edit a replication link from either the parent site or the child site of the replication link.  

> [!TIP]  
> You can edit database replication links from the **Database Replication** node in either workspace. However, when you use the **Database Replication** node in the **Monitoring** workspace, you also can view the status of database replication for replication links, and access the Replication Link Analyzer tool to help you investigate problems with database replication.  

For information about how to configure replication links, see [Site database replication controls](#BKMK_DBRepControls). For more information about how to monitor replication, see [How to monitor database replication links and replication status](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) in the [Monitor hierarchy and replication infrastructure in System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) topic.  

Use the information in the following sections to help you plan for database replication links.  

### <a name="bkmk_distviews"></a> Distributed views  
Through distributed views, requests that are made at a central administration site for selected site data access that site data directly from the database at a child primary site. The direct access replaces the need to replicate that site data from the primary site to the central administration site. Because each replication link is independent from other replication links, you can use distributed views on only the replication links that you choose. You cannot use distributed views between a primary site and a secondary site.  

Distributed views can provide the following benefits:  

-  Reduce the CPU load to process database changes at the central administration site and primary sites
-  Reduce the amount of data that transfers across the network to the central administration site
-  Improve the performance of the SQL server that hosts the central administration site's database
-  Reduce the disk space used by the database at the central administration site

Consider using distributed views when a primary site is in close proximity to the central administration site on the network, and the two sites are always on, and always connected. This is because distributed views replace the replication of the selected data between the sites with direct connections between the SQL servers at each site. A direct connection is made each time a request for this data is made at the central administration site. Typically, requests for data you might enable for distributed views are made when you run reports or queries, when you view information in Resource Explorer, and by collection evaluation for collections that include rules that are based on the site data.  

By default, distributed views are turned off for each replication link. When you turn on distributed views for a replication link, you select site data that will not replicate to the central administration site across that link. The central administration site accesses this data directly from the database of the child primary site that shares the link. You can configure the following types of site data for distributed views:  

-  Hardware inventory data from clients
-  Software inventory and metering data from clients
-  Status messages from clients, the primary site, and all secondary sites

Operationally, distributed views are invisible to an administrative user who views data in the Configuration Manager console or in reports. When a request is made for data that is enabled for distributed views, the SQL server that hosts the database for the central administration site directly accesses the SQL server of the child primary site to retrieve the information. For example, you use a Configuration Manager console at the central administration site to request information about hardware inventory from two sites, and only one site has hardware inventory enabled for a distributed view. The inventory information for clients from the site that is not configured for distributed views is retrieved from the database at the central administration site. The inventory information for clients from the site that is configured for distributed views is accessed from the database at the child primary site. This information appears in the Configuration Manager console or in a report without identifying the source.  

As long as a replication link has a type of data enabled for distributed views, the child primary site does not replicate the data to the central administration site. As soon as you turn off distributed views for a type of data, the child primary site resumes the replication of the data to the central administration site as part of normal data replication. However, before this data is available at the central administration site, the replication groups that have this data must reinitialize between the primary site and the central administration site. Similarly, after you uninstall a primary site that has distributed views turned on, the central administration site must complete reinitialization of its data before you can access data that was enabled for distributed views on the central administration site.  

> [!IMPORTANT]  
> When you use distributed views on any replication link in the site hierarchy, you must turn off distributed views for all replication links before you uninstall any primary site. For more information, see [Uninstall a primary site that is configured with distributed views](../../../core/servers/deploy/install/uninstall-sites-and-hierarchies.md#BKMK_UninstallPrimaryDistViews).  

#### Prerequisites and limitations for distributed views  

-  You can use distributed views only on replication links between a central administration site and a primary site.
- The central administration site must use an Enterprise edition of SQL Server. The primary site does not have this requirement.
-  The central administration site can have only one instance of the SMS Provider installed, and that instance must be installed on the site database server. This is required to support the Kerberos authentication required so that the SQL server at the central administration site can access the SQL server at the child primary site. There are no limitations on the SMS Provider at the child primary site.
-  The central administration site can have only one SQL Server Reporting Services point installed, and it must be located on site database server. This is required to support the Kerberos authentication required to enable the SQL server at the central administration site to access the SQL server at the child primary site.
-  The site database cannot be hosted on a SQL Server cluster.
-  The site database cannot be hosted on a SQL Server Always On availability group.
-  The computer account of the database server from the central administration site requires Read permissions for the site database of the primary site.

> [!IMPORTANT]  
>  Distributed views and schedules for when data can replicate are mutually exclusive settings for a database replication link.  

### <a name="BKMK_schedules"></a> Schedule transfers of site data on database replication links  
To help you control the network bandwidth that is used to replicate site data from a child primary site to its central administration site, you can schedule when a replication link is used, and specify when different types of site data replicates. You can control when the primary site replicates status messages, inventory, and metering data. Database replication links from secondary sites do not support schedules for site data. The transfer of global data cannot be scheduled.  

When you configure a database replication link schedule, you can restrict the transfer of selected site data from the primary site to the central administration site, and you can configure different times to replicate different types of site data.  

> [!IMPORTANT]  
> Distributed views and schedules for when data can replicate are mutually exclusive configurations for a database replication link.  

### <a name="BKMK_SummarizeDBReplication"></a> Summarization of database replication traffic  
Each site periodically summarizes data about the network traffic that traverses database replication links for the site. Summarized data is used in reports for database replication. Both sites on a replication link summarize the network traffic that traverses the replication link. The summarization of data is performed by the SQL Server that hosts the site database. After data is summarized, the information replicates to other sites as global data.  

By default, summarization occurs every 15 minutes. To modify the frequency of summarization for network traffic, in the properties of the database replication link, edit the **Summarization interval**. The frequency of summarization affects the information that you view in reports about database replication. You can choose an interval of between 5 minutes and 60 minutes. When you increase the frequency of summarization, you increase the processing load on the SQL server at each site on the replication link.  

### <a name="BKMK_DBRepThresholds"></a> Database replication thresholds  
Database replication thresholds define when the status of a database replication link is reported as either degraded or failed. By default, a link is set to degraded status when any one replication group fails to complete replication for a period of 12 consecutive attempts. The link is set to failed status when any replication group fails to replicate in 24 consecutive attempts.  

You can specify custom values to fine-tune when Configuration Manager reports a replication link as degraded or failed. Adjusting when Configuration Manager reports each status for your database replication links can help you accurately monitor the health of database replication across your database replication links.  

Because it is possible for one or a few replication groups to fail to replicate while other replication groups continue to replicate successfully, plan to review the replication status of a replication link when it first reports a degraded status. If there are recurring delays for specific replication groups and their delay does not present a problem, or where the network link between sites has low available bandwidth, consider modifying the retry values for the degraded or failed status of the link. When you increase the number of retries before the link is set to degraded or failed, you can eliminate false warnings for known issues and more accurately track the status of the link.  

Also, consider the replication sync interval for each replication group to understand how frequently replication of that group occurs. To view the **Synchronization Interval** for replication groups, in the **Monitoring** workspace, on the **Database Replication** node, select the **Replication Detail** tab of a replication link.  

For more information about how to monitor database replication, including how to view the replication status, see [How to monitor database replication links and replication status](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) in the [Monitor hierarchy and replication infrastructure in System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) topic.  

For information about configuring database replication thresholds, see [Site database replication controls](#BKMK_DBRepControls).  

## <a name="BKMK_DBRepControls"></a> Site database replication controls  
You can change the settings for each site database to help you control the network bandwidth used for database replication. The settings apply only to the site database in which you configure the settings. The settings are always used when the site replicates any data by database replication to any other site.  

The following are replication controls that you can modify for each site database:  

-  Change the SSB port.  
-  Configure the period of time to wait before replication failures trigger the site to reinitialize its copy of the site database.  
-  Configure a site database to compress the data that it replicates by database replication. The data is compressed only for transfer between sites, and not for storage in the site database at either site.  

To change the settings for the replication controls for a site database, in the Configuration Manager console, on the **Database Replication** node, edit the properties of the site database. This node appears under the **Hierarchy Configuration** node in the **Administration** workspace, and also appears in the **Monitoring workspace**. To edit the properties of the site database, select the replication link between the sites, and then open either **Parent Database Properties** or **Child Database Properties**.  

> [!TIP]  
> You can configure database replication controls from the **Database Replication** node in either workspace. However, when you use the **Database Replication** node in the **Monitoring** workspace, you also can view the status of database replication for a replication link, and access the Replication Link Analyzer tool to help you investigate problems with replication.  
