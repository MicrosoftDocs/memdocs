---
title: Plan site system roles
titleSuffix: Configuration Manager
description: Consider site system servers and site system roles as you plan your Configuration Manager hierarchy.
ms.date: 03/29/2022
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Plan for site system servers and site system roles in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Each Configuration Manager site you install includes a site server that's a **site system server**. The site can also include additional site system servers on computers that are remote from the site server. Site system servers (the site server or a remote site system server) support **site system roles**.  

## <a name="bkmk_siteservers"></a> Site system servers  

When you install a site system role on a computer, that computer becomes a site system server. At each site, you can install one or more additional site system servers. You don't have to install additional site system servers, and can choose to run all site system roles directly on the site server computer. Each site system server supports one or more site system roles. Additional servers can help expand the capabilities and capacity of a site by sharing the processing load that site system roles place on a server.  

When considering the addition of a site system server, ensure the server meets prerequisites for the intended use. Also add it on a network location that has sufficient bandwidth to communicate with expected endpoints. These endpoints include the site server, domain resources, a cloud-based location, site system servers, and clients.  


## <a name="bkmk_planroles"></a> Site system roles  

Install site system roles on a server to provide additional capabilities to the site. Examples include:  

- Additional management points so that the site can support more devices, up to the site's supported capacity.  

- Additional distribution points to expand your content infrastructure, improving the performance of content distributions to devices.  

- One or more feature-specific site system roles. For example, a software update point lets you manage software updates for managed devices. A reporting services point lets you run reports to monitor, understand, and share information about your environment.  

Different Configuration Manager sites can support different sets of site system roles. The supported set of site system roles depends on the type of site. (The types of sites include a central administration site, primary sites, or secondary sites.) The topology of your hierarchy can limit the placement of some roles at certain site types. For example, the service connection point is only supported at the top-tier site of the hierarchy. The top-tier site might be a central administration site or a standalone primary site. This role isn't supported at a child primary site or at secondary sites.  

After a site installs, you can move the location of some site system roles from their default location on the site server to another server. For example, the management point or distribution point roles install by default on a primary or secondary site server. Also install additional instances of some site system roles to expand the capabilities of your site, and to meet your business requirements. Some roles are required, while others are optional.  

### Configuration Manager site server

This role identifies the server where Configuration Manager setup is run to install a site, or the server on which you install a secondary site. You can't move or uninstall this role until the site is uninstalled.  

### Configuration Manager site system

This role is assigned to any computer on which you either install a site or install a site system role. You can't move or uninstall this role until you remove the last site system role from the computer.  

### Configuration Manager component site system role

This role identifies a site system that runs an instance of the **SMS Executive** service. It's required to support other roles, like management points. You can't move or uninstall this role until you remove the last applicable site system role from the computer.  

### Configuration Manager site database server

The site assigns this role to site system servers that hold an instance of the site database. Only move this role to a new server by running setup to modify the site to use a different instance of SQL Server to host the site database.  

### SMS Provider

The site assigns this role to each computer that hosts an instance of the SMS Provider. The provider is the interface between a Configuration Manager console and the site database. By default, this role automatically installs on the site server of a central administration site and primary sites. Install additional instances at each site to provide access to additional administrative users or for redundancy.  

To install additional providers, run Configuration Manager setup to [Manage the SMS Provider](../../servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider). Then install additional providers on additional computers. Only install one instance of the SMS Provider on a computer. That computer must be in the same domain as the site server.  

### Asset Intelligence synchronization point

> [!IMPORTANT]
> Starting in November 2021, this feature of Configuration Manager is deprecated.<!-- 12454890 --> For more information, see [Asset intelligence deprecation](../../clients/manage/asset-intelligence/deprecation.md).

A site system role that connects to Microsoft to download information for the Asset Intelligence catalog. This role also uploads uncategorized titles, so that Microsoft can consider them for future inclusion in the catalog. A hierarchy supports only a single instance of this role at the top-tier site of your hierarchy. If you expand a standalone primary site into a larger hierarchy, uninstall this role from the primary site. Then install it at the central administration site.

For more information, see [Asset Intelligence in Configuration Manager](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

### Certificate registration point

> [!WARNING]
> Starting in version 2203, the certificate registration point is no longer supported.<!--13951253--> For more information, see [Frequently asked questions about resource access deprecation](../../../protect/plan-design/resource-access-deprecation-faq.yml).

A site system role that communicates with a server that runs the Network Device Enrollment Service (NDES). This role manages device certificate requests that use the Simple Certificate Enrollment Protocol (SCEP). This role is supported only at primary sites and the central administration site.

Although a single certificate registration point can provide functionality to an entire hierarchy, you may want to install multiple instances of this role at a site, and at multiple sites in the same hierarchy. This design helps with load balancing. When multiple instances exist in a hierarchy, clients are randomly assigned to one of the certificate registration points.  

Each certificate registration point requires access to a separate NDES instance. You can't configure two or more certificate registration points to use the same NDES instance. Additionally, don't install the certificate registration point on the same server that runs NDES.  

### Cloud management gateway connection point

A site system role for communicating with the [cloud management gateway](../../clients/manage/cmg/overview.md).  

### Data warehouse service point

Use the data warehouse service point to store and report on long-term historical data in your Configuration Manager environment. For more information, see [Data warehouse](../../servers/manage/data-warehouse.md).  

### Distribution point

A site system role that contains source files for clients to download, for example:

- Application content
- Software packages
- Software updates
- OS images
- Boot images  

By default, this role installs on the site server when you install a new primary or secondary site. This role isn't supported at a central administration site. Install multiple instances of this role at a supported site, and at multiple sites in the same hierarchy. For more information, see [Fundamental concepts for content management](fundamental-concepts-for-content-management.md), and [Manage content and content infrastructure](../../servers/deploy/configure/manage-content-and-content-infrastructure.md).  

### Endpoint Protection point

A site system role that Configuration Manager uses to accept the Endpoint Protection license terms, and to configure the default membership for Cloud Protection Service. A hierarchy only supports a single instance of this role, and that must be at the top-tier site. If you expand a standalone primary site into a larger hierarchy, uninstall this role from the primary site, and then install it at the central administration site. For more information, see [Endpoint Protection in Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

### Enrollment point

> [!IMPORTANT]
> With the deprecation of on-premises MDM and the Configuration Manager client for macOS, this site system role is also deprecated. For more information, see [Removed and deprecated features for Configuration Manager](../changes/deprecated/removed-and-deprecated-cmfeatures.md).<!-- 12454901,12927803 -->

A site system role that uses PKI certificates for Configuration Manager to enroll mobile devices and macOS computers. Although this role is supported only at primary sites, you can install multiple instances of this role at a site, or at multiple sites in the same hierarchy.  

If a user enrolls mobile devices by using Configuration Manager, and the user's Active Directory account is in a forest that's untrusted by the site server's forest, install an enrollment point in the user's forest. Then Configuration Manager can authenticate the user.  

### Enrollment proxy point

> [!IMPORTANT]
> With the deprecation of on-premises MDM and the Configuration Manager client for macOS, this site system role is also deprecated. For more information, see [Removed and deprecated features for Configuration Manager](../changes/deprecated/removed-and-deprecated-cmfeatures.md).<!-- 12454901,12927803 -->

A site system role that manages Configuration Manager enrollment requests from mobile devices and macOS computers. Although this role is supported only at primary sites, you can install multiple instances of this role at a site, or at multiple sites in the same hierarchy.  

When you support mobile devices on the internet, install an enrollment proxy point in a perimeter network, and install one on the intranet.

### Exchange Server connector

For information about this role, see [Manage mobile devices with Configuration Manager and Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

### Fallback status point

A site system role that helps you monitor client installation. It identifies clients that are unmanaged because they can't communicate with their management point. Although this role is supported only at primary sites, you can install multiple instances of this role at a site, and at multiple sites in the same hierarchy.

### Management point

A site system role that provides policy and service location information to clients. It also receives configuration data from clients.  

By default, this role installs on the site server when you install a new primary or secondary site. Primary sites support multiple instances of this role. Secondary sites support a single management point. Also referred to as a proxy management point, this role at a secondary site provides a local point of contact for clients to obtain computer and user policies.  

Set up management points to support either HTTP or HTTPs. They can also support mobile devices that you manage with Configuration Manager on-premises mobile device management (MDM). To help reduce the processing load placed on the site database server by management points as they service requests from clients, use [Database replicas for management points](../../servers/deploy/configure/database-replicas-for-management-points.md).  

> [!IMPORTANT]
> Starting in Configuration Manager version 2103, sites that allow HTTP client communication are deprecated. Configure the site for HTTPS or Enhanced HTTP. For more information, see [Enable the site for HTTPS-only or enhanced HTTP](../../servers/deploy/install/list-of-prerequisite-checks.md#enable-site-system-roles-for-https-or-enhanced-http).<!-- 9390933,9572265 -->

### Reporting services point

A site system role that integrates with SQL Server Reporting Services to create and manage reports for Configuration Manager. This role is supported at primary sites and the central administration site, and you can install multiple instances of this role at a supported site. For more information, see [Planning for reporting](../../servers/manage/planning-for-reporting.md).  

### Service connection point

A site system role that uploads usage data from your site, and is required to make updates for Configuration Manager available in the console. A hierarchy only supports a single instance of this role, and that must be at the top-tier site of your hierarchy. If you expand a standalone primary site into a larger hierarchy, uninstall this role from the primary site, and then install it at the central administration site. For more information, see [About the service connection point](../../servers/deploy/configure/about-the-service-connection-point.md).  

### Software update point

A site system role that integrates with Windows Server Update Services (WSUS) to provide software updates to Configuration Manager clients. This role is supported at all sites:  

- Install this site system at the central administration site to synchronize with WSUS.  

- Set up each instance of this role at child primary sites to synchronize with the central administration site.  

- When data transfer across the network is slow, consider installing a software update point in secondary sites.  

For more information, see [Plan for software updates](../../../sum/plan-design/plan-for-software-updates.md).  

### State migration point

When you migrate a computer to a new operating system, this site system role stores user state data. This role is supported at primary sites and at secondary sites. Install multiple instances of this role at a site, and at multiple sites in the same hierarchy. For more information about storing user state when you deploy an OS, see [Manage user state](../../../osd/get-started/manage-user-state.md).  


## Next steps

Some Configuration Manager site system roles require connections to the internet. If your environment requires internet traffic to use a proxy server, configure these site system roles to use the proxy. For more information, see [Proxy server support](../network/proxy-server-support.md).  
