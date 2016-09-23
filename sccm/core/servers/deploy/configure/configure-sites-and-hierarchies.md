---
title: "Configure sites and hierarchies for System Center Configuration Manager"
ms.custom: na
ms.date: 07/22/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9efb4061-f642-48bd-8332-3357ff5b3118
caps.latest.revision: 15
author: Brenduns

---
# Configure sites and hierarchies for System Center Configuration Manager
After you install your first System Center Configuration Manager site or add additional sites to your hierarchy, use the following checklist to ensure you consider the most common configurations that affect both sites and hierarchies.  

## Checklist of common configurations for new and additional sites  
 In most deployments you will not need to configure the following options in any specific order:  

-   Some options build upon each other, such Active Directory Forest Discovery, boundaries,  and boundary groups.  

-   Several configurations have default values you can use without configuration changes, at least temporarily.  

-   Other configurations, like boundary groups and distribution point groups, require you to configure them before you can use them.  

|Action|Details|  
|------------|-------------|  
|Configure role-based administration|Role-based administration is how you to segregate administrative assignments to control which administrative users can view and manage different objects and data in your Configuration Manager environment.<br /><br /> Configurations for role-based administration are shared with all sites in a hierarchy.   <br />See [Configure role-based administration for System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md)|  
|Publish site data to Active Directory Domain Services (AD DS)|When you publish site data to AD DS, you make it easy for clients to find services and make efficient use of site resources.<br /><br /> You must first [Extend the Active Directory schema for System Center Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md), and then each site must be configured to [Publish site data for System Center Configuration Manager](../../../../core/servers/deploy/configure/publish-site-data.md) individually.|  
|Configure a service connection point|At the top-tier site of your hierarchy you should plan to install and configure the service connection point. For information, see [About the service connection point in System Center Configuration Manager](../../../../core/servers/deploy/configure/about-the-service-connection-point.md).|  
|Add site system roles|Install one or more additional site system roles to individual sites.  See [Add site system roles for System Center Configuration Manager](../../../../core/servers/deploy/configure/add-site-system-roles.md)|  
|Configure site boundaries and boundary groups|Specify boundaries that define network locations on your intranet that can contain devices that you want to manage, and then configure boundary groups so that clients at those network locations can find Configuration Manager services resources. See [Define site boundaries and boundary groups for System Center Configuration Manager](../../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md)|  
|Configure distribution point groups|Configure logical  groups of distribution points to make managing deployments easier. See [Manage distribution point groups](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) in [Install and configure distribution points for System Center Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md).|  
|Run Discovery|Run discovery to find resources on your network including network infrastructure, devices, and users.<br /><br /> See [Run discovery for System Center Configuration Manager](../../../../core/servers/deploy/configure/run-discovery.md)|  
|Add redundancy and capacity for those who manage your infrastructure|You can install additional SMS Providers and Configuration Manager consoles to expand capacity for administrators to manage your infrastructure:<br /><br /> **Install additional SMS Providers** to provide redundancy for contact points to administer your site and hierarchy. See [Manage the SMS Provider](../../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider) in [Modify your System Center Configuration Manager infrastructure](../../../../core/servers/manage/modify-your-infrastructure.md)<br /><br /> **Install additional Configuration Manager consoles** to provide access to additional administrative users at the same time. See [Install Configuration Manager consoles](../../../../core/servers/deploy/install/install-consoles.md)|  
|Configure site components|You can configure site components at each site to modify the behavior of site system roles and site status reporting. See [Site components for System Center Configuration Manager](../../../../core/servers/deploy/configure/site-components.md)|  
|Create custom collections|Using information that is discovered about devices and users, create custom collections of objects to simplify future management tasks. See [How to create collections in System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md)|  
|Configure settings to manage high-risk deployments|Configure settings at a site that will warn administrative users when they create a high-risk task sequence deployment.  See [Settings to manage high-risk deployments for System Center Configuration Manager](../../../../protect/understand/settings-to-manage-high-risk-deployments.md)|  
|Configure database replicas for management points|Configure a database replica to reduce the CPU load placed on the site database server by management points as they service requests from clients. See [Database replicas for management points for System Center Configuration Manager](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md)|  
|Configure a SQL Server AlwaysOn Availability Group to host the site database|Beginning with version 1602, you can configure availability groups as a high-availability and disaster-recovery solution for hosting the site database at primary sites and the central administration site. See [SQL Server AlwaysOn for a highly available site database for System Center Configuration Manager](../../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)|  
|Modify replication between sites|See [Data transfers between sites in System Center Configuration Manager](../../../../core/servers/manage/data-transfers-between-sites.md) to learn about the following subjects:<br /><br /> Configure [File-based replication](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_fileroute) between secondary sites<br /><br /> Configure [Database replication links](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_Dblinks)<br /><br /> Configure [Distributed views](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_distviews)|  

