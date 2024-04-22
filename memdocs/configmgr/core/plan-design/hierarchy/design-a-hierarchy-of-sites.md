---
title: Design a site hierarchy
titleSuffix: Configuration Manager
description: Understand the available topologies and management options for Configuration Manager to plan your site hierarchy.
ms.date: 10/01/2021
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Design a hierarchy of sites for Configuration Manager

*Applies to: Configuration Manager (current branch)*

Before installing the first site of a new Configuration Manager hierarchy, it's a good idea to understand:  

- The available topologies for Configuration Manager  

- The types of available sites and their relationships with each other  

- The scope of management that each type of site provides  

- The content management options that can reduce the number of sites you need to install  

Then plan a topology that efficiently serves your current business needs and can later expand to manage future growth.  

When planning, keep in mind limitations for adding additional sites to a hierarchy or a stand-alone site:  

- Install a new primary site below a central administration site, up to the [supported number of primary sites](../configs/size-and-scale-numbers.md) for the hierarchy.  

- [Expand a standalone primary site to install a new central administration site](../../servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand), to then install additional primary sites.  

- Install new secondary sites below a primary site, up to the [supported limit for the primary site](../configs/size-and-scale-numbers.md) and overall hierarchy.  

- You can't add a previously installed site to an existing hierarchy to merge two standalone sites. Configuration Manager only supports installation of new sites to an existing hierarchy of sites.  


> [!NOTE]  
> When planning a new installation of Configuration Manager, be aware of the [release notes](../../servers/deploy/install/release-notes.md), which detail current issues in the active versions. The release notes apply to all branches of Configuration Manager. When you use the [technical preview branch](../../get-started/technical-preview.md), find issues specific to that branch in the documentation for each version of the technical preview.  



##  <a name="bkmk_topology"></a> Hierarchy topology  

Hierarchy topologies range from:  

- Simplest: A single standalone primary site  

- Most complex: A group of connected primary and secondary sites with a central administration site at the top-level site of the hierarchy  

The key driver of the type and count of sites that you use in a hierarchy is usually the number and type of devices you must support.   

### Standalone primary site

Use a standalone primary site when it can support management of all devices and users. For more information, see [Sizing and scale numbers](../configs/size-and-scale-numbers.md). This topology is also successful when your company's geographic locations can be served by a single primary site. To help manage network traffic, use multiple management points in boundary groups, and a carefully planned content infrastructure. For more information, see [Configure boundary groups](../../servers/deploy/configure/boundary-groups.md) and [Fundamental concepts for content management](fundamental-concepts-for-content-management.md).  

This topology provides the following benefits:  

- Simplified administrative overhead  

- Simplified client site assignment and discovery of available resources and services  

- Elimination of possible delays introduced by database replication between sites  

- Option to expand a standalone primary site into a larger hierarchy with a central administration site. This option enables you to then install new primary sites to expand the scale of your deployment.  


### Central administration site with one or more child primary sites 

Use this topology when you require more than one primary site to support management of all your devices and users. It's required when you need to use more than a single primary site. 

This topology provides the following benefits:  

- It supports up to 25 primary sites that enable you to extend the scale of your hierarchy.    

- You always use the central administration site, unless you reinstall your sites. This option is permanent. You can't detach a child primary site to make it a standalone primary site.  



##  <a name="BKMK_ChooseCAS"></a> Determine when to use a central administration site  

Use a central administration site to configure hierarchy-wide settings and to monitor all sites and objects in the hierarchy. This site type doesn't manage clients directly. It coordinates site-to-site data replication, which includes the configuration of sites and clients throughout the hierarchy.  

The following information can help you decide when to install a central administration site:  

- The central administration site is the top-level site in a hierarchy.  

- When you configure a hierarchy that has more than one primary site, install a central administration site.  

     - If you immediately need two or more primary sites, install the central administration site first.  

     - When you already have a primary site, and want to then install a central administration site, [expand the stand-alone primary site](../../servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand) to install the central administration site.  

- The central administration site supports only primary sites as child sites.  

- The central administration site can't have clients assigned to it.  

- The central administration site doesn't support site system roles that directly support clients, such as management points and distribution points.  

- Manage all clients in the hierarchy and perform all site management tasks from the Configuration Manager console that is connected to the central administration site. These tasks include installing management points or other site system roles at child primary or secondary sites.  

- When you use a central administration site, it's the only place where you see site data from all sites in your hierarchy. This data includes information such as inventory data and status messages.  

- Configure discovery operations throughout the hierarchy from the central administration site. From the central administration site, assign discovery methods to run at individual primary sites.  

- Manage security throughout the hierarchy by assigning different security roles, security scopes, and collections to different administrative users. These configurations apply at each site in the hierarchy.  

- Configure replication to control communication between sites in the hierarchy. Schedule database replication for site data, and managing the bandwidth for the transfer of file-based data between sites.  



##  <a name="BKMK_ChoosePriimary"></a> Determine when to use a primary site  

Use primary sites to manage clients. Install a primary site as a child site below a central administration site, or as the first site of a new hierarchy. A primary site that's the first site of a hierarchy creates a standalone primary site. Both child primary sites and standalone primary sites support secondary sites.  

Consider adding additional primary sites for the following reasons:  

- To increase the number of devices, manage with a single hierarchy.  

- To meet organizational management requirements. For example, you might install a primary site at a remote location to manage the transfer of deployment content across a low-bandwidth network.  

     - Consider instead using options to throttle the network bandwidth when transferring data to a distribution point. That content management capability can replace the need to install additional sites.  


The following information can help you decide when to install a primary site:  

- A primary site can be a standalone primary site or a child primary site in a larger hierarchy. When a primary site is a member of a hierarchy with a central administration site, the sites use database replication to replicate data between the sites. Unless you need to support more clients and devices than a single primary site supports, consider installing a standalone primary site. After you install a standalone primary site, expand it if needed in the future to report to a new central administration site to scale up your deployment.  

- A primary site supports only a central administration site as a parent site.  

- A primary site supports only secondary sites as child sites, and supports multiple secondary sites.  

- Primary sites are responsible for processing all client data from their assigned clients.  

- Primary sites use database replication to communicate directly to their central administration site. This behavior is configured automatically when a new site installs.  



##  <a name="BKMK_ChooseSecondary"></a> Determine when to use a secondary site  

Use secondary sites to manage the transfer of deployment content and client data across low-bandwidth networks.  

You manage a secondary site from a central administration site or the secondary site's direct parent primary site. Secondary sites are attached to a primary site. You can't move them to a different parent site without uninstalling them and then reinstalling them as a child site below the new primary site.

However, you can route content between two peer secondary sites to help manage the file-based replication of deployment content. To transfer client data to a primary site, the secondary site uses file-based replication. A secondary site also uses database replication to communicate with its parent primary site.  

Consider installing a secondary site if any of the following conditions apply:  

- You don't require a local point of connectivity for an administrative user.  

- You're required to manage the transfer of deployment content to sites lower in the hierarchy.  

- You're required to manage client information that's sent to sites higher in the hierarchy.  

If you don't want to install a secondary site, and you have clients in remote locations, consider the following options:  

- Use peer-to-peer technologies such as Windows BranchCache  

- Enable distribution points for bandwidth control and scheduling   

Use these content management options with or without secondary sites. They help reduce the size of your Configuration Manager infrastructure. For more information about content management options in Configuration Manager, see [Determine when to use content management options](#BKMK_ChooseSecondaryorDP).  


The following information can help you decide when to install a secondary site:  

- If a local instance of SQL Server isn't available, secondary site servers automatically install SQL Server Express during site installation.  

- Secondary site installation is initiated from the Configuration Manager console, instead of running setup directly on a computer.  

- Secondary sites use a subset of the information in the site database. This behavior reduces the amount of data that SQL Server replicates between the parent primary site and secondary site.  

- Secondary sites support the routing of file-based content to other secondary sites that have a common parent primary site.  

- Secondary site installations automatically install the management point and distribution point site system roles on the secondary site server.  



##  <a name="BKMK_ChooseSecondaryorDP"></a> Determine when to use content management options  

If you have clients in remote network locations, consider using one or more content management options instead of a primary or secondary site. The following options often remove the need to install a site:  

- Windows Delivery Optimization

- Configuration Manager peer cache  

- Windows BranchCache  

- Configure distribution points for bandwidth control  

- Manually copy content to distribution points (prestage content)  


If any of the following conditions apply, consider deploying a distribution point instead of installing another site:  

- Your network bandwidth is sufficient for client computers at the remote location to communicate with a management point at the primary site. Clients communicate with a management point to download client policy, send inventory, send reporting status, and send discovery information.  

- Background Intelligent Transfer Service (BITS) doesn't provide sufficient bandwidth control for your network requirements.  

For more information about content management options in Configuration Manager, see [Fundamental concepts for content management](fundamental-concepts-for-content-management.md).  



##  <a name="bkmk_beyond"></a> Beyond hierarchy topology  

Along with your initial hierarchy topology, also consider the following questions:  

- Which site system roles provide services or capabilities from different sites in the hierarchy?  

- How are you managing hierarchy-wide configurations and capabilities in your infrastructure?  


The following common considerations are covered in separate articles. This information is important to influence or be influenced by your hierarchy design:  

- When you're preparing to [Manage computers and devices](../../clients/manage/manage-clients.md), consider whether the devices are on-premises, in the cloud, or include user-owned devices (BYOD). Additionally, consider how you'll manage devices that support multiple management options. For example, manage Windows devices with Configuration Manager or though integration with Microsoft Intune. For more information, see [Choose a device management solution](../choose-a-device-management-solution.md).  

- Understand how your available network infrastructure might affect the flow of data between remote locations. For more information, see [Prepare your network environment](../network/configure-firewalls-ports-domains.md). Also consider the geographic location of your users and devices, and whether they access your infrastructure through your on-premises network or the internet.  

- Plan for a content infrastructure to efficiently distribute the content you deploy to devices you manage. This content may be applications, software updates, or operating systems. For more information, see [Manage content and content infrastructure](../../servers/deploy/configure/manage-content-and-content-infrastructure.md).  

- Determine which [features and capabilities of Configuration Manager](../changes/features-and-capabilities.md) you plan to use. Different features require different site system roles or Windows infrastructure. In a multiple site hierarchy, decide where you deploy them for the most efficient use of your network and server resources.  

- Consider security for data and devices, including the use of a public key infrastructure (PKI). For more information, see [PKI certificate requirements](../network/pki-certificate-requirements.md).  

## Next steps

Review the following articles for site-specific configurations:  

- [Plan for the SMS Provider](plan-for-the-sms-provider.md)  

- [Plan for the site database](plan-for-the-site-database.md)  

- [Plan for site system servers and site system roles](plan-for-site-system-servers-and-site-system-roles.md)  

- [Plan for security](../security/plan-for-security.md)  

- [Managing network bandwidth](manage-network-bandwidth.md) when deploying content within a site  

Consider configurations that span sites and hierarchies  

- [High availability options](../../servers/deploy/configure/high-availability-options.md) for sites and hierarchies

- [Extend the Active Directory schema](../network/extend-the-active-directory-schema.md) and configure sites to [publish site data](../../servers/deploy/configure/publish-site-data.md)  

- [Data transfers between sites](data-transfers-between-sites.md)  

- [Fundamentals of role-based administration](../../understand/fundamentals-of-role-based-administration.md)  

- [Manage clients on the internet](../../clients/manage/manage-clients-internet.md)  
