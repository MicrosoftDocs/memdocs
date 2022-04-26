---
title: Reference for maintenance tasks
titleSuffix: Configuration Manager
description: Details for each of the Configuration Manager site maintenance tasks
ms.date: 04/27/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# Reference for maintenance tasks in Configuration Manager

*Applies to: Configuration Manager (current branch)*

This article lists the details for each of the Configuration Manager site maintenance tasks. Each entry specifies the site types where the task is available, and whether it's enabled by default.

For more information, see [Set up maintenance tasks](maintenance-tasks.md#set-up-maintenance-tasks).  

## Tasks

### Backup Site Server

Use this task to create a backup of your critical information to restore a site and the Configuration Manager database. For more information, see [Back up a Configuration Manager site](backup-and-recovery.md).  

| Site type | Status |
| --------- | ------ |
|**Central administration site**|Enabled|
|**Primary site**|Not enabled|
|Secondary site|Not available|

### Check Application Title with Inventory Information

Use this task to maintain consistency of software titles between software inventory and the Asset Intelligence catalog. For more information, see [Introduction to Asset Intelligence](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

| Site type | Status |
| --------- | ------ |
|**Central administration site**|Enabled|
|Primary site|Not available|
|Secondary site|Not available|

### Clear Undiscovered Clients

> [!TIP]
> You may also see this task in the console named **Clear Install Flag**.

Use this task to remove the installed flag for clients that don't submit a Heartbeat Discovery record during the **Client Rediscovery** period. The installed flag prevents automatic client push installation to a computer that might have an active Configuration Manager client. The default value is 21 days.

> [!IMPORTANT]
> Make sure this value is greater than the interval for [Heartbeat discovery](../deploy/configure/configure-discovery-methods.md#BKMK_ConfigHBDisc), which by default is seven days. Otherwise, clients will unnecessarily reinstall.<!-- 7355291 -->

| Site type | Status |
| --------- | ------ |
|Central administration site|Not available|
|**Primary site**|Not enabled|
|Secondary site|Not available|

### Delete Aged Application Request Data

Use this task to delete aged application requests from the database. For more information, see [Create and deploy an application](../../../apps/get-started/create-and-deploy-an-application.md).  

| Site type | Status |
| --------- | ------ |
|Central administration site|Not available|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Delete Unused Application Revisions

Use this task to delete application revisions that are no longer referenced. For more information, see [How to revise and supersede applications](../../../apps/deploy-use/revise-and-supersede-applications.md).

| Site type | Status |
| --------- | ------ |
|**Central administration site**|Enabled|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Delete Aged Client Download History

Use this task to delete historical data about the download source used by clients. The site uses download source information to populate the [Client Data Sources dashboard](../deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard).

| Site type | Status |
| --------- | ------ |
|Central administration site|Not available|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Delete Aged Client Operations

Use this task to delete from the site database all aged data for client operations. For example, this data includes the following operations:

- Aged or expired client notifications, like download requests for machine or user policy
- Endpoint Protection, like requests by an administrative user for clients to run a scan or download updated definitions
- Run Scripts status results

| Site type | Status |
| --------- | ------ |
|**Central administration site**|Enabled|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Delete Aged Client Presence History

Use this task to delete history information about the online status of clients recorded by client notification. It deletes information for clients with status that's older than the specified time. For more information, see [How to monitor clients](../../clients/manage/monitor-clients.md).

| Site type | Status |
| --------- | ------ |
|**Central administration site**|Enabled|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Delete Aged Cloud Management Gateway Traffic Data

Use this task to delete from the site database all aged data about the traffic that passes through the [cloud management gateway](../../clients/manage/cmg/overview.md). This data includes:

- The number of requests
- Total request bytes
- Total response bytes
- Number of failed requests
- Maximum number of concurrent requests

| Site type | Status |
| --------- | ------ |
|**Central administration site**|Enabled|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Delete Aged CMPivot Results

Use this task to delete from the site database aged information from clients in CMPivot queries. For more information, see [CMPivot for real-time data](cmpivot.md).

| Site type | Status |
| --------- | ------ |
|Central administration site|Not available|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Delete Aged Collected Diagnostic Files
<!--6503308-->
Use this task to delete [collected diagnostic files](../../clients/manage/client-notification.md#client-diagnostics). Collected client logs are stored according to the software inventory file collection settings. The files are stored on the site server in the **Inboxes\sinv.box\FileCol** directory. **Delete Aged Collected Diagnostic Files** uses a default value of 14 days when looking for diagnostic files to clean up and doesn't affect other collected files. This maintenance task is enabled by default and was introduced in Configuration Manager version 2010. Earlier Configuration Manager versions use the [Delete Aged Collected Files](#delete-aged-collected-files) task for deleting client diagnostic files.

| Site type | Status |
| --------- | ------ |
|Central administration site|Not available|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Delete Aged Collected Files

Use this task to delete from the database aged information about collected files. This task also deletes the collected files from the site server folder structure at the selected site. By default, the five most-recent copies of collected files are stored on the site server in the **Inboxes\sinv.box\FileCol** directory. For more information, see [Introduction to software inventory](../../clients/manage/inventory/introduction-to-software-inventory.md).  

| Site type | Status |
| --------- | ------ |
|Central administration site|Not available|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Delete Aged Computer Association Data

Use this task to delete from the database aged OS deployment computer association data. This information is used when restoring user state during a task sequence. For more information, see [Manage user state](../../../osd/get-started/manage-user-state.md).  

| Site type | Status |
| --------- | ------ |
|Central administration site|Not available|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Delete Aged Console Connection Data

This task deletes data from the site database about console connections to the site.<!-- SCCMDocs#528 -->

| Site type | Status |
| --------- | ------ |
|**Central administration site**|Enabled|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Delete Aged Delete Detection Data

Use this task to delete aged data from the database that has been created by extraction views. It deletes old data change information used by external systems extracting data from the database.<!--SCCMDocs#1590--><!--By default, Extraction Views are disabled. You only enable them by using the Configuration Manager SDK. Unless Extraction Views are enabled, there is no data for this task to delete.-->

| Site type | Status |
| --------- | ------ |
|**Central administration site**|Enabled|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Delete Aged Device Wipe Record

Use this task to delete from the database aged data about mobile device wipe actions. For more information, see [Protect data with remote wipe, lock, or passcode reset](../../../mdm/deploy-use/wipe-lock-reset-devices.md).  

| Site type | Status |
| --------- | ------ |
|Central administration site|Not available|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Delete Aged Discovery Data

Use this task to delete aged discovery data from the database. This data can include records from:

- Heartbeat discovery
- Network discovery
- Active Directory discovery methods: System, User, and Group

This task also removes aged devices marked as decommissioned. When this task runs at a site, data associated with that site is deleted, and those changes replicate to other sites. For more information, see [Run discovery](../deploy/configure/run-discovery.md).

| Site type | Status |
| --------- | ------ |
|Central administration site|Not available|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Delete Aged Distribution Point Usage Stats

Use this task to delete from the database aged data for distribution points that has been stored longer than a specified time.  

| Site type | Status |
| --------- | ------ |
|**Central administration site**|Enabled|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Delete Aged Endpoint Protection Health Status History Data

Use this task to delete from the database aged status information for Endpoint Protection (EP). For more information, see [How to monitor Endpoint Protection](../../../protect/deploy-use/monitor-endpoint-protection.md).

| Site type | Status |
| --------- | ------ |
|Central administration site|Not available|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Delete Aged Enrolled Devices

Use this task to delete from the site database the aged data about mobile devices that haven't reported any information to the site for a specified time.

This task applies to devices that are enrolled with Configuration Manager [on-premises MDM](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md). For more information on these devices, see [Supported operating systems for clients and devices](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS).

| Site type | Status |
| --------- | ------ |
|Central administration site|Not available|
|**Primary site**|Not enabled|
|Secondary site|Not available|

### Delete Aged Exchange Partnership

> [!Tip]
> > You may also see this task in the console named **Delete Aged Devices Managed by the Exchange Server Connector**.

Use this task to delete aged data about mobile devices managed by the Exchange Server connector. The site deletes this data according to the **Ignore mobile devices that are inactive for more than (days)** setting on the **Discovery** tab of the Exchange Server connector properties. For more information, see [Manage mobile devices with Configuration Manager and Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).

| Site type | Status |
| --------- | ------ |
|Central administration site|Not available|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Delete Aged Inventory History

Use this task to delete from the database inventory data that has been stored longer than a specified time. For more information, see [How to use Resource Explorer to view hardware inventory](../../clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).

| Site type | Status |
| --------- | ------ |
|Central administration site|Not available|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Delete Aged Log Data

Use this task to delete from the database aged log data used for troubleshooting. This data isn't related to Configuration Manager component operations.  

> [!IMPORTANT]  
> By default, this task runs daily at each site. At a central administration site and primary sites, the task deletes data that's older than 30 days. When you use SQL Server Express at a secondary site, make sure that this task runs daily and deletes data that's inactive for seven days.  

| Site type | Status |
| --------- | ------ |
|**Central administration site**|Enabled|
|**Primary site**|Enabled|
|**Secondary site**|Enabled|

### Delete Aged Notification Server History

This task deletes aged client presence history.

| Site type | Status |
| --------- | ------ |
|**Central administration site**|Enabled|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Delete Aged Notification Task History

Use this task to delete from the site database information about client notification tasks. This task applies to data that hasn't been updated for a specified time. For more information, see [Client notifications](../../clients/manage/client-notification.md).

| Site type | Status |
| --------- | ------ |
|Central administration site|Not available|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Delete Aged Passcode Records

Use this task at the top-level site of your hierarchy to delete aged Passcode Reset data for Windows Phone devices. Passcode Reset data is encrypted, but does include the PIN for devices. By default, this task is enabled, and deletes data that is older than one day.  

| Site type | Status |
| --------- | ------ |
|**Central administration site**|Enabled|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Delete Aged Replication Data

Use this task to delete from the database aged data about database replication between Configuration Manager sites. When you change the configuration of this maintenance task, the configuration applies to each applicable site in the hierarchy. For more information, see [Monitor database replication](monitor-replication.md).  

| Site type | Status |
| --------- | ------ |
|**Central administration site**|Enabled|
|**Primary site**|Enabled|
|**Secondary site**|Enabled|

### Delete Aged Replication Summary Data

Use this task to delete from the site database aged replication summary data when it hasn't been updated for a specified time. For more information, see [Monitor database replication](monitor-replication.md).  

| Site type | Status |
| --------- | ------ |
|**Central administration site**|Enabled|
|**Primary site**|Enabled|
|**Secondary site**|Enabled|

### Delete Aged Scenario Health History

Use this task to delete from the database aged data for scenario health activity. For more information, see [Monitor scenario health](scenario-health.md).

| Site type | Status |
| --------- | ------ |
|**Central administration site**|Enabled|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Delete Aged Software Metering Data

Use this task to delete from the database aged data for software metering that has been stored longer than a specified time. For more information, see [Software metering](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).

| Site type | Status |
| --------- | ------ |
|Central administration site|Not available|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Delete Aged Software Metering Summary Data

Use this task to delete from the database aged summary data for software metering that's been stored longer than a specified time. For more information, see [Software metering](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).

| Site type | Status |
| --------- | ------ |
|Central administration site|Not available|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Delete Aged Status Messages

Use this task to delete from the database aged status message data as configured in status filter rules. For more information, see [Monitor the status system](use-status-system.md#monitor-the-status-system).

| Site type | Status |
| --------- | ------ |
|**Central administration site**|Enabled|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Delete Aged Threat Data

Use this task to delete from the database aged Endpoint Protection threat data that's been stored longer than a specified time. For more information, see [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).

| Site type | Status |
| --------- | ------ |
|Central administration site|Not available|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Delete Aged Unknown Computers

Use this task to delete information about unknown computers from the site database when it hasn't been updated for a specified time. For more information, see [Prepare for unknown computer deployments](../../../osd/get-started/prepare-for-unknown-computer-deployments.md).

| Site type | Status |
| --------- | ------ |
|Central administration site|Not available|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Delete Aged User Device Affinity Data

Use this task to delete aged User Device Affinity data from the database. For more information, see [Link users and devices with user device affinity](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

| Site type | Status |
| --------- | ------ |
|Central administration site|Not available|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Delete Duplicate System Discovery Data

Use this task to delete from the site database any duplicate records generated by system discovery.<!-- SCCMDocs#1339 -->

| Site type | Status |
| --------- | ------ |
|**Central administration site**|Enabled|
|Primary site|Not available|
|Secondary site|Not available|

### Delete Expired MDM Bulk Enroll Package Records

Use this task to delete old Bulk Enrollment certificates and corresponding profiles after the enrollment certificate has expired. For more information, see [Create certificate profiles](../../../protect/deploy-use/create-certificate-profiles.md).

| Site type | Status |
| --------- | ------ |
|**Central administration site**|Enabled|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Delete Inactive Client Discovery Data

Use this task to delete from the database discovery data for inactive clients. The site marks clients as inactive when the client is flagged as obsolete and by configurations that are made for client status.

This task operates only on resources that are Configuration Manager clients. It's different than the **Delete Aged Discovery Data** task, which deletes any aged discovery data record. When this task runs at a site, it removes the data from the database at all sites in a hierarchy. For more information, see [How to configure client status](../../clients/deploy/configure-client-status.md).

> [!IMPORTANT]  
> When it's enabled, configure this task to run at an interval greater than the **Heartbeat Discovery** schedule. This configuration enables active clients to send a Heartbeat Discovery record to mark their client record as active so this task doesn't delete them.  

| Site type | Status |
| --------- | ------ |
|Central administration site|Not available|
|**Primary site**|Not enabled|
|Secondary site|Not available|

### Delete Obsolete Alerts

Use this task to delete from the database expired alerts that have been stored longer than a specified time. For more information, see [Configure alerts](configure-alerts.md).

| Site type | Status |
| --------- | ------ |
|**Central administration site**|Enabled|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Delete Obsolete Client Discovery Data

Use this task to delete obsolete client records from the database. A record that's marked as obsolete has usually been replaced by a newer record for the same client. The newer record becomes the client's current record. For information about discovery, see [Run discovery](../deploy/configure/run-discovery.md).

> [!IMPORTANT]  
> When it's enabled, configure this task to run at an interval greater than the Heartbeat Discovery schedule. This configuration enables the client to send a Heartbeat Discovery record that correctly sets the obsolete status.  

| Site type | Status |
| --------- | ------ |
|Central administration site|Not available|
|**Primary site**|Not enabled|
|Secondary site|Not available|

### Delete Obsolete Forest Discovery Sites and Subnets

Use this task to delete data about Active Directory sites, subnets, and domains. It removes data that the site hasn't discovered by the Active Directory Forest Discovery method in the last 30 days. This task removes the discovery data, but doesn't affect boundaries that you create from this discovery data. For more information, see [Run discovery](../deploy/configure/run-discovery.md).

| Site type | Status |
| --------- | ------ |
|**Central administration site**|Enabled|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Delete Orphaned Client Deployment State Records

Use this task to periodically purge the table that contains client deployment state information. This task cleans up records associated with obsolete or decommissioned devices.  

| Site type | Status |
| --------- | ------ |
|Central administration site|Not available|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Evaluate Collection Members

You configure the Collection Membership Evaluation as a site component. For more information, see [Site components](../deploy/configure/site-components.md).

| Site type | Status |
| --------- | ------ |
|Central administration site|Not available|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Monitor Keys

Use this task to monitor the integrity of the Configuration Manager database primary keys. A primary key is a column or a combination of columns that uniquely identifies one row. The key distinguishes the row from any other row in a Microsoft SQL Server database table.

| Site type | Status |
| --------- | ------ |
|**Central administration site**|Enabled|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Rebuild Indexes

Use this task to rebuild the Configuration Manager database indexes. An index is a database structure that's created on a database table to speed up data retrieval. For example, searching an indexed column is often much faster than searching a column that isn't indexed.

To improve performance, the Configuration Manager database indexes are frequently updated to remain synchronized with the constantly changing data that's stored in the database. This task:

- Rebuilds indexes when they are more than 10% fragmented
   - For indexes that are less than 30% fragmented, the index is reorganized
   - For indexes that are greater than 30% fragmented, the index is rebuilt

| Site type | Status |
| --------- | ------ |
|**Central administration site**|Not enabled|
|**Primary site**|Not enabled|
|**Secondary site**|Not enabled|

### Summarize Installed Software Data

Use this task to summarize the data from collected asset intelligence software information through the hardware inventory to merge multiple records into one general record. Data summarization can compress the amount of data that's stored in the Configuration Manager database. For more information, see [Configure Asset Intelligence maintenance tasks](../../clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_ConfigureMaintenanceTasks).

| Site type | Status |
| --------- | ------ |
|Central administration site|Not available|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Summarize Software Metering File Usage Metering Data

Use this task to summarize the data from multiple records for software metering file usage into one general record. Data summarization can compress the amount of data that's stored in the Configuration Manager database.

To summarize software metering data and to conserve disk space in the database, use this task with the **Summarize Software Metering Monthly Usage Data** task. For more information, see [Software metering](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).

| Site type | Status |
| --------- | ------ |
|Central administration site|Not available|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Summarize Software Metering Monthly Usage Data

Use this task to summarize the data from multiple records for software metering monthly usage into one general record. Data summarization can compress the amount of data that's stored in the Configuration Manager database.

To summarize software metering data and to conserve space in the database, use this task with the **Summarize Software Metering File Usage Data** task. For more information, see [Software metering](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).

| Site type | Status |
| --------- | ------ |
|Central administration site|Not available|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Update Application Available Targeting

Use this task to have Configuration Manager recalculate the mapping of policy and application deployments to resources in collections. When you deploy policy or applications to a collection, Configuration Manager creates an initial mapping between the objects that you deploy and the collection members.

These mappings are stored in a table for quick reference. When a collections membership changes, the site updates these stored mappings to reflect those changes. However, it's possible for these mappings to fall out of sync. For example, if the site fails to properly process a notification file, that change might not be reflected in a change to the mappings. This task refreshes that mapping based on current collection membership.  

| Site type | Status |
| --------- | ------ |
|Central administration site|Not available|
|**Primary site**|Enabled|
|Secondary site|Not available|

### Update Application Catalog Tables

This task exists in the site, but isn't used. The application catalog is no longer supported.

## See also

[Maintenance tasks](maintenance-tasks.md)
