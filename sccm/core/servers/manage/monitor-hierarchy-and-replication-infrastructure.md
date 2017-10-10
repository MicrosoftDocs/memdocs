---
title: "Monitor replication"
titleSuffix: "Configuration Manager"
description: "Learn how to monitor infrastructure and operations in Configuration Manager by using the Monitoring workspace in the console."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3fab4d67-8d2a-45ce-8b06-471280102cf6
caps.latest.revision: 11
caps.handback.revision: 0
author: Brendunsms.author: brendunsmanager: angrobe

---
# Monitor hierarchy and replication infrastructure in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
To monitor infrastructure and operations in System Center Configuration Manager, use the **Monitoring** workspace in the Configuration Manager console.  

> [!NOTE]  
>  The exception to this location is Migration, which is monitored directly in the **Migration** node in the **Administration** workspace. For more information, see [Operations for migrating to System Center Configuration Manager](../../../core/migration/operations-for-migration.md).  

 In addition to using the Configuration Manager console for monitoring, you can use the Configuration Manager reports, or view Configuration Manager log files for Configuration Manager components. For information about reports, see [Reporting in System Center Configuration Manager](../../../core/servers/manage/reporting.md). For information about log files, see [Log files in System Center Configuration Manager](../../../core/plan-design/hierarchy/log-files.md).  

 When you monitor sites, look for signs that indicate problems that require you to take action. For example:  

-   A backlog of files on site servers and site systems.  

-   Status messages that indicate an error or a problem.  

-   Failing intrasite communication.  

-   Error and warning messages in the system event log on servers.  

-   Error and warning messages in the Microsoft SQL Server error log.  

-   Sites or clients that have not reported in a long time.  

-   Sluggish response from the SQL Server database.  

-   Signs of hardware failure.  

To minimize the risk of a site failure, if monitoring tasks reveal any signs of problems, investigate the source of the problem and repair it as soon as possible.  



##  <a name="BKMK_MonintorMgmtTasks"></a> Monitor  common management tasks for Configuration Manager  
 Configuration Manager provides built-in monitoring from within the Configuration Manager console. You can monitor many tasks including those related to software updates, power management, and the deployment of content throughout your hierarchy.  

 Use the following information to help you monitor common Configuration Manager tasks:  

 **Alerts**  
   See [Monitor alerts](../../../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorAlerts) in [Use alerts and the status system for System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

 **Compliance Settings**  
   See [How to monitor compliance settings in System Center Configuration Manager](../../../compliance/deploy-use/monitor-compliance-settings.md).  

 **Content Deployment**  
   For general information about monitoring content, see [Manage content and content infrastructure for System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

For information about monitoring specific types of content deployment:
-   To monitor Applications, see [Monitor applications with System Center Configuration Manager](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

-   To monitor Packages and Programs, see How to manage packages and programs   in [Packages and programs in System Center Configuration Manager](../../../apps/deploy-use/packages-and-programs.md).  

**Endpoint Protection**  
   See [How to monitor Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/monitor-endpoint-protection.md).  

**Monitor Power Management**  
 See [How to monitor and plan for power management in System Center Configuration Manager](../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).  

**Monitor Software Metering**  
See [Monitor app usage with software metering in System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

**Monitor Software Updates**  
 See [Monitor software updates in System Center Configuration Manager](../../../sum/deploy-use/monitor-software-updates.md).  


##  <a name="BKMK_MonitorInfrastructure"></a> Monitor hierarchy infrastructure for Configuration Manager  
Configuration Manager provides several methods to monitor the status and operations of your hierarchy. You can check system status of sites throughout the hierarchy, monitor intersite replication from a site hierarchy or geographical view, monitor replication links between sites for database replication, and use the Replication Link Analyzer tool to remediate replication issues.  

###  <a name="BKMK_SH_Node"></a> About the Site Hierarchy node  
The **Site Hierarchy** node of the **Monitoring** workspace provides you with an overview of your Configuration Manager hierarchy and intersite links. You can use two views:  

-   **Hierarchy Diagram**: This view displays your hierarchy as a topology map that has been simplified to show only vital information.  

-   **Geographical View**: This view displays your sites on a geographical map showing site locations that you configure.  

Use the **Site Hierarchy** node to monitor the health of each site and the intersite replication links and their relationship to external factors, such as a geographical location.  

Because site status and intersite link status replicate as site data and not global data, when you connect your Configuration Manager console to a child primary site, you cannot view the site or link status for other primary sites or their child secondary sites. For example, in a multi-primary site hierarchy, when your Configuration Manager console connects to a primary site, you can view the status of child secondary sites, the primary site, and the central administration site, but you cannot see the status for other nodes of the hierarchy below the central administration site.  

 Use the **Configure Settings** command to control how the site hierarchy display renders. Configurations to the **Site Hierarchy** node that you make when your Configuration Manager console is connected to one site are replicated to all other sites.  

#### Hierarchy diagram  
 The hierarchy diagram displays your sites in a topology map. In this view, you can select a site and view a status message summary from that site, drill through to view status messages, and access the **Properties** dialog box of the sites.  

 Additionally, you can pause the mouse pointer on a site or replication link between sites to view high-level status for that object. Because replication link status does not replicate globally, in a hierarchy with multiple primary sites, you must connect your Configuration Manager console to the central administration site to view the replication link details between all sites.  

 The following options modify the hierarchy diagram:  

-   **Groups**: You can configure the number of primary sites and secondary sites that trigger a change in the hierarchy diagram display that combines the sites into a single object. When sites are combined into a single object, you see the total number of sites and a high-level rollup of status messages and site status. Group configurations do not affect the geographical view.  

-   **Favorite sites**: You can specify individual sites to be a favorite site. A star icon identifies a favorite site in the hierarchy diagram. Favorite sites are not combined with others sites when you used groups and always are displayed individually.  

#### Geographical view  
 The geographical view displays the location of each site on a geographical map. Only sites that you configure with a location are displayed. When you select a site in this view, replication links to parent or child sites are shown. Unlike the hierarchy diagram view, you cannot display site status message or replication link details in this view.  

> [!NOTE]  
>  To use the geographical view, the computer to which your Configuration Manager console connects must have Internet Explorer installed and be able to access Bing Maps by using the HTTP protocol.  

The following option modifies the geographical view.  

-   **Site Location**: You can specify a geographical location for each site. You can specify the location as a street address, a place name such as the name of a city, or by latitude and longitude coordinates. For example, to use the latitude and longitude of Redmond Washington, you would specify **N 47 40 26.3572 W 122 7 17.4432** as the location of the site. You do not need to specify the symbols for the degree, minutes or seconds of longitude or latitude. Configuration Manager uses Bing Maps to display the location on the geographical view. This provides you the option to view your hierarchy in relation to a geographical location, which can provide insight into regional issues that might affect specific sites or intersite replication.  

     When you specify a location, you can use the **Location** box to search for a specific site in your hierarchy. With the site selected, enter the location as a city name or street address in the **Location** column. Configuration Manager uses Bing Maps to resolve the location.  

###  <a name="BKMK_MonitorRepLinksAndStatuss"></a> How to monitor database replication links and replication status  
 In addition to high level details that are accessible from the **Site Hierarchy** node in the **Monitoring** workspace. You can also monitor details for database replication when you use the **Database Replication** node in the **Monitoring** workspace. From the **Database Replication** you can monitor the status of replication links between sites, and the initialization details and replication details for replication groups at the site to which your  Configuration Manager console is connected.  

> [!TIP]  
>  Although a **Database Replication** node also appears under the **Hierarchy Configuration** node in the **Administration** workspace, you cannot view the replication status for database replication links from that location.  

####  <a name="BKMK_MonitorReplicationLinks"></a> Replication link status  
Database replication between sites involves the replication of several sets of information, called replication groups. Each replication group replicates with different replication priorities. By default, the data contained in a replication group and the frequency of replication cannot be modified.  

 When a replication link is active, and does not have a status of failed or degraded, all replication groups replicate in a timely manner. When one or more replication groups fail to complete replication in the expected period of time, the link displays as degraded. Degraded links can still function, but you should monitor them to ensure that they return to active status, or investigate them to ensure that additional degradation or replication failures do not occur.  

 For each replication link you can specify the number of times that an unsuccessfully replicated replication group retries to replicate before the status of the link is set to degraded or failed. Even if all but one replication group replicate successfully, the status of the link is set to degraded or failed because the one replication group fails to complete replication in the specified number of attempts. For information about replication thresholds, see the [Database Replication Thresholds](../../../core/servers/manage/data-transfers-between-sites.md#BKMK_DBRepThresholds) section in  [Data transfers between sites in System Center Configuration Manager](../../../core/servers/manage/data-transfers-between-sites.md).  

 Use the information in following table to understand the status of replication links that might require further investigation.  

|Link description|More information|  
|----------------------|----------------------|  
|**Link is active**|No problems have been detected, and communication across the link is current.|  
|**Link is degraded**|Replication is functional, but at least one replication object or group is delayed. Monitor links that are in this state and review information from both sites on the link for indications that the link might fail.<br /><br /> A link can also display a status of degraded when the site that receives replicated data is unable to quickly commit the data to the database. This can happen when large volumes of data replicate. For example, if you deploy a software update to a large number of computers, the volume of data that replicates might take some time to be processed by the parent site on the link. A processing lag at the parent site can result in the link status being set to degraded until the parent site can successfully process the backlog of data.|  
|**Link has failed**|Replication is not functional. It is possible that a replication link might recover without further action. You can use the Replication Link Analyzer to investigate and help remediate replication on this link.<br /><br /> This status can also indicate a problem with the physical network between the parent and child site on the replication link.|  

 While a parent site is in the process of upgrading to a new service pack and you view the link status from the child site, the link status displays as active. After the upgrade, until the child site is also at the same service pack as the parent site, the link status displays as active when viewed from the parent site, and as being configured when viewed from the child site.  

####  <a name="BKMK_MonitorReplicationStatus"></a> Replication status  
 You can use the **Database Replication** node in the **Monitoring** workspace to view the status of replication for a replication link, and view details about the site database at each site on the replication link. You can also view details about replication groups. To view details, select a replication link, and then select the appropriate tab for the replication status you want to view. The following are details about the different tabs for replication status.  

 **Summary**  
 View high level information about the replication of site data and global data between the two sites on a link.  

 You can also click **View reports for historical traffic data** to view a report that shows details about the network bandwidth used by replication across the replication link.  

 **Parent Site**  
 For the parent site on a replication link, view details about the database, which include:  

-   Firewall ports for the SQL Server  

-   Free disk space  

-   Database file locations  

-   Certificates  

**Child Site**  
 For the child site on a replication link, view details about the database, which include:  

-   Firewall ports for the SQL Server  

-   Free disk space  

-   Database file locations  

-   Certificates  

**Initialization Detail**    
 View the initialization status for replication groups that replicate across the replication link. This information can help you identify when initialization of replication data is in progress or has failed.  

 Additionally, You can use this information to identify when a site might be in interoperability mode. Interoperability mode occurs when the child site does not run the same version of Configuration Manager as the parent site.  

**Replication Detail**    
 View the replication status for each replication group that replicates across the link. Use this information to help identify problems or delays for the replication of specific data, and to help determine the appropriate database replication thresholds for this link. For information about database replication thresholds, see the [Database Replication Thresholds](../../../core/servers/manage/data-transfers-between-sites.md#BKMK_DBRepThresholds) section in  [Data transfers between sites in System Center Configuration Manager](../../../core/servers/manage/data-transfers-between-sites.md).  

> [!TIP]  
>  Replication groups for site data are sent only from the child site to the parent site. Replication groups for global data replicate in both directions.  

###  <a name="BKMK_RLA"></a> About the Replication Link Analyzer  
 Configuration Manager includes **Replication Link Analyzer** which you use to analyze and repair replication issues. You can use Replication Link Analyzer to remediate replication link failures when replication has failed and when replication stops working but has not yet been reported as failed. Replication Link Analyzer can be used to remediate replication issues between the following computers in the Configuration Manager hierarchy (the direction of the replication failure does not matter):  

-   Between a site server and the site database server.  

-   Between a sites site database server and another sites site database computer (intersite replication).  

You can run Replication Link Analyzer in either the Configuration Manager console or at a command prompt:  

-   To run in the Configuration Manager console: In the **Monitoring** workspace, click the **Database Replication** node, select the replication link that you want to analyze, and then in the **Database Replication** group on the **Home** tab, select **Replication Link Analyzer**.  

-   To run at a command prompt, type the following command: **%path%\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManager.ReplicationLinkAnalyzer.Wizard.exe &lt;source site server FQDN\> &lt;destination site server FQDN\>**  

When you run Replication Link Analyzer, it detects problems by using a series of diagnostic rules and checks. When the tool runs, you can view the problems that the tool identifies. When instructions to resolve an issue are known, they are displayed. If Replication Link Analyzer can automatically remediate a problem, you are presented with that option. When Replication Link Analyzer finishes, it saves the results in the following XML-based report and a log file on the desktop of the user who runs the tool:  

-   ReplicationAnalysis.xml  

-   ReplicationLinkAnalysis.log  

When Replication Link Analyzer runs, it stops the following services while it remediates some problems, and restarts these services when remediation is complete:  

-   SMS_SITE_COMPONENT_MANAGER  

-   SMS_EXECUTIVE  

If Replication Link Analyzer fails to complete remediation, review the site server and restart these services if they are stopped.  

Successful and unsuccessful investigation and remediation actions are logged to provide additional details that are not presented in the tool interface.  

**Prerequisites to use the Replication Link Analyzer:**  

-   The account that you use to run the Replication Link Analyzer must have local administrator rights on each computer that is involved in the replication link. The account does not require a specific role-based administration security role. Therefore, an administrative user with access to the **Database Replication** node can run the tool in the Configuration Manager console, or a system administrator with sufficient rights to each computer can run the tool at a command prompt.  

-   The account that you use to run the Replication Link Analyzer must have sysadmin rights on each SQL Server database that is involved in the replication link.  

**Known issues for the Replication Link Analyzer:**  

-   With the release of System Center Configuration Manager version 1511, the replication link analyzer generates SQL Server Service Broker certificate errors for primary sites that upgraded from System Center 2012 Configuration Manager. This is due to changes in the names of the certificates introduced with version 1511 for which Replication Link Analyzer has not yet been updated. These errors can be safely ignored.  

###  <a name="BKMK_ProcsforMonitoringReplication"></a> Procedures for monitoring database replication  

##### To monitor high-level site-to-site database replication status    
1.  In the Configuration Manager console, click **Monitoring**.  

2.  In the **Monitoring** workspace, click **Site Hierarchy** to open the **Hierarchy Diagram** view.  

3.  Briefly pause the mouse pointer on the line between the two sites to view the status of global and site data replication for these sites.  

##### To monitor the replication status for a replication link    
1.  In the Configuration Manager console, click **Monitoring**.  

2.  In the **Monitoring** workspace, click **Database Replication**, and then select the replication link for the link that you want to monitor. Then, in the workspace, select the appropriate tab to view different details about the replication status for that link.  
