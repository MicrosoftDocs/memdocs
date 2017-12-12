---
title: "Design a site hierarchy "
titleSuffix: "Configuration Manager"
description: "Understand the available topologies and management options for System Center Configuration Manager so you can plan your site hierarchy."
ms.custom: na
ms.date: 8/24/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 07ce872e-1558-42ad-b5ad-582c5b1bdbb4
caps.latest.revision: 22
caps.handback.revision: 0
author: aaroncz
ms.author: aaroncz
manager: angrobe

---
# Design a hierarchy of sites for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Before installing the first site of a new System Center Configuration Manager hierarchy, it's a good idea to understand the available topologies for Configuration Manager, the types of available sites and their relationships with each other, and the scope of management that each site type provides.
Then, after considering content management options that can reduce the number of sites you need to install, you can plan a topology that efficiently serves your current business needs and can later expand to manage future growth.  

When planning, keep in mind limitations for adding additional sites to a hierarchy or stand-alone site:
-   You can install a new primary site below a central administration site, up to the [supported number of primary sites](/sccm/core/plan-design/configs/size-and-scale-numbers) for the hierarchy.
-   You can [expand a stand-alone primary site to install a new central administration site](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#bkmk_expand), so that you can then install additional primary sites.
-   You can install new secondary sites below a primary site, up to [supported limits for the primary site](/sccm/core/plan-design/configs/size-and-scale-numbers) and overall hierarchy.
-   You cannot add a previously installed site to an existing hierarchy to merge two stand-alone sites. Only installation of new sites to an existing hierarchy of sites is supported.


> [!NOTE]
> When planning a new installation of Configuration Manager, be aware of the [release notes]( /sccm/core/servers/deploy/install/release-notes), which detail current issues in the active versions. The release notes apply to all branches of Configuration Manager.  However, when you use the [Technical Preview Branch]( /sccm/core/get-started/technical-preview), you will find issues specific only to that branch in the documentation for each version of the Technical Preview.  

##  <a name="bkmk_topology"></a> Hierarchy topology  
 Hierarchy topologies range from a single stand-alone primary site to a group of connected primary and secondary sites with a central administration site at the top-level (top-tier) site of the hierarchy.   The key driver of the type and count of sites that you use in a hierarchy is usually the number and type of devices you must support, as follows:   

 **Stand-alone primary site:** Use a stand-alone primary site when a single primary site can support  management of all of your devices and users (see [Sizing and scale numbers](/sccm/core/plan-design/configs/size-and-scale-numbers)). This topology is also successful when your company’s different geographic locations can be successfully served by a single primary site.  To help manage network traffic, you can use preferred management points and a carefully planned content infrastructure (see [Fundamental concepts for content management in System Center Configuration Manager](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md)).  

 Benefit of this topology include:  

-   Simplified administrative overhead.  

-   Simplified client site assignment and discovery of available resources and services.  

-   Elimination of possible lag that's introduced by database replication between sites.

-   Option to expand a stand-alone primary hierarchy into a larger hierarchy with a central administration site. This enables you to then install new primary sites to expand the scale of your deployment.  


**Central administration site with one or more child primary sites:** Use this topology when you require more than one  primary site to support  management of all your devices and users.  It's required when you need to use more than a single primary site. Benefits of this topology include:  


-   It supports up to 25 primary sites that enable you to extend the scale of your hierarchy.  

-   You will always use the central administration site (unless you reinstall your sites). This is a permanent option. You cannot detach a child primary site to make it a stand-alone primary site.

 The following sections can help you understand when to use a specific site or content management option in place of an additional site.  

##  <a name="BKMK_ChooseCAS"></a> Determine when to use a central administration site  
 Use a central administration site to configure hierarchy-wide settings and to monitor all sites and objects in the hierarchy. This site type does not manage clients directly but it does coordinate inter-site data replication, which includes the configuration of sites and clients throughout the hierarchy.  

**The following information can help you decide when to install a central administration site:**  

-   The central administration site is the top-level site in a hierarchy.  

-   When you configure a hierarchy that has more than one primary site, you must install a central administration site. If you will need two or more primary sites immediately, install the central administration site first. When you already have a primary site and want to then install a central administration site, you must [expand the stand-alone primary site](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#bkmk_expand) to install the central administration site.

-   The central administration site supports only primary sites as child sites.  

-   The central administration site cannot have clients assigned to it.  

-   The central administration site does not support site system roles that directly support clients, such as management points and distribution points.  

-   You can manage all clients in the hierarchy and perform site management tasks for any child site when you use a Configuration Manager console that is connected to the central administration site. This can include installing management points or other site system roles at child primary or secondary sites.  

-   When you use a central administration site, the central administration site is the only place where you can see site data from all sites in your hierarchy. This data includes information such as inventory data and status messages.  

-   You can configure discovery operations throughout the hierarchy from the central administration site by assigning discovery methods to run at individual sites.  

-   You can manage security throughout the hierarchy by assigning different security roles, security scopes, and collections to different administrative users. These configurations apply at each site in the hierarchy.  

-   You can configure file replication and database replication to control communication between sites in the hierarchy. This includes scheduling database replication for site data and managing the bandwidth for the transfer of file-based data between sites.  

##  <a name="BKMK_ChoosePriimary"></a> Determine when to use a primary site  
 Use primary sites to manage clients. You can install a primary site as a child primary site below a central administration site, or as the first site of a new hierarchy. A primary site that is installed as the first site of a hierarchy creates a stand-alone primary site. Both child primary sites and stand-alone primary sites support secondary sites as child sites of the primary site.  

 Consider using a primary site for any of the following reasons:  

-   To manage device and users.  

-   To increase the number of devices you can manage with a single hierarchy.  

-   To provide an additional point of connectivity for the administration of your deployment.  

-   To meet organizational management requirements. For example, you might install a primary site at a remote location to manage the transfer of deployment content across a low-bandwidth network. However, with System Center Configuration Manager, you can use options to throttle the network bandwidth use when transferring data to a distribution point. That content management capability can replace the need to install additional sites.  


**The following information can help you decide when to install a primary site:**  

-   A primary site can be a stand-alone primary site or a child primary site in a larger hierarchy. When a primary site is a member of a hierarchy with a central administration site, the sites use database replication to replicate data between the sites. Unless you need to support more clients and devices than a single primary site can support, consider installing a stand-alone primary site.  After a stand-alone primary site is installed, you can expand it to report to a new central administration site to scale up your deployment.  

-   A primary site supports only a central administration site as a parent site.  

-   A primary site supports only secondary sites as child sites, and can also support multiple secondary child sites.  

-   Primary sites are responsible for processing all client data from their assigned clients.  

-   Primary sites use database replication to communicate directly to their central administration site (which is configured automatically when a new site installs).  

##  <a name="BKMK_ChooseSecondary"></a> Determine when to use a secondary site  
 Use secondary sites to manage the transfer of deployment content and client data across low-bandwidth networks.  

 You manage a secondary site from a central administration site or the secondary site's direct parent primary site. Secondary sites must be attached to a primary site, and you cannot move them to a different parent site without uninstalling them and then re-installing them as a child site below the new primary site.

However, you can route content between two peer secondary sites to help manage the file-based replication of deployment content. To transfer client data to a primary site, the secondary site uses file-based replication. A secondary site also uses database replication to communicate with its parent primary site.  

 Consider installing a secondary site if any of the following conditions apply:  

-   You do not require a local point of connectivity for an administrative user.  

-   You must manage the transfer of deployment content to sites lower in the hierarchy.  

-   You must manage client information that is sent to sites higher in the hierarchy.  

 If you do not want to install a secondary site and you have clients in remote locations, consider using Windows BranchCache or installing  distribution points that are enabled for bandwidth control and scheduling. You can use these content management options with or without secondary sites, and they can help you to reduce the number of sites and servers that you must install. For information about content management options in Configuration Manager, see  [Determine when to use content management options](#BKMK_ChooseSecondaryorDP).  


**The following information can help you decide when to install a secondary site:**  

-   Secondary sites automatically install SQL Server Express during site installation if a local instance of SQL Server is not available.  

-   Secondary site installation is initiated from the Configuration Manager console, instead of running Setup directly on a computer.  

-   Secondary sites use a subset of the information in the site database, which reduces the amount of data that replicates by database replication between the parent primary site and secondary site.  

-   Secondary sites support the routing of file-based content to other secondary sites that have a common parent primary site.  

-   Secondary site installations automatically deploy a management point and distribution point that are located on the secondary site server.  

##  <a name="BKMK_ChooseSecondaryorDP"></a> Determine when to use content management options  
 If you have clients in remote network locations, consider using one or more content management options instead of a primary or secondary site. You can often remove the need to install a site when you use Windows BranchCache, configure distribution points for bandwidth control, or manually copy content to distribution points (prestage content).  


**Consider deploying a distribution point instead of installing another site if any of the following conditions apply:**  

-   Your network bandwidth is sufficient for client computers at the remote location to communicate with a management point to download client policy, and send inventory, reporting status, and discovery information.  

-   Background Intelligent Transfer Service (BITS) does not provide sufficient bandwidth control for your network requirements.  

 For more information about content management options in Configuration Manager, see [Fundamental concepts for content management in System Center Configuration Manager](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

##  <a name="bkmk_beyond"></a> Beyond hierarchy topology  
 In addition to an initial hierarchy topology, consider which services or capabilities will be available from different sites  in the hierarchy (site system roles), and how hierarchy-wide configurations and capabilities will be managed in your infrastructure. The following common considerations are covered in separate topics. These are important because they can influence or be influenced by your hierarchy design:  

-   When you are preparing to [Manage computers and devices with System Center Configuration Manager](/sccm/core/clients/manage/manage-clients), consider whether the devices that you manage are on-premises, in the cloud, or include user-owned devices (BYOD).  Additionally, consider how you will manage devices that are supported by multiple management options, such as Windows 10 computers that can be managed directly by Configuration Manager or though integration with Microsoft Intune.  

-   Understand how your available network infrastructure might affect the flow of data between remote locations (see [Prepare your network environment for System Center Configuration Manager](/sccm/core/plan-design/network/configure-firewalls-ports-domains)). Also consider where the users and devices that you manage are geographically located, and whether they access your infrastructure through your corporate domain or the Internet.  

-   Plan for a content infrastructure to efficiently distribute the information you deploy (files and apps) to devices you manage (see [Manage content and content infrastructure for System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)).  

-   Determine which [features and capabilities of System Center Configuration Manager](../../../core/plan-design/changes/features-and-capabilities.md) you plan to use, the site system roles or Windows infrastructure they require, and at which sites in a multiple site hierarchy you might deploy them for the most efficient use of your network and server resources.  

-   Consider security for data and devices, including the use of a PKI. See [PKI certificate requirements for System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  


**Review the following resources for site-specific configurations:**  

-   [Plan for the SMS Provider for System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md)  

-   [Plan for the site database for System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-the-site-database.md)  

-   [Plan for site system servers and site system roles for System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)  

-   [Plan for security in System Center Configuration Manager](../../../core/plan-design/security/plan-for-security.md)  

-   [Managing network bandwidth](../../../core/plan-design/hierarchy/manage-network-bandwidth.md) when deploying content within a site  


**Consider configurations that span sites and hierarchies:**  

-   [High availability options for System Center Configuration Manager](/sccm/protect/understand/high-availability-options) for sites and hierarchies

-   [Extend the Active Directory schema for System Center Configuration Manager](../../../core/plan-design/network/extend-the-active-directory-schema.md) and configure sites to [publish site data for System Center Configuration Manager](../../../core/servers/deploy/configure/publish-site-data.md)  

-   [Data transfers between sites in System Center Configuration Manager](../../../core/servers/manage/data-transfers-between-sites.md)  

-   [Fundamentals of role-based administration for System Center Configuration Manager](../../../core/understand/fundamentals-of-role-based-administration.md)
