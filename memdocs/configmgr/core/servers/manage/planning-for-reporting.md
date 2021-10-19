---
title: Plan for reporting
titleSuffix: Configuration Manager
description: From installation details to security and network bandwidth, it's important to plan for reporting in Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.localizationpriority: medium
---

# Plan for reporting in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Reporting in Configuration Manager provides a set of tools and resources that help you use the advanced reporting capabilities of SQL Server Reporting Services or Power BI Report Server. Use the following sections to help you plan for reporting in Configuration Manager.

## Where to install the reporting services point

When you run Configuration Manager reports at a site, the reports have access to the information in the site database in which it connects. Use the following sections to help you determine where to install the reporting services point and what data source to use.

> [!NOTE]
> For more information about planning for site systems in Configuration Manager, see [Add site system roles](../deploy/configure/add-site-system-roles.md).

### Supported site system servers

You can install the reporting services point on a central administration site (CAS) and primary sites. It works on multiple site systems at a site, and at other sites in the hierarchy. Configuration Manager doesn't support the reporting services point at secondary sites. The first reporting services point at a site is set as the default report server. You can add more reporting services points at a site, but Configuration Manager reports actively use the default report server at each site. Install the reporting services point on the site server or a remote site system. For best performance, use SQL Server Reporting Services on a remote site system server.

### Data replication considerations

Consider the following factors to help you determine where to install your reporting services points:

- A reporting services point with the CAS database as its reporting data source has access to all global and site data in the Configuration Manager hierarchy. If you require reports that contain site data for multiple sites in a hierarchy, consider installing the reporting services point on a site system at the CAS. Then use its database as the reporting data source.

- A reporting services point with a child primary site database as its reporting data source has access to global data and site data for only the local primary site and any child secondary sites. Site data for other primary sites in the Configuration Manager hierarchy doesn't replicate to this primary site. Reporting Services can't access site data for other primary sites. If you require reports that contain site data for a specific primary site or global data, and you don't want the user to have access to site data from other primary sites, install a reporting services point on a site system at the primary site. Then use the primary site's database as the reporting data source.

For more information on global and site data, see [Types of data](../../plan-design/hierarchy/database-replication.md#types-of-data).

### Network bandwidth considerations

Depending on how you configure the site, site systems in the same site communicate with each other by using server message block (SMB), HTTP, or HTTPS. Configuration Manager doesn't manage this communication. It can occur at any time without network bandwidth control. Review your available network bandwidth before you install the reporting services point role on a site system.

For more information about planning for site systems, see [Add site system roles](../deploy/configure/add-site-system-roles.md).

## Plan for role-based administration

Security for reporting is much like other objects in Configuration Manager where you can assign security roles and permissions to administrative users. Administrative users can only run and modify reports for which they have appropriate security rights. To run reports in the Configuration Manager console, users need the **Read** right for the **Site** permission and the permissions configured for specific objects.

Unlike other objects in Configuration Manager, the security rights that you set for administrative users in the Configuration Manager console are also configured in Reporting Services. When you configure security rights in the Configuration Manager console, the reporting services point connects to Reporting Services and sets appropriate permissions for reports.

For example, the **Software Update Manager** security role has the **Run Report** and **Modify Report** permissions. Users with the **Software Update Manager** role can only run and modify reports for software updates. The Configuration Manager console doesn't display reports for other objects to this role. The exception to this behavior is that some reports aren't associated with specific Configuration Manager securable objects. For these reports, the administrative user must have the **Read** right for the **Site** permission to run the reports and the **Modify** right for the **Site** permission to modify the reports.  

> [!IMPORTANT]
> For users from a different domain than that of the reporting services point account to successfully run reports, establish a two-way trust between the two domains.

Reports are fully enabled for role-based administration. Configuration Manager filters the data for all included reports based on the permissions of the user who runs the report. Users with specific roles can only view information defined for their roles.

For more information about security rights for reporting, see [Configure reporting](configuring-reporting.md).

For more information about role-based administration in Configuration Manager, see [Configure role-based administration](../deploy/configure/configure-role-based-administration.md).

## Reporting recommendations

Consider the following recommendations and tips for reporting in Configuration Manager:

- For best performance, install the reporting services point on a remote site system. Although you can install it on the site server, the reporting services point performs best when you install it on a remote site system. When this role does background processing, it can compete for system resources with other roles. There are many variables to consider with site and role performance, but in general this configuration improves reporting and overall site performance.

- Optimize SQL Server Reporting Services queries. Typically any reporting delays are because of the time it takes to run queries and retrieve the results. Microsoft SQL Server tools such as Query Analyzer and Profiler can help you optimize queries.

- Schedule report subscription processing to run outside standard office hours. Whenever possible, processing subscriptions during off-hours can minimize the CPU processing on the Configuration Manager site database server. This practice also improves availability for unpredicted report requests.

- Site updates preserve built-in reports. If you modify a standard report, when the site updates, it renames the report with an underscore prefix (`_`). This behavior makes sure that the site update doesn't overwrite the modified report by the standard report.

## Security and privacy

Configuration Manager reports display information that it collects during standard Configuration Manager management operations. For example, you can display a report of information that Configuration Manager collected from discovery or inventory. Reports can also contain the current status information for client management operations, such as deploying software, and checking for compliance.

For more information about any security recommendations and privacy information for Configuration Manager operations that might generate data that you can view in reports, see [Security and privacy for Configuration Manager](../../../security/index.yml).  

## Next steps

[Prerequisites for reporting](prerequisites-for-reporting.md)