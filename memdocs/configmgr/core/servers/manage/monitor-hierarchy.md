---
title: Monitor the hierarchy
titleSuffix: Configuration Manager
description: Learn how to monitor your infrastructure in Configuration Manager by using the Monitoring workspace in the console.
ms.date: 06/06/2019
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: article
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Monitor the hierarchy

*Applies to: Configuration Manager (current branch)*

To monitor your hierarchy in Configuration Manager, use the **Monitoring** workspace in the Configuration Manager console.  

> [!NOTE]  
> The exception to this location is when migrating sites. Monitored this process in the **Migration** node of the **Administration** workspace. For more information, see [Operations for migrating to Configuration Manager current branch](../../migration/operations-for-migration.md).  

Along with using the Configuration Manager console for monitoring, use the following features:

- [Introduction to reporting](introduction-to-reporting.md)
- [Log files](../../plan-design/hierarchy/log-files.md).  

When you monitor sites, look for signs that indicate problems that require you to take action. For example:  

- A backlog of files on site servers and site systems.  

- Status messages that indicate an error or a problem.  

- Failing intrasite communication.  

- Error and warning messages in the system event log on servers.  

- Error and warning messages in the Microsoft SQL Server error log.  

- Sites or clients that haven't reported status in a long time.  

- Sluggish response from the SQL Server database.  

- Signs of hardware failure.  

If monitoring tasks reveal any signs of problems, investigate the source of the problem. Then quickly repair it to minimize the risk of a site failure.  


## <a name="BKMK_MonintorMgmtTasks"></a> Monitor common management tasks

Configuration Manager provides built-in monitoring from within the Configuration Manager console.

### Alerts

For more information, see [Monitor alerts](configure-alerts.md#monitor-alerts).  

### Compliance settings

For more information, see [How to monitor compliance settings](../../../compliance/deploy-use/monitor-compliance-settings.md).

### Content

For general information about monitoring content, see [Manage content and content infrastructure](../deploy/configure/manage-content-and-content-infrastructure.md).  

For more information about monitoring specific types of content:

- [Monitor applications](../../../apps/deploy-use/monitor-applications-from-the-console.md)

- [Monitor packages and programs](../../../apps/deploy-use/packages-and-programs.md#monitor-packages-and-programs)  

- [Monitor content for software updates](../../../sum/deploy-use/monitor-software-updates.md#BKMK_MonitorContent)

- [Monitor content for OS deployments](../../../osd/deploy-use/monitor-operating-system-deployments.md#BKMK_MonitorContent)

### Endpoint Protection

For more information, see [How to monitor Endpoint Protection](../../../protect/deploy-use/monitor-endpoint-protection.md).  

### OS deployment

For more information, see [Monitor OS deployments](../../../osd/deploy-use/monitor-operating-system-deployments.md).

### Monitor power management

For more information, see [How to monitor and plan for power management](../../clients/manage/power/monitor-and-plan-for-power-management.md).  

### Monitor software metering

For more information, see [Monitor app usage with software metering](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

### Monitor software updates

For more information, see [Monitor software updates](../../../sum/deploy-use/monitor-software-updates.md).  


## <a name="BKMK_SH_Node"></a> Monitor the site hierarchy

The **Site Hierarchy** node of the **Monitoring** workspace provides you with an overview of your Configuration Manager hierarchy and intersite links. 

Use the **Site Hierarchy** node to monitor the health of each site. Also monitor the intersite replication links and their relationship to external factors, such as a geographical location.  

Both site status and intersite link status replicate as site data and not global data. When you connect your Configuration Manager console to a child primary site, you can't view the site or link status for other primary sites or their child secondary sites. For example, in a hierarchy with multiple primary sites, when you connect the console to a primary site, you can view the status of child secondary sites, the primary site, and the central administration site. From this view, you can't see the status for other sites below the central administration site.  

To control the display in the **Site Hierarchy** node, use the **Configure Settings** action. The hierarchy replicates the settings that you configure in this node.  

### Hierarchy diagram

The hierarchy diagram displays your sites in a topology map. Select a site, and view a status message summary from that site. Drill through to view status messages, and access the site **Properties**.  

To view high-level status for a site or replication link between sites, hover your mouse pointer over the object. Replication link status doesn't replicate globally. To view the replication link details between all primary sites in a hierarchy, connect the console to the central administration site.  

The following options modify the hierarchy diagram:  

#### Groups

Configure the number of primary sites and secondary sites that trigger a change in the hierarchy diagram. This change in the display combines the sites into a single object. Then you see the total number of sites and a high-level rollup of status messages and site status.

#### Favorite sites

Specify individual sites to be a favorite site. A star icon identifies a favorite site in the hierarchy diagram. Favorite sites aren't combined with others sites when you use groups. They're always displayed individually.  

### Geographical view

> [!IMPORTANT]
> Starting in August 2020, this feature is deprecated. Use the **Hierarchy Diagram** option.<!--8116777-->

The geographical view displays the location of each site on a geographical map. It only displays sites that you configure with a location. When you select a site in this view, it shows replication links to parent or child sites. Unlike the hierarchy diagram view, you can't display site status message or replication link details in this view.  

> [!NOTE]  
> To use the geographical view, the computer to which your Configuration Manager console connects must have Internet Explorer installed and be able to access Bing Maps by using the HTTP protocol.  

The following option modifies the geographical view:  

#### Site Location

Specify a geographical location for each site using one of the following types:

- A street address
- A place name such as the name of a city
- By latitude and longitude coordinates

For example, to use the latitude and longitude of Redmond, Washington, specify **N 47 40 26.3572 W 122 7 17.4432** as the location of the site. You don't need to specify the symbols for the degree, minutes, or seconds of latitude or longitude. Configuration Manager uses Bing Maps to display the location on the geographical view. Then you can view your hierarchy with the geographical locations. This view provides insight into regional issues that might affect specific sites or intersite replication.  

When you specify a location, you can use the **Location** box to search for a specific site in your hierarchy. With the site selected, enter the location as a city name or street address in the **Location** column. Configuration Manager uses Bing Maps to resolve the location.  

<a name="BKMK_MonitorRepLinksAndStatuss"></a>

## Next steps

[Monitor database replication](monitor-replication.md)
