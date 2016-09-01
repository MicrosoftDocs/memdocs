---
title: "Design a hierarchy of sites for System Center Configuration Manager"
ms.custom: na
ms.date: 2016-03-15
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
author: Brenduns
translation.priority.ht: 
  - cs-cz
  - de-de
  - en-gb
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# Design a hierarchy of sites for System Center Configuration Manager
Before installing the first site of a new System Center Configuration Manager hierarchy, you should understand the available topologies for Configuration Manager, the available types of sites and their relationships with each other, and the scope of  management each site type provides. Then, after considering content management options that can reduce the number of sites you need to install, you can plan out a topology that efficiently serves your current business needs and can later expand to manage future growth.  
  
##  <a name="bkmk_topology"></a> Hierarchy topology  
 Hierarchy topologies range from a single stand-alone primary site to a group of connected primary and secondary sites with a central administration site at the top-level (top-tier) site of the hierarchy.    
The key driver of the type and count of sites that you use in a hierarchy is usually the number and type of devices you must support:  
  
 **Stand-alone primary site:** Use a stand-alone primary site when a single primary site can support  management of all of your devices and users (see [Sizing and scale numbers](../Topic/Supported%20operating%20systems%20for%20sites%20and%20clients%20for%20System%20Center%20Configuration%20Manager.md#bkmk_Sizing)). This topology is also successful when your companies different geographic locations can be successful served by a single primary site.  To help manage the network traffic you can use preferred management points and a carefully planned content infrastructure (see [Fundamental concepts for content management in System Center Configuration Manager](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md)).  
  
 Benefit of this topology include:  
  
-   Simplified administrative overhead  
  
-   Simplified client site assignment and discovery of available resources and services  
  
-   Eliminates possible lag introduced by database replication between sites  
  
-   This choice is not permanent and you can expand a stand-alone primary hierarchy  into a larger hierarchy with a central administration site. This enables you to then install new primary sites to expand the scale of your deployment.  
  
 **Central administration site with one or more child primary sites:** Use this topology when you require more than one  primary site to support  management of all of your devices and users.  Benefits of this topology include:  
  
-   Required  when you need to use more than a single primary site  
  
-   Supports up to 25 primary sites enabling you to extend the scale of your hierarchy  
  
-   This choice is permanent. You cannot detach a child primary site to make it a stand-alone primary site. Therefore, unless you reinstall your sites,  you will always use the central administration site  
  
 The following sections can help you understand when to use a specific site or content management option in place of an additional site.  
  
##  <a name="BKMK_ChooseCAS"></a> Determine when to use a central administration site  
 Use a central administration site to configure hierarchy-wide settings and to monitor all sites and objects in the hierarchy. This site type does not manage clients directly but it does coordinate inter-site data replication, which includes the configuration of sites and clients throughout the hierarchy.  
  
 **The following information can help you decide when to install a central administration site:**  
  
-   The central administration site is the top-level site in a hierarchy  
  
-   When you configure a hierarchy that has more than one primary site, you must install a central administration site, and it must be the first site that you install  
  
-   The central administration site supports only primary sites as child sites  
  
-   The central administration site cannot have clients assigned to it  
  
-   The central administration site does not support site system roles that directly support clients, like management points and distribution points  
  
-   You can manage all clients in the hierarchy and perform site management tasks for any child site when you use a Configuration Manager console that is connected to the central administration site. This can include installing management points or other site system roles at a child primary or secondary sites  
  
-   When you use a central administration site, the central administration site is the only place where you can see site data from all sites in your hierarchy. This data includes information such as inventory data and status messages  
  
-   You can configure discovery operations throughout the hierarchy from the central administration site by assigning discovery methods to run at individual sites  
  
-   You can manage security throughout the hierarchy by assigning different security roles, security scopes, and collections to different administrative users. These configurations apply at each site in the hierarchy  
  
-   You can configure file replication and database replication to control communication between sites in the hierarchy. This includes scheduling database replication for site data, and managing the bandwidth for the transfer of file-based data between sites  
  
##  <a name="BKMK_ChoosePriimary"></a> Determine when to use a primary site  
 Use primary sites to manage clients. You can install a primary site as a child primary site below a central administration site, or as the first site of a new hierarchy. A primary site that installs as the first site of a hierarchy creates a stand-alone primary site. Both child primary sites and stand-alone primary sites support secondary sites as child sites of the primary site.  
  
 Consider using a primary site for any of the following reasons:  
  
-   To manage device and users  
  
-   To increase the number of devices you can manage with a single hierarchy  
  
-   To provide additional point of connectivity for administration of your deployment  
  
-   To meet organizational management requirements. For example, you might install a primary site at a remote location to manage the transfer of deployment content across a low-bandwidth network. However, with System Center Configuration Manager you can use options to throttle the network bandwidth use when transferring data to a distribution point and  that content management capability can replace the need to install additional sites.  
  
 **The following information can help you decide when to install a  primary site:**  
  
-   A primary site can be a stand-alone primary site or a child primary site in a larger hierarchy. When a primary site is a member of a hierarchy with a central administration site, the sites use database replication to replicate data between the sites. Unless you need to support more clients and devices than a single primary site can support, consider installing a stand-alone primary site.  After a stand-alone primary site installs, you can expand it to report to a new central administration site to scale up your deployment.  
  
-   A primary site supports only a central administration site as a parent site  
  
-   A primary site supports only secondary sites as child sites and can support multiple secondary child sites  
  
-   Primary sites are responsible for processing all client data from their assigned clients  
  
-   Primary sites use database replication to communicate directly to their central administration site (this is configured automatically when a new site installs)  
  
##  <a name="BKMK_ChooseSecondary"></a> Determine when to use a secondary site  
 Use secondary sites to manage the transfer of deployment content and client data across low-bandwidth networks.  
  
 You manage a secondary site from a central administration site or the secondary site’s direct parent primary site. Secondary sites must be attached to a primary site, and you cannot move them to a different parent site without uninstalling them and then re-installing them as a child site below the new primary site. However, you can route content between two peer secondary sites to help manage the file-based replication of deployment content. To transfer client data to a primary site, the secondary site uses file-based replication. A secondary site also uses database replication to communicate with its parent primary site.  
  
 Consider installing a secondary site if any of the following conditions apply:  
  
-   You do not require a local point of connectivity for an  administrative user  
  
-   You have to manage the transfer of deployment content to sites lower in the hierarchy  
  
-   You have to manage client information that is sent to sites higher in the hierarchy  
  
 If you do not want to install a secondary site and you have clients in remote locations, consider using Windows BranchCache or installing  distribution points that are enabled for bandwidth control and scheduling. You can use these content management options with or without secondary sites, and they can help you to reduce the number of sites and servers that you have to install. For information about content management options in Configuration Manager, see [Determine when to use content management options](#BKMK_ChooseSecondaryorDP).  
  
 **The following information can help you decide when to install a secondary site:**  
  
-   Secondary sites automatically install SQL Server Express during site installation if a local instance of SQL Server is not available  
  
-   Secondary site installation is initiated from the Configuration Manager console, instead of running Configuration Manager Setup directly on a computer  
  
-   Secondary sites use a subset of the information in the site database which reduces the amount of data that replicates by database replication between the parent primary site and secondary site  
  
-   Secondary sites support the routing of file-based content to other secondary sites that have a common parent primary site  
  
-   Secondary site installations automatically deploy a management point and distribution point that are located on the secondary site server  
  
##  <a name="BKMK_ChooseSecondaryorDP"></a> Determine when to use content management options  
 If you have clients in remote network locations, consider using one or more content management options instead of a primary or secondary site. You can often remove the need to install a site when you use Windows BranchCache, configure distribution points for bandwidth control, or manually copy content to distribution points (prestage content).  
  
 **Consider deploying a distribution point instead of installing another site if any of the following conditions apply:**  
  
-   Your network bandwidth is sufficient for client computers at the remote location to communicate with a management point to download client policy, and send inventory, reporting status, and discovery information  
  
-   Background Intelligent Transfer Service (BITS) does not provide sufficient bandwidth control for your network requirements  
  
 For more information about content management options in Configuration Manager, see [Fundamental concepts for content management in System Center Configuration Manager](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  
  
##  <a name="bkmk_beyond"></a> Beyond hierarchy topology  
 In addition to an initial hierarchy topology, consider what services or capabilities will be available from  different sites  in the hierarchy (site system roles), and how hierarchy wide configurations and capabilities will be managed in your infrastructure. The following are the  more common considerations and are covered in separate topics. These should be considered as they can influence or be influenced by your hierarchy design:  
  
-   When you are preparing to [Manage computers and devices with System Center Configuration Manager](../Topic/Manage%20computers%20and%20devices%20with%20System%20Center%20Configuration%20Manager.md), consider if the devices you manage reside on-premises, in the cloud, or include user owned devices (BYOD).  Additionally, consider how you will manage devices that are supported by multiple  management options, like Windows 10 computers that can be managed directly by Configuration Manager or though integration with Microsoft Intune.  
  
-   Understand how your available network infrastructure might affect the flow of data between remote locations (see [Prepare your network environment for System Center Configuration Manager](../Topic/Prepare%20your%20network%20environment%20for%20System%20Center%20Configuration%20Manager.md)). Also consider where users and devices you manage are geographically located, and if they will access your infrastructure through your corporate domain, or from the Internet.  
  
-   Plan for a content infrastructure to efficiently distribute the information you deploy (files and apps) to devices you manage (see [Manage content and content infrastructure for System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)).  
  
-   Determine which [Features and capabilities of System Center Configuration Manager](../../../core/plan-design/changes/features-and-capabilities.md) you plan to use, the site system roles or Windows infrastructure they require, and at which sites in a multiple site hierarchy you might deploy them for the most efficient use of your network and server resources.  
  
-   Consider security for data and devices, including the use of a PKI. See [PKI certificate requirements for System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md)  
  
 **Review the following resources  for site specific configurations:**  
  
-   [Plan for the SMS Provider for System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md)  
  
-   [Plan for the site database for System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-the-site-database.md)  
  
-   [Plan for site system servers and site system roles for System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)  
  
-   [Plan for security in System Center Configuration Manager](../../../core/plan-design/security/plan-for-security.md)  
  
-   [Managing network bandwidth](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#bkmk_bandwidth) when deploying content within a site  
  
 **Consider configurations that span sites and hierarchies:**  
  
-   [High availability options for System Center Configuration Manager](../Topic/Supported%20operating%20systems%20for%20sites%20and%20clients%20for%20System%20Center%20Configuration%20Manager.md#bkmk_HA) for sites and hierarchies  
  
-   Will you [Extend the Active Directory schema for System Center Configuration Manager](../../../core/plan-design/network/extend-the-active-directory-schema.md) and configure and sites to [Publish site data for System Center Configuration Manager](../../../core/servers/deploy/configure/publish-site-data.md)?  
  
-   To manage network bandwidth between sites in a hierarchy, see [Data transfers between sites in System Center Configuration Manager](../../../core/servers/manage/data-transfers-between-sites.md)  
  
-   [Fundamentals of role-based administration for System Center Configuration Manager](../../../core/understand/fundamentals-of-role-based-administration.md)  
  
## See Also  
 [Plan for System Center Configuration Manager infrastructure](../Topic/Plan%20for%20System%20Center%20Configuration%20Manager%20infrastructure.md)