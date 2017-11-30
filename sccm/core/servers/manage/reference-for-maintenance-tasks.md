---
title: "Reference for maintenance tasks"
titleSuffix: "Configuration Manager"
description: "Read details for each of the System Center Configuration Manager site maintenance tasks and whether these tasks are enabled by default."
ms.custom: na
ms.date: 3/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68dc6acd-5848-47a4-b4c1-ffa40e47890b
caps.latest.revision: 16
caps.handback.revision: 0
author: mstewart
ms.author: mstewart
manager: angrobe

---
# Reference for maintenance tasks for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

This topic lists details for each of the System Center Configuration Manager site maintenance tasks and specifies the site types where the task is available. Each entry also indicates if the task is enabled or not enabled by default. For information about planning for and configuring sites to run maintenance tasks, see [Maintenance tasks for System Center Configuration Manager](../../../core/servers/manage/maintenance-tasks.md).  

**Backup Site Server**: Use this task to prepare for the recovery of critical data. You can create a backup of your critical information to restore a site and the Configuration Manager database. For more information, see [Backup and recovery for System Center Configuration Manager](../../../protect/understand/backup-and-recovery.md).  

-   **Central administration site**: Enabled    
-   **Primary site**: Not enabled    
-   Secondary site: Not available  

**Check Application Title with Inventory Information**: Use this task to maintain consistency between software titles that are reported in the software inventory and software titles in the Asset Intelligence catalog. For more information, see [Introduction to Asset Intelligence in System Center Configuration Manager](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

-   **Central administration site**: Enabled    
-   **Primary site**: Enabled    
-   Secondary site: Not available  

**Clear Install Flag**: Use this task to remove the installed flag for clients that don't submit a Heartbeat Discovery record during the **Client Rediscovery** period. The installed flag prevents automatic client push installation to a computer that might have an active Configuration Manager client.  

-   Central administration site: Not available    
-   **Primary site**: Not enabled    
-   Secondary site: Not available  

**Delete Aged Application Request Data**: Use this task to delete aged application requests from the database. For more information about application requests, see [Create and deploy an application with System Center Configuration Manager](/sccm/apps/get-started/create-and-deploy-an-application).  

-   Central administration site: Not available
-   **Primary site**: Enabled    
-   Secondary site: Not available  

**Delete Aged Client Download History**: Use this task to delete historical data about the download source used by clients. Download source information is used to populate the [Client Data Sources dashboard](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).  
-  Central administration site – Not available
-	 **Primary site** - Enabled
-  Secondary site - Not available

**Delete Aged Client Operations**: Use this task to delete all aged data for client operations from the site database. For example, this includes data for aged or expired client notifications (like download requests for machine or user policy), and for Endpoint Protection (like requests by an administrative user for clients to run a scan or download updated definitions).

-   **Central administration site**: Enabled    
-   **Primary site**: Enabled    
-   Secondary site: Not available  

**Delete Aged Client Presence History**: Use this task to delete history information about the online status of clients (recorded by client notification) that is older than the specified time. For more information about client notification, see [How to monitor clients in System Center Configuration Manager](../../../core/clients/manage/monitor-clients.md).  

-   **Central administration site**: Enabled   
-   **Primary site**: Enabled    
-   Secondary site: Not available  

**Delete Aged Cloud Management Gateway Traffic Data**:
Use this task to delete all aged data about the traffic that passes through the [cloud management gateway](/sccm/core/clients/manage/plan-cloud-management-gateway) from the site database. For example, this includes data about the number of requests, total request bytes, total response bytes, number of failed requests, and maximum number of concurrent requests.  
- **Central administration site** - Enabled
- **Primary site** - Enabled
- Secondary site - Not available


**Delete Aged Collected Files**: Use this task to delete aged information about collected files from the database. This task also deletes the collected files from the site server folder structure at the selected site. By default, the five most-recent copies of collected files are stored on the site server in the **Inboxes\sinv.box\FileCol** directory. For more information, see [Introduction to software inventory in System Center Configuration Manager](/sccm/core/clients/manage/inventory/introduction-to-software-inventory).  

-   Central administration site: Not available    
-   **Primary site**: Enabled    
-   Secondary site: Not available  

**Delete Aged Computer Association Data**: Use this task to delete aged Operating System Deployment computer association data from the database. This information is used as part of completing user state restores. For more information about computer associations, see [Manage user state in System Center Configuration Manager](../../../osd/get-started/manage-user-state.md).  

-   Central administration site: Not available    
-   **Primary site**: Enabled    
-   Secondary site: Not available  

**Delete Aged Delete Detection Data**: Use this task to delete aged data from the database that has been created by Extraction Views. By default, Extraction Views are disabled. You only enable them by using the Configuration Manager SDK. Unless Extraction Views are enabled, there is no data for this task to delete.  

-   **Central administration site**: Enabled    
-   **Primary site**: Enabled    
-   Secondary site: Not available  

**Delete Aged Device Wipe Record**: Use this task to delete aged data about mobile device wipe actions from the database. For information about wiping mobile devices, see [Protect data with remote wipe, lock, or passcode reset using System Center Configuration Manager](/sccm/mdm/deploy-use/wipe-lock-reset-devices).  

-   Central administration site: Not available    
-   **Primary site**: Enabled    
-   Secondary site: Not available  

**Delete Aged Devices Managed by the Exchange Server Connector**: Use this task to delete aged data about mobile devices that are managed by using the Exchange Server connector. This data is deleted according to the interval that is configured for the **Ignore mobile devices that are inactive for more than (days)** option on the **Discovery** tab of the Exchange Server connector properties. For more information, see [Manage mobile devices with System Center Configuration Manager and Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

-   Central administration site: Not available   
-   **Primary site**: Enabled    
-   Secondary site: Not available  

**Delete Aged Discovery Data**: Use this task to delete aged discovery data from the database. This data can include records that result from heartbeat discovery, network discovery, and Active Directory Domain Services discovery methods (System, User, and Group). When this task runs at a site, data associated with that site is deleted, and those changes replicate to other sites. For information about Discovery, see [Run discovery for System Center Configuration Manager](../../../core/servers/deploy/configure/run-discovery.md).  

-   Central administration site: Not available    
-   **Primary site**: Enabled    
-   Secondary site: Not available  

**Delete Aged Distribution Point Usage Data**: Use this task to delete from the database aged data for distribution points that has been stored longer than a specified time.  

-   **Central administration site**: Enabled    
-   **Primary site**: Enabled    
-   Secondary site: Not available  

**Delete Aged Endpoint Protection Health Status History Data**: Use this task to delete aged status information for Endpoint Protection from the database. For more information about Endpoint Protection status information, see [How to monitor Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/monitor-endpoint-protection.md).  

-   Central administration site: Not available    
-   **Primary site**: Enabled    
-   Secondary site: Not available  

**Delete Aged Enrolled Devices**: Beginning with the update for 1602, this task is disabled by default. You can use this task to delete from the site database the aged data about mobile devices that haven't reported any information to the site for a specified time.

This task applies to devices that are enrolled by using Microsoft Intune (hybrid) or Configuration Manager on-premises mobile device management. For information about the operating systems of devices that are enrolled by using Configuration Manager or Intune, see the [Mobile devices enrolled by Microsoft Intune](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mobile-devices-enrolled-by-microsoft-intune) section in [Supported operating systems for clients and devices for System Center Configuration Manager](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md).

-   Central administration site: Not available    
-   **Primary site**: Not enabled    
-   Secondary site: Not available  

**Delete Aged Inventory History**: Use this task to delete inventory data that has been stored longer than a specified time from the database. For information about inventory history, see [How to use Resource Explorer to view hardware inventory in System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

-   Central administration site: Not available    
-   **Primary site**: Enabled    
-   Secondary site: Not available  

**Delete Aged Log Data**: Use this task to delete aged log data that is used for troubleshooting from the database. This data isn't related to Configuration Manager component operations.  

> [!IMPORTANT]  
> By default, this task runs daily at each site. At a central administration site and primary sites, the task deletes data that is older than 30 days. When you use SQL Server Express at a secondary site, ensure that this task runs daily and deletes data that has been inactive for seven days.  

-   **Central administration site**: Enabled    
-   **Primary site**: Enabled    
-   **Secondary site**: Enabled  

**Delete Aged Notification Task History**: Use this task to delete information about client notification tasks from the site database when it hasn't been updated for a specified time. For more information about client notification, see [Client deployment tasks for System Center Configuration Manager](../../../core/clients/manage/monitor-clients.md).  

-   Central administration site: Not available    
-   **Primary site**: Enabled    
-   Secondary site: Not available  

**Delete Aged Replication Summary Data**: Use this task to delete aged replication summary data from the site database when it hasn't been updated for a specified time. For more information, see the [How to monitor database replication links and replication status](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) section in the [Monitor hierarchy and replication infrastructure in System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) topic.  

-   **Central administration site**: Enabled    
-   **Primary site**: Enabled    
-   **Secondary site**: Enabled  

**Delete Aged Passcode Records**: Use this task at the top-level site of your hierarchy to delete aged Passcode Reset data for Android and Windows Phone devices. Passcode Reset data is encrypted, but does include the PIN for devices. By default, this task is enabled and deletes data that is older than one day.  

-   **Central administration site**: Enabled    
-   **Primary site**: Enabled    
-   Secondary site: Not available  

**Delete Aged Replication Tracking Data**: Use this task to delete aged data about database replication between Configuration Manager sites from the database. When you change the configuration of this maintenance task, the configuration applies to each applicable site in the hierarchy. For more information, see the [How to monitor database replication links and replication status](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) section in the [Monitor hierarchy and replication infrastructure in System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) topic.  

-   **Central administration site**: Enabled    
-   **Primary site**: Enabled    
-   **Secondary site**: Enabled  

**Delete Aged Software Metering Data**: Use this task to delete aged data for software metering that has been stored longer than a specified time from the database. For more information, see [Software metering in System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

-   Central administration site: Not available    
-   **Primary site**: Enabled    
-   Secondary site: Not available  

**Delete Aged Software Metering Summary Data**: Use this task to delete aged summary data for software metering that has been stored longer than a specified time from the database. For more information, see [Software metering in System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

-   Central administration site: Not available    
-   **Primary site**: Enabled    
-   Secondary site: Not available  

**Delete Aged Status Messages**: Use this task to delete aged status message data as configured in status filter rules from the database. For information, see the "Monitor the status system of Configuration Manager" section in the topic [Use alerts and the status system for System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

-   **Central administration site**: Enabled    
-   **Primary site**: Enabled    
-   Secondary site: Not available  

**Delete Aged Threat Data**: Use this task to delete aged Endpoint Protection threat data that has been stored longer than a specified time from the database. For information about Endpoint Protection, see [Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

-   Central administration site: Not available    
-   **Primary site**: Enabled    
-   Secondary site: Not available  

**Delete Aged Unknown Computers**: Use this task to delete information about unknown computers from the site database when it hasn't been updated for a specified time. For more information, see [Prepare for unknown computer deployments in System Center Configuration Manager](../../../osd/get-started/prepare-for-unknown-computer-deployments.md).  

-   Central administration site: Not available    
-   **Primary site**: Enabled    
-   Secondary site: Not available  

**Delete Aged User Device Affinity Data**: Use this task to delete aged User Device Affinity data from the database. For more information, see [Link users and devices with user device affinity in System Center Configuration Manager](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

-   Central administration site: Not available    
-   **Primary site**: Enabled    
-   Secondary site: Not available  

**Delete Expired MDM Bulk Enroll Package Records**: Use this task to delete old Bulk Enrollment certificates and corresponding profiles after the enrollment certificate has expired. For more information, see [Create certificate profiles](/sccm/protect/deploy-use/create-certificate-profiles).
-   **Central administrations site**: Enabled
-   **Primary site**: Enabled
-   Secondary Site: Not available

**Delete Inactive Client Discovery Data**: Use this task to delete discovery data for inactive clients from the database. Clients are marked as inactive when the client is flagged as obsolete and by configurations that are made for client status.

This task operates only on resources that are Configuration Manager clients. It's different than the **Delete Aged Discovery Data** task, which deletes any aged discovery data record. When this task runs at a site, it removes the data from the database at all sites in a hierarchy. For more information, see [How to configure client status in System Center Configuration Manager](../../../core/clients/deploy/configure-client-status.md).  

> [!IMPORTANT]  
> When it's enabled, configure this task to run at an interval greater than the **Heartbeat Discovery** schedule. This enables active clients to send a Heartbeat Discovery record to mark their client record as active so this task doesn't delete them.  

-   Central administration site: Not available    
-   **Primary site**: Not enabled    
-   Secondary site: Not available  

**Delete Obsolete Alerts**: Use this task to delete expired alerts that have been stored longer than a specified time from the database. For more information, see [Use alerts and the status system for System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

-   **Central administration site**: Enabled    
-   **Primary site**: Enabled    
-   Secondary site: Not available  

**Delete Obsolete Client Discovery Data**: Use this task to delete obsolete client records from the database. A record that is marked as obsolete has usually been replaced by a newer record for the same client. The newer record becomes the client's current record. For information about Discovery, see [Run discovery for System Center Configuration Manager](../../../core/servers/deploy/configure/run-discovery.md).  

> [!IMPORTANT]  
> When it's enabled, configure this task to run at an interval greater than the Heartbeat Discovery schedule. This enables the client to send a Heartbeat Discovery record that sets the obsolete status correctly.  

-   Central administration site: Not available    
-   **Primary site**: Not enabled    
-   Secondary site: Not available  

**Delete Obsolete Forest Discovery Sites and Subnets**: Use this task to delete data about Active Directory sites, subnets, and domains that haven't been discovered by the Active Directory Forest Discovery method in the last 30 days. This removes the discovery data, but doesn't affect boundaries that are created from this discovery data. For more information, see [Run discovery for System Center Configuration Manager](../../../core/servers/deploy/configure/run-discovery.md).  

-   **Central administration site**: Enabled    
-   **Primary site**: Enabled    
-   Secondary site: Not available  

**Delete Orphaned Client Deployment State Records**: Use this task to periodically purge the table that contains client deployment state information. This task will clean up records associated with obsolete or decommissioned devices.  
-   **Central administration site**: Enabled    
-   **Primary site**: Enabled    
-   Secondary site: Not available

**Delete Unused Application Revisions**: Use this task to delete application revisions that are no longer referenced. For more information, see [How to revise and supersede applications in System Center Configuration Manager](../../../apps/deploy-use/revise-and-supersede-applications.md).  

-   Central administration site: Not available    
-   **Primary site**: Enabled    
-   Secondary site: Not available  

**Evaluate Collection Members**: You configure the Collection Membership Evaluation as a site component. For information about site components, see [Site components for System Center Configuration Manager](../../../core/servers/deploy/configure/site-components.md).  

-   Central administration site: Not available    
-   **Primary site**: Enabled    
-   Secondary site: Not available  

**Monitor Keys**: Use this task to monitor the integrity of the Configuration Manager database primary keys. A primary key is a column (or a combination of columns) that uniquely identifies one row and distinguishes it from any other row in a Microsoft SQL Server database table.  

-   **Central administration site**: Enabled    
-   **Primary site**: Enabled    
-   Secondary site: Not available  

**Rebuild Indexes**: Use this task to rebuild the Configuration Manager database indexes. An index is a database structure that is created on a database table to speed up data retrieval. For example, searching an indexed column is often much faster than searching a column that isn't indexed.

To improve performance, the Configuration Manager database indexes are frequently updated to remain synchronized with the constantly changing data that is stored in the database. This task creates indexes on database columns that are at least 50 percent unique, drops indexes on columns that are less than 50 percent unique, and rebuilds all existing indexes that meet the data uniqueness criteria.  

-   **Central administration site**: Not enabled    
-   **Primary site**: Not enabled    
-   **Secondary site**: Not enabled  

**Summarize Installed Software Data**: Use this task to summarize the data for installed software from multiple records into one general record. Data summarization can compress the amount of data that is stored in the Configuration Manager database. For more information, see [Introduction to software inventory in System Center Configuration Manager](../../clients/manage/inventory\introduction-to-software-inventory.md).  

-   Central administration site: Not available    
-   **Primary site**: Enabled    
-   Secondary site: Not available  

**Summarize Software Metering File Usage Data**: Use this task to summarize the data from multiple records for software metering file usage into one general record. Data summarization can compress the amount of data that is stored in the Configuration Manager database.

You can use this task with the **Summarize Software Metering Monthly Usage Data** task to summarize software metering data and to conserve disk space in the Configuration Manager database. For more information, see [Software metering in System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

-   Central administration site: Not available    
-   **Primary site**: Enabled    
-   Secondary site: Not available  

**Summarize Software Metering Monthly Usage Data**: Use this task to summarize the data from multiple records for software metering monthly usage into one general record. Data summarization can compress the amount of data that is stored in the Configuration Manager database.

You can use this task with the **Summarize Software Metering File Usage Data** task to summarize software metering data and to conserve space in the Configuration Manager database. For more information, see [Software metering in System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

-   Central administration site: Not available    
-   **Primary site**: Enabled    
-   Secondary site: Not available  

**Update Application Available Targeting**: Use this task to have Configuration Manager recalculate the mapping of policy and application deployments to resources in collections. When you deploy policy or applications to a collection, Configuration Manager creates an initial mapping between the objects that you deploy and the collection members.

These mappings are stored in a table for quick reference. When a collections membership changes, these stored mappings are updated to reflect those changes. However, it's possible for these mappings to fall out of sync. For example, if the site fails to properly process a notification file, that change might not be reflected in a change to the mappings. This task refreshes that mapping based on current collection membership.  

-   Central administration site: Not available    
-   **Primary site**: Enabled    
-   Secondary site: Not available  

**Update Application Catalog Tables**: Use this task to synchronize the Application Catalog website database cache with the latest application information. When you change the configuration of this maintenance task, the configuration applies to all primary sites in the hierarchy.  

-   Central administration site: Not available    
-   **Primary site**: Enabled    
-   Secondary site: Not available  
