---
title: "Plan site system roles"
titleSuffix: "Configuration Manager"
description: "Consider site system servers and site system roles as you plan your System Center Configuration Manager hierarchy."
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0a7415ba-2c53-4433-983e-780e92aa662f
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Plan for site system servers and site system roles for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Each System Center Configuration Manager site you install includes a site server that is a **site system server**. The site can also include additional site system servers on computers that are remote from the site server. Site system servers (the site server or a remote site system server) support **site system roles**.


##  <a name="bkmk_siteservers"></a> Site system servers  
 When you install a site system role on a computer, that computer becomes a site system server. At each site, you can install one or more additional site system servers. You can also choose not to install additional site system servers, and run all site system roles directly on the site server computer. Each site system server supports one or more site system roles. Additional servers can help expand the capabilities and capacity of a site by sharing the CPU processing load that site system roles place on a server.  

 When considering the addition of a site system server, ensure the server meets prerequisites for the intended use. It's also a good idea to add it on a network location that has sufficient bandwidth to communicate with expected endpoints, including the site server, domain resources, a cloud-based location, site system servers, and clients).  

 If you configure the site system server with a proxy for use by site system roles, see [Site system roles that can use a proxy server](#bkmk_proxy).  

##  <a name="bkmk_planroles"></a> Site system roles  
 Site system roles are installed on a computer to provide additional capabilities to the site. Examples include:  

-   Additional management points so that the site can support more devices, up to the site's supported capacity.  

-   Additional distribution points to expand your content infrastructure, improving the performance of content distributions to devices and users.  

-   One or more feature-specific site system roles. For example, a software update point lets you manage software updates for managed devices, or a reporting services point lets you run reports to monitor and understand, or share information about, your deployment.  


Different Configuration Manager sites can support different sets of site system roles. The supported set of site system roles depends on the type of site (a central administration site, primary site, or secondary site). The topology of your hierarchy can limit the placement of some roles at certain site types. For example, the service connection point is only supported at the top-tier site of the hierarchy, which might be a central administration site or a stand-alone primary site. This role is not supported at a child primary site or at secondary sites.  

After a site installs, you can move the location of some site system roles from their default location on the site server to another server. For example, this is true of the management point or distribution point, which install by default on a primary or secondary site server. You can also install additional instances of some site system roles to expand the capabilities of your site (provide more services to clients), and to meet your business requirements. Some roles are required, while others are optional.  

-   **Configuration Manager site server.** This role identifies the server where Configuration Manager Setup is run to install a site, or the server on which you install a secondary site. This role cannot be moved or uninstalled until the site is uninstalled.  

-   **Configuration Manager site system.** This role is assigned to any computer on which you either install a site or install a site system role. This role cannot be moved or uninstalled until the last site system role is removed from the computer.  

-   **Configuration Manager component site system role.** This role identifies a site system that runs an instance of the SMS Executive service, and is required to support other roles, like management points. This role cannot be moved or uninstalled until the last applicable site system role is removed from the computer.  

-   **Configuration Manager site database server.** This role is assigned to site system servers that hold an instance of the site database for a site. This role can only be moved  to a new server by modifying the site to use a different instance of SQL Server to host the site database.  

-   **SMS Provider.** The SMS Provider role is assigned to each computer that hosts an instance of the SMS Provider, the interface between a Configuration Manager console and the site database. By default, this role installs automatically on the site server of a central administration site and primary sites. You can install additional instances at each site to provide access to additional administrative users.  

     To install additional providers, you must run Configuration Manager Setup to [Manage the SMS Provider](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider). Then you install additional providers on additional computers. You can only install one instance of the SMS Provider on a computer, and that computer must be in the same domain as the site server.  

-   **Application Catalog web service point.** A site system role that provides software information to the Application Catalog website from the Software Library. Although this role is supported only at primary sites, you can install multiple instances of this role at a site, or at multiple sites in the same hierarchy.  

-   **Application Catalog website point.** A site system role that provides users with a list of available software from the Application Catalog. Although this role is supported only at primary sites, you can install multiple instances of this role at a site, or at multiple sites in the same hierarchy.  

     When the Application Catalog supports client computers on the Internet, it's a security best practice to install the Application Catalog website point in a perimeter network for security, and to install the Application Catalog web service point on the intranet.  

-   **Asset Intelligence synchronization point.** A site system role that connects to Microsoft to download information for the Asset Intelligence catalog. This role also uploads uncategorized titles, so that they can be considered for future inclusion in the catalog. A hierarchy supports only a single instance of this role, and that must be at the top-tier site of your hierarchy (a central administration site or the stand-alone primary site). If you expand a stand-alone primary site into a larger hierarchy, you must uninstall this role from the primary site, and then install it at the central administration site.   For more information, see [Asset Intelligence in System Center Configuration Manager](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

-   **Certificate registration point.** A site system role that communicates with a server that runs the Network Device Enrollment Service. This role manages device certificate requests that use the Simple Certificate Enrollment Protocol (SCEP). This role is supported only at primary sites and the central administration site.

     Although a single certificate registration point can provide functionality to an entire hierarchy, you may want to install multiple instances of this role at a site, and at multiple sites in the same hierarchy. This can help with load balancing. When multiple instances exist in a hierarchy, clients are randomly assigned to one of the certificate registration points.  

     Each certificate registration point requires access to a separate instance of a Network Device Enrollment Service. You cannot configure two or more certificate registration points to use the same Network Device Enrollment Service. Additionally, the certificate registration point must not be installed on the same server that runs the Network Device Enrollment Service.  

- **Cloud management gateway connector point.** A site system role for communicating with the [cloud management gateway](/sccm/core/clients/manage/setup-cloud-management-gateway).

-   **Distribution point.** A site system role that contains source files for clients to download, such as application content, software packages, software updates, operating system images, and boot images. By default, this role installs on the site server computer of new primary and secondary sites when the site installs. This role is not supported at a central administration site. You can install multiple instances of this role at a supported site, and at multiple sites in the same hierarchy. For more information, see [Fundamental concepts for content management in System Center Configuration Manager](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md), and [Manage content and content infrastructure for System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   **Fallback status point.** A site system role that helps you monitor client installation, and identify the clients that are unmanaged because they cannot communicate with their management point. Although this role is supported only at primary sites, you can install multiple instances of this role at a site, and at multiple sites in the same hierarchy.     


-   **Endpoint Protection point.** A site system role that Configuration Manager uses to accept the Endpoint Protection license terms, and to configure the default membership for Cloud Protection Service. A hierarchy supports only a single instance of this role, and that must be at the top-tier site of your hierarchy (a central administration site or the stand-alone primary site). If you expand a stand-alone primary site into a larger hierarchy, you must uninstall this role from the primary site, and then install it at the central administration site. For more information, see [Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

-   **Enrollment point.** A site system role that uses PKI certificates for Configuration Manager to enroll mobile devices and Mac computers. Although this role is supported only at primary sites, you can install multiple instances of this role at a site, or at multiple sites in the same hierarchy.  

     If a user enrolls mobile devices by using Configuration Manager, and the user's Active Directory account is in a forest that is untrusted by the site server's forest, you must install an enrollment point in the user's forest. The user can then be authenticated.  

-   **Enrollment proxy point.** A site system role that manages Configuration Manager enrollment requests from mobile devices and Mac computers. Although this role is supported only at primary sites, you can install multiple instances of this role at a site, or at multiple sites in the same hierarchy.  

     When you support mobile devices on the Internet, install the enrollment proxy point in a perimeter network for security, and install the enrollment point on the intranet.  

-   **Exchange Server connector.** For information about this role, see [Manage mobile devices with System Center Configuration Manager and Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)  

-   **Management point.** A site system role that provides policy and service location information to clients, and receives configuration data from clients.  

    By default, this role installs on the site server computer of new primary and secondary sites when the site installs. Primary sites support multiple instances of this role. Secondary sites support a single management point, to provide a local point of contact for clients to obtain computer and user polices (a management point at a secondary site is referred to as a proxy management point).  

     Management points can be set up to support HTTP or HTTPs, as well as to support mobile devices you manage with System Center Configuration Manager On-premises Mobile Device Management. You can use [Database replicas for management points for System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md) to help reduce the CPU load placed on the site database server by management points as they service requests from clients.  

-   **Reporting services point.** A site system role that integrates with SQL Server Reporting Services to create and manage reports for Configuration Manager. This role is supported at primary sites and the central administration site, and you can install multiple instances of this role at a supported site. For more information, see [Planning for reporting in System Center Configuration Manager](../../../core/servers/manage/planning-for-reporting.md).  

-   **Service connection point.** A site system role that you use to manage mobile devices with Microsoft Intune and on-premises MDM. This role also uploads usage data from your site, and is required to make updates for Configuration Manager available in the Configuration Manager console. A hierarchy supports only a single instance of this role, and that must be at the top-tier site of your hierarchy (a central administration site or the stand-alone primary site). If you expand a stand-alone primary site into a larger hierarchy, you must uninstall this role from the primary site, and then install it at the central administration site. For more information, see [About the service connection point in System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  

-   **Software update point.** A site system role that integrates with Windows Server Update Services (WSUS) to provide software updates to Configuration Manager clients. This role is supported at all sites:  

    -   Install this site system in the central administration site to synchronize with WSUS.  

    -   Set up each instance of this role at child primary sites to synchronize with the central administration site.  

    -   Consider installing a software update point in secondary sites when data transfer across the network is slow.  

    For more information, see [Plan for software updates in System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

-   **State migration point.** A site system role that stores user state data when a computer is migrated to a new operating system. This role is supported at primary sites and at secondary sites. You can install multiple instances of this role at a site, and at multiple sites in the same hierarchy. For more information about storing user state when you deploy an operating system, see [Manage user state in System Center Configuration Manager](../../../osd/get-started/manage-user-state.md).  

-   **System Health Validator point.** Although this site system role remains visible in the Configuration Manager console, it is no longer used.  

###  <a name="bkmk_proxy"></a> Site system roles that can use a proxy server  
 Some Configuration Manager site system roles require connections to the Internet, and will use a proxy server when the site system server that hosts the role is configured for one. Typically, this connection is made in the **system** context of the computer where the site system role is installed. The connection cannot use a proxy configuration for typical user accounts. When a proxy server is required to complete a connection to the Internet, you must set up the computer to use a proxy server:  

-   You can set up a proxy server when installing a site system role.  

-   You can add or modify a proxy server configuration when you use the Configuration Manager console.  

-   The same proxy server configuration is used for all site system roles on a site system server that can use a proxy server configuration. If you require different site system roles to use different proxy servers, you must install the site system roles on different site system server computers.  

-   If you modify the proxy server configuration, or install a new site system role on a computer that already has a proxy server configuration, the original configuration is overwritten by the new configuration.  


For procedures about setting up the proxy server for site system roles, see the [Add site system roles for System Center Configuration Manager](../../../core/servers/deploy/configure/add-site-system-roles.md) topic.  

The following are site system roles that can use a proxy server:  

-   **Asset Intelligence synchronization point.** This site system role connects to Microsoft, uses a proxy server configuration on the computer that hosts the Asset Intelligence synchronization point.  

-   **Cloud-based distribution point.** When you use a cloud-based distribution point, the primary site that manages the cloud-based distribution point must be able to connect to Microsoft Azure to provision, monitor, and distribute content to the distribution point. If a proxy server is required for this connection, you must set up the proxy server on the primary site server. You cannot set up a proxy server on the cloud-based-distribution point in Azure. For more information, see the [Configure proxy settings for primary sites that manage cloud services](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#BKMK_ConfigProxyforCloud) section in the [Install cloud-based distribution points in Microsoft Azure for System Center Configuration Manager](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md) topic.  

-   **Exchange Server connector.** This site system role connects to an Exchange Server, and uses a proxy server configuration on the computer that hosts the Exchange Server connector.  

-   **Software updates point.** This site system role can require connections to Microsoft Update, to download patches and synchronize information about updates. Typically, when you set up the proxy server, each site system role on that computer that supports using the proxy server uses the proxy server. No additional configuration is required. An exception to this is the software updates point. By default, a software updates point does not use an available proxy server, unless you also enable the following options when you set up the software updates point:  

    -   **Use a proxy server when synchronizing software updates**  

    -   **Use a proxy server when downloading content by using automatic deployment rules**  

    > [!TIP]  
    >  Before you can select either option, a proxy server must be set up on the site system server that hosts the software updates point. The proxy server is only used for the specific options you select.  

 For more information about proxy servers for software update points, see the "Proxy Server Settings" section in [Install a software update point](../../../sum/get-started/install-a-software-update-point.md) topic.  

-   **Service connection point.** When set up to be online (not offline), this site system role connects to Microsoft Intune and the Microsoft cloud service.  
