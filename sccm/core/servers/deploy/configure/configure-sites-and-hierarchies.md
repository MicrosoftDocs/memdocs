---
title: Configure sites and hierarchies
titleSuffix: Configuration Manager
description: Consult this checklist to ensure you consider the most common configurations that affect both sites and hierarchies.
ms.date: 07/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9efb4061-f642-48bd-8332-3357ff5b3118
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Configure sites and hierarchies for Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

After you install your first Configuration Manager site or add additional sites to your hierarchy, use this checklist to ensure that you consider the most common configurations that affect both sites and hierarchies.  

The following configuration notes apply to most deployments:  

- Some options build upon each other, such as Active Directory Forest Discovery, boundaries, and boundary groups.  

- Several configurations have default values to use without configuration changes, at least to start.  

- Other configurations, like boundary groups and distribution point groups, require you to configure them before using.  

| Action | Details |  
|------------|-------------|  
| Configure role-based administration | Segregate administrative assignments to control which administrative users can view and manage different objects and data in your Configuration Manager environment.<br /><br /> Configurations for role-based administration are shared with all sites in a hierarchy.   <br/><br/>For more information, see [Configure role-based administration](/sccm/core/servers/deploy/configure/configure-role-based-administration). |  
| Publish site data to Active Directory Domain Services | Make it easy for clients to find services and efficiently use site resources.<br /><br /> First [extend the Active Directory schema](/sccm/core/plan-design/network/extend-the-active-directory-schema). Then individually configure each site to [publish site data](/sccm/core/servers/deploy/configure/publish-site-data) |  
| Configure a service connection point | Plan to install and configure the service connection point at the top-level site of your hierarchy. For more information, see [About the service connection point](/sccm/core/servers/deploy/configure/about-the-service-connection-point). |  
| Add site system roles | Install one or more additional site system roles for individual sites. For more information, see [Add site system roles](/sccm/core/servers/deploy/configure/add-site-system-roles). |  
| Configure site boundaries and boundary groups | Specify boundaries that define network locations on your intranet that can contain devices that you want to manage. Then configure boundary groups so that clients at those network locations can find Configuration Manager resources. For more information, see [Define site boundaries and boundary groups](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups). |  
| Configure distribution point groups | Configure logical groups of distribution points to make managing deployments easier. For more information, see [Manage distribution point groups](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_manage). |  
| Run discovery | Run discovery to find resources on your network, including network infrastructure, devices, and users.<br /><br /> For more information, see [Run discovery](/sccm/core/servers/deploy/configure/run-discovery). |  
| Add redundancy and capacity for administrators | Install additional SMS Providers and Configuration Manager consoles to expand capacity for administrators to manage your infrastructure:<br /><br /> **Install additional SMS providers** to provide redundancy for console and API connections to the site. For more information, see [Manage the SMS Provider](/sccm/core/servers/manage/modify-your-infrastructure#BKMK_ManageSMSprovider).<br /><br /> **Install additional Configuration Manager consoles** to provide access to additional administrative users. For more information, see [Install Configuration Manager consoles](/sccm/core/servers/deploy/install/install-consoles). |  
| Configure site components | Configure site components at each site to modify the behavior of site system roles and site status reporting. For more information, see [Site components](/sccm/core/servers/deploy/configure/site-components). |  
| Create custom collections | Using information that the site discovers about devices and users, create custom collections of objects to simplify future management tasks. For more information, see [How to create collections](/sccm/core/clients/manage/collections/create-collections). |  
| Configure settings to manage high-risk deployments | Configure settings at a site to warn administrators when they create a high-risk deployment. For more information, see [Settings to manage high-risk deployments](/sccm/core/servers/manage/settings-to-manage-high-risk-deployments). |  
| Configure database replicas for management points | Configure a database replica to reduce the processor load that's placed on the site database server by management points as they service requests from clients. For more information, see [Database replicas for management points](/sccm/core/servers/deploy/configure/database-replicas-for-management-points). |  
| Configure a SQL Server Always On availability group | Configure availability groups as high-availability and disaster-recovery solutions for hosting the site database at primary sites and the central administration site. For more information, see [SQL Server AlwaysOn for a highly available site database](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database). |  
| Modify replication between sites | See [Data transfers between sites](/sccm/core/servers/manage/data-transfers-between-sites) to learn about the following subjects:<br /><br /> Configure [file-based replication](/sccm/core/servers/manage/data-transfers-between-sites#bkmk_fileroute) between secondary sites<br /><br /> Configure [database replication links](/sccm/core/servers/manage/data-transfers-between-sites#bkmk_Dblinks)<br /><br /> Configure [distributed views](/sccm/core/servers/manage/data-transfers-between-sites#bkmk_distviews) |  
| Configure site servers in passive mode | Starting in version 1806, configure a site server in passive mode for each primary site and the central administration site. This feature provides a highly available site server. For more information, see [Site server high availability](/sccm/core/servers/deploy/configure/site-server-high-availability). |  
