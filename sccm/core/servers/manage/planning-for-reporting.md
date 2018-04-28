---
title: "Planning for reporting"
titleSuffix: "Configuration Manager"
description: "From installation details to security and network bandwidth, it's important to plan for reporting in Configuration Manager."
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ff920c84-d5c8-458c-b67f-bc7219b05690
author: aczechowski
manager: dougeby
ms.author: aaroncz
---
# Planning for reporting in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
Reporting in System Center Configuration Manager provides a set of tools and resources that help you use the advanced reporting capabilities of SQL Server Reporting Services. Use the following sections to help you plan for reporting in Configuration Manager.  

##  <a name="BKMK_InstallReportingServicesPoint"></a> Determine where to install the Reporting Services Point  
 When you run Configuration Manager reports at a site, the reports have access to the information in the site database in which it connects. Use the following sections to help you determine where to install the reporting services point and what data source to use.  

> [!NOTE]  
>  For more information about planning for site systems in Configuration Manager, see [Add site system roles](../deploy/configure/add-site-system-roles.md).  

###  <a name="BKMK_SupportedSiteServers"></a> Supported site system servers  
 You can install the reporting services point on a central administration site and primary sites, and on multiple site systems at a site and at other sites in the hierarchy. The reporting services point is not supported on secondary sites. The first reporting services point at a site is configured as the default report server. You can add more reporting services points at a site, but the default report server at each site is actively used for Configuration Manager reports. You can install the reporting services point on the site server or a remote site system. However, as a best practice for performance reasons, use Reporting Services on a remote site system server.  

###  <a name="BKMK_DataReplication"></a> Data replication considerations  
 Configuration Manager classifies the data that it replicates as either global data or site data. Global data refers to objects that were created by administrative users and that are replicated to all sites throughout the hierarchy, while secondary sites receive only a subset of global data. Examples of global data include software deployments, software updates, collections, and role-based administration security scopes. Site data refers to operational information that Configuration Manager primary sites and the clients that report to primary sites create. Site data replicates to the central administration site but not to other primary sites. Examples of site data include hardware inventory data, status messages, alerts, and the results from query-based collections. Site data is only visible at the central administration site and the primary site where the data originates.  

 Consider the following factors to help you determine where to install your reporting services points:  

-   A reporting services point with the central administration site database as its reporting data source has access to all global and site data in the Configuration Manager hierarchy. If you require reports that contain site data for multiple sites in a hierarchy, consider installing the reporting services point on a site system at the central administration site and use the central administration site's database as the reporting data source.  

-   A reporting services point with the child primary site database as its reporting data source has access to global data and site data for only the local primary site and any child secondary sites. Site data for other primary sites in the Configuration Manager hierarchy is not replicated to the primary site, and therefore Reporting Services cannot access it. If you require reports that contain site data for a specific primary site or global data, but you do not want the report user to have access to site data from other primary sites, install a reporting services point on a site system at the primary site and use the primary site's database as the reporting data source.  

###  <a name="BKMK_NetworkBandwidth"></a> Network bandwidth considerations  
 Site system servers in the same site communicate with each other by using server message block (SMB), HTTP, or HTTPS, depending on how you configure the site. Because these communications are unmanaged and can occur at any time without network bandwidth control, review your available network bandwidth before you install the reporting services point role on a site system.  

> [!NOTE]  
>  For more information about planning for site systems, see [Add site system roles](../deploy/configure/add-site-system-roles.md).  

##  <a name="BKMK_RoleBaseAdministration"></a> Planning for role-based administration for reports  
 Security for reporting is much like other objects in Configuration Manager where you can assign security roles and permissions to administrative users. Administrative users can only run and modify reports for which they have appropriate security rights. To run reports in the Configuration Manager console, you must have the **Read** right for the **Site** permission and the permissions configured for specific objects.  

 However, unlike other objects in Configuration Manager, the security rights that you set for administrative users in the Configuration Manager console must also be configured in Reporting Services. When you configure security rights in the Configuration Manager console, the reporting services point connects to Reporting Services and sets appropriate permissions for reports. For example, the **Software Update Manager** security role has the **Run Report** and **Modify Report** permissions associated with it. Administrative users who are only assigned the **Software Update Manager** role can only run and modify reports for software updates. Reports for other objects are not displayed in the Configuration Manager console. The exception to this is that some reports are not associated with specific Configuration Manager securable objects. For these reports, the administrative user must have the **Read** right for the **Site** permission to run the reports and the **Modify** right for the **Site** permission to modify the reports.  

 Reports are fully enabled for role-based administration. The data for all reports included with Configuration Manager is filtered based on the permissions of the administrative user who runs the report. Administrative users with specific roles can only view information defined for their roles.  

 For more information about security rights for reporting, see [Configure reporting](configuring-reporting.md).  

 For more information about role-based administration in Configuration Manager, see [Configure role-based administration](../deploy/configure/configure-role-based-administration.md).  

## Next steps  
 Use the following additional topics to help you plan for reporting in Configuration Manager:  

-   [Prerequisites for reporting in System Center Configuration Manager](../../../core/servers/manage/prerequisites-for-reporting.md)  
-   [Best practices for reporting in System Center Configuration Manager](../../../core/servers/manage/best-practices-for-reporting.md)  
