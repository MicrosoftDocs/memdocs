---
title: Database replication
titleSuffix: Configuration Manager
description: Learn how Configuration Manager database replication uses SQL Server to transfer data in the hierarchy.
ms.date: 04/11/2022
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Database replication

*Applies to: Configuration Manager (current branch)*

Configuration Manager database replication uses SQL Server to transfer data. It uses this method to merge changes in its site database with the information from the database at other sites in the hierarchy.

Note the following points about database replication:

- All sites share the same information.

- When you install a site in a hierarchy, Configuration Manager automatically establishes database replication between the new site and its parent site.

- When the site installation finishes, database replication automatically starts.

When you add a new site to a hierarchy, Configuration Manager creates a generic database at the new site. The parent site creates a snapshot of the relevant data in its database. It then transfers the snapshot to the new site using [file-based replication](file-based-replication.md). The new site then uses the SQL Server Bulk Copy Program (BCP) to load the information into its local copy of the Configuration Manager database. After the snapshot loads, each site conducts database replication with the other site.

To replicate data between sites, Configuration Manager uses its own database replication service. The database replication service uses SQL Server change tracking to monitor the local site database for changes. It then replicates the changes to other sites by using SQL Server Service Broker (SSB). By default, this process uses TCP port 4022.

## Replication groups

Configuration Manager groups data that replicates by database replication into different replication groups. Each replication group has a separate, fixed replication schedule. The site uses this schedule to determine how frequently it replicates changes to other sites.

For example, a change to a role-based administration configuration replicates quickly to other sites. This behavior makes sure that the other site can quickly enforce these changes. A lower-priority configuration change, such as a request to install a new secondary site, replicates with less urgency. It can take several minutes for a new site request to reach the destination primary site.

## Settings

You can modify the following settings for database replication:

- **Database replication links**: Control when specific traffic traverses the network.

- **Distributed views**: When a central administration site (CAS) requests selected site data, it can access the data directly from the database at a child primary site.

- **Schedules**: Specify when a replication link is used, and when different types of site data replicate.

- **Summarization**: Change settings for data summarization about network traffic that traverses replication links. By default, summarization occurs every 15 minutes. It's used in reports for database replication.

- **Database replication thresholds**: Define when the site reports links as degraded or failed. You can also configure when Configuration Manager raises alerts about replication links that have a degraded or failed status.

## Types of data

Configuration Manager primarily classifies the data that it replicates as either *global data* or *site data*. When database replication occurs, the site transfers changes to global data and site data across the database replication link. Global data replicates to a parent or child site. Site data replicates only to a parent site. A third data type, *local data*, doesn't replicate to other sites. Local data is information that other sites don't require.

### Global data

Global data is administrator-created objects that replicate to all sites throughout the hierarchy. Secondary sites only receive a subset of global data, as global proxy data. You create global data at the CAS and primary sites. This type includes the following data:

- Software deployments
- Software updates
- Collection definitions
- Role-based administration security scopes

### Site data

Site data is operational information created by Configuration Manager primary sites and their assigned clients. Site data replicates to the CAS, but not to other primary sites. Site data is only viewable at the CAS and at the primary site where the data originates. You can only modify site data at the primary site where you created it. This type includes the following data:

- Hardware inventory
- Status messages
- Alerts
- The results of query-based collections

All site data replicates to the CAS. The CAS does administration and reporting for the entire site hierarchy.

## Database replication links

When you install a new site in a hierarchy, Configuration Manager automatically creates a database replication link between the parent site and the new site. It creates a single link to connect the two sites.

To control the transfer of data across the replication link, change settings for each link. Each replication link supports separate configurations. Each database replication link includes the following controls:

- Stop the replication of selected site data from a primary site to the CAS. This action causes the CAS to access this data directly from the database of the primary site.

- Schedule selected site data to transfer from a child primary site to the CAS.

- Define the settings that determine when a database replication link has a degraded or failed status.

- Specify when to raise alerts for a failed replication link.

- Specify how frequently Configuration Manager summarizes data about the replication traffic that uses the replication link. It uses this data in reports.

To configure a database replication link, in the Configuration Manager console, go to the **Monitoring** workspace. Select the **Database Replication** node, and edit the properties for the link. This node is also in the **Administration** workspace, under the **Hierarchy Configuration** node. Edit a replication link from either the parent site or the child site of the replication link.

> [!TIP]
> You can edit database replication links from the **Database Replication** node in either workspace. However, when you use the **Database Replication** node in the **Monitoring** workspace, you can also view the status of database replication. It also provides access to the [Replication Link Analyzer](../../servers/manage/monitor-replication.md#BKMK_RLA) tool. Use this tool to help investigate problems with database replication.

For more information about how to configure replication links, see [Site database replication controls](#site-database-replication-controls). For more information about how to monitor replication, see [Monitor database replication](../../servers/manage/monitor-replication.md).

## Distributed views

Through distributed views, when you make a request at the CAS for selected site data, it directly accesses the database at the child primary site. This direct access replaces the need to replicate site data from the primary site to the CAS. Because each replication link is independent from other replication links, you can use distributed views on the replication links that you choose. You can't use distributed views between a primary site and a secondary site.

Distributed views provide the following benefits:

- Reduce the CPU load to process database changes at the CAS and primary sites

- Reduce the amount of data that transfers across the network to the CAS

- Improve the performance of the SQL Server that hosts the CAS database

- Reduce the disk space used by the CAS database

Consider using distributed views when a primary site is closely located to the CAS on the network, the two sites are always on, and always connected. Distributed views replace the replication of the selected data between the sites with direct connections between the site database servers at each site. The CAS makes a direct connection each time you request this data.

The site requests distributed view data in the following example scenarios:

- When you run reports or queries
- When you view information in Resource Explorer
- Collection evaluation for collections that include site data-based rules

By default, distributed views are turned off for each replication link. When you turn on distributed views, you select site data that won't replicate to the CAS across that link. The CAS accesses this data directly from the database of the child primary site that shares the link. You can configure the following types of site data for distributed views:

- **Hardware inventory** data from clients
- **Software inventory and software metering** data from clients
- **Status messages** from clients, the primary site, and all secondary sites

When you view data in the Configuration Manager console or in reports, distributed views are operationally invisible to you. When you request data that's enabled for distributed views, the CAS site database server directly accesses the child primary site's database to retrieve the information.

For example, you use a Configuration Manager console connected to the CAS. You request information about hardware inventory from two primary sites: ABC and XYZ. You only enabled hardware inventory for distributed views at site ABC. The CAS retrieves inventory information for XYZ clients from its own database. The CAS retrieves inventory information for ABC clients directly from the database at site ABC. This information appears in the Configuration Manager console or in a report without identifying the source.

If a replication link has a type of data enabled for distributed views, the child primary site doesn't replicate that data to the CAS. When you turn off distributed views for a type of data, the child primary site resumes normal data replication to the CAS. Before this data is available at the CAS, the replication groups for this data must reinitialize between the primary site and the CAS. After you uninstall a primary site that has distributed views turned on, the CAS must complete reinitialization of its data before you can access data that you enabled for distributed views on the CAS.

> [!IMPORTANT]
> When you use distributed views on any replication link in the site hierarchy, before you uninstall any primary site, turn off distributed views for all replication links. For more information, see [Uninstall a primary site that uses distributed views](../../servers/deploy/install/uninstall-sites-and-hierarchies.md#bkmk_distviews).

### Prerequisites and limitations for distributed views

- Only use distributed views on replication links between the CAS and a primary site.

- The CAS must use SQL Server Enterprise edition. The primary site doesn't have this requirement.

- The CAS can have only one instance of the SMS Provider. Install that single instance on the site database server. This configuration supports Kerberos authentication. The SQL Server at the CAS requires Kerberos to access the SQL Server at the child primary site. There are no limitations on the SMS Provider at the child primary site.

- You can only install one reporting services point at the CAS. Install SQL Server Reporting Services on the site database server. This configuration supports Kerberos authentication. The SQL Server at the CAS requires Kerberos to access the SQL Server at the child primary site.

- You can host the site database on a [SQL Server Always On failover cluster instance](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md), if it has the following configurations:<!-- 13846496 -->

  - The CAS database is on a single SQL Server with a local SMS Provider.
  - The primary site listener is on port 1433.

- The computer account of the CAS database server requires **Read** permissions on the primary site database.

> [!IMPORTANT]
> Distributed views and [schedules](#schedule-transfers-of-site-data) for when data can replicate are mutually exclusive settings for a database replication link.

## Schedule transfers of site data

To help you control the network bandwidth that's used to replicate site data from a child primary site to the CAS, schedule when a replication link is used. Then specify when different types of site data replicate. You can control when the primary site replicates status messages, inventory, and metering data. Database replication links from secondary sites don't support schedules for site data. You can't schedule the transfer of global data.

When you configure a database replication link schedule, you can restrict the transfer of selected site data from the primary site to the CAS. You can also configure different times to replicate different types of site data.

> [!IMPORTANT]
> [Distributed views](#distributed-views) and schedules for when data can replicate are mutually exclusive configurations for a database replication link.

## Summarization of traffic

Each site periodically summarizes data about the network traffic that traverses database replication links for the site. The site uses summarized data in reports for database replication. Both sites on a replication link summarize the network traffic that traverses the replication link. The site database server summarizes the data. After it summarizes data, the information replicates to other sites as global data.

By default, summarization occurs every 15 minutes. To modify the frequency of summarization for network traffic, in the properties of the database replication link, edit the **Summarization interval**. The frequency of summarization affects the information that you view in reports about database replication. You can choose an interval from 5 to 60 minutes. When you increase the frequency of summarization, you increase the processing load on the SQL Server at each site on the replication link.

## Database replication thresholds

Database replication thresholds define when Configuration Manager reports the status of a database replication link as either degraded or failed. By default, it sets a link as *degraded* when any one replication group fails to complete replication for 12 consecutive attempts. It sets the link as *failed* when any replication group fails to replicate in 24 consecutive attempts.

You can specify custom values for degraded or failed status. If you adjust these values, you can more accurately monitor the health of database replication across the links.

One or more replication groups can fail to replicate while other replication groups continue to successfully replicate. Plan to review the replication status of a link when it first reports as degraded.

Consider modifying the retry values for the degraded or failed status of the link in the following situations:

- There are recurring delays for specific replication groups, and their delay isn't a problem

- The network link between sites has low available bandwidth

When you increase the number of retries before the site sets the link to degraded or failed, you can eliminate false warnings for known issues. This action lets you more accurately track the status of the link.

To understand how frequently replication of that group occurs, consider the replication sync interval for each replication group. To view the **Synchronization Interval** for replication groups, go to the **Monitoring** workspace in the Configuration Manager console. In the **Database Replication** node, select the **Replication Detail** tab of a replication link.

For more information about how to monitor database replication, including how to view the replication status, see [Monitor database replication](../../servers/manage/monitor-replication.md).

## Site database replication controls

To help you control the network bandwidth used for database replication, change the settings for each site database. The settings apply only to the site database in which you configure the settings. The settings are always used when the site replicates any data by database replication to any other site.

You can modify the following replication controls for each site database:

- The SSB port.

- The period of time to wait before replication failures trigger the site to reinitialize its copy of the site database.

- Compress the data that a site replicates. It only compresses the data for transfer between sites, and not for storage in the site database at either site.

To change the settings for the replication controls for a site database, in the Configuration Manager console, on the **Database Replication** node, edit the properties of the site database. This node appears under the **Hierarchy Configuration** node in the **Administration** workspace, and also appears in the **Monitoring** workspace. To edit the properties of the site database, select the replication link between the sites, and then open either **Parent Database Properties** or **Child Database Properties**.

> [!TIP]
> You can configure database replication controls from the **Database Replication** node in either workspace. However, when you use the **Database Replication** node in the **Monitoring** workspace, you can also view the status of database replication for a replication link, and access the Replication Link Analyzer tool to help you investigate problems with replication.

## Next steps

[Monitor replication](../../servers/manage/monitor-replication.md)

[Troubleshoot SQL Server replication](../../servers/manage/replication/overview.md)
