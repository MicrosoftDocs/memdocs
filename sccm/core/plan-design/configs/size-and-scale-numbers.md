---
title: Size and scale
titleSuffix: Configuration Manager
description: Determine the number of site system roles and sites that you'll need to support the devices in your environment.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c5a42100-2f60-4952-b495-918025ea6559
author: mestew
ms.author: mstewart
manager: dougeby


---

# Size and scale numbers for Configuration Manager

*Applies to: Configuration Manager (current branch)*

Each Configuration Manager deployment has a maximum number of sites, site system roles, and devices that it can support. These numbers vary depending on your hierarchy structure, what types and numbers of sites you use, and the site system roles that you deploy. The information in this article can help you determine the number of site system roles and sites that you need to support the devices you expect to manage.

For more information, see the following articles:

- [Recommended hardware](/sccm/core/plan-design/configs/recommended-hardware)
- [Supported operating systems for site system servers](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers)  
- [Supported operating systems for clients and devices](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices)
- [Site and site system prerequisites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)

These support numbers are based on using the recommended hardware for Configuration Manager. They're also based on the default settings for all available Configuration Manager features. When you don't use the recommended hardware or use more aggressive custom settings, the performance of site systems can degrade. The site systems might not meet the stated levels of support. (An example of more aggressive client settings is running hardware or software inventory more frequently than the defaults of once every seven days.)


## <a name="bkmk_SiteSystemScale"></a> Site types  

### Central administration site  

- A central administration site supports up to 25 child primary sites.  

### Primary site  

- Each primary site supports up to 250 secondary sites.  

- The number of secondary sites per primary site is based on continuously connected and reliable wide area network (WAN) connections. For locations that have fewer than 500 clients, consider a distribution point instead of a secondary site.  

  For information about the number of clients and devices that a primary site can support, see [Client numbers for sites and hierarchies](#bkmk_clientnumbers).  

### Secondary site  

- Secondary sites don't support child sites.  


## <a name="bkmk_roles"></a> Site system roles

### Application catalog web service point  

> [!Important]
> The application catalog's Silverlight user experience isn't supported as of current branch version 1806. Starting in version 1906, updated clients automatically use the management point for user-available application deployments. You also can't install new application catalog roles. Support ends for the application catalog roles with version 1910.  
>
> For more information, see the following articles:
>
> - [Configure Software Center](/sccm/apps/plan-design/plan-for-software-center#bkmk_userex)
> - [Removed and deprecated features](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)  

- You can install multiple instances of the Application Catalog web service point at primary sites.  

### Application catalog website point  

> [!Important]
> The application catalog's Silverlight user experience isn't supported as of current branch version 1806. Starting in version 1906, updated clients automatically use the management point for user-available application deployments. You also can't install new application catalog roles. Support ends for the application catalog roles with version 1910.  
>
> For more information, see the following articles:
>
> - [Configure Software Center](/sccm/apps/plan-design/plan-for-software-center#bkmk_userex)
> - [Removed and deprecated features](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures)  

- You can install multiple instances of the Application Catalog website point at primary sites.  

### <a name="bkmk_cmg"></a> Cloud management gateway

- You can install multiple instances of the cloud management gateway (CMG) at primary sites, or the central administration site.  

    > [!Tip]  
    > In a hierarchy, create the CMG at the central administration site.  

    - One CMG supports one to 16 virtual machine (VM) instances in the Azure cloud service.  

    - Each CMG VM instance supports 6,000 simultaneous client connections. When the CMG is under high load due to more than the supported number of clients, it still handles requests but there may be delay.  

For more information, see CMG [Performance and scale](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#performance-and-scale)

### Cloud management gateway connection point

- You can install multiple instances of the CMG connection point at primary sites.  

- One CMG connection point can support a CMG with up to four VM instances. If the CMG has more than four VM instances, add a second CMG connection point for load balancing. A CMG with 16 VM instances should be linked with four CMG connection points.

For more information, see CMG [Performance and scale](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#performance-and-scale)

### Distribution point  

- Distribution points per site:  

    - Each primary and secondary site supports up to 250 distribution points.  

    - Each primary and secondary site supports up to 2000 additional distribution points that are configured as pull-distribution points. **For example**, a single primary site supports 2250 distribution points when 2000 of those distribution points are configured as pull-distribution points.  

    - Each distribution point supports connections from up to 4,000 clients.  

    - A pull-distribution point acts like a client when it accesses content from a source distribution point.  

- Each primary site supports a combined total of up to 5,000 distribution points. This total includes all the distribution points at the primary site and all the distribution points that belong to the primary site’s child secondary sites.  

- Each distribution point supports a combined total of up to 10,000 packages and applications.  

> [!WARNING]  
> The actual number of clients that one distribution point can support depends on the speed of the network and the hardware configuration of the server.  
>
> The number of pull-distribution points that one source distribution point can support similarly depends on the speed of the network and the hardware configuration of the source distribution point. But this number is also affected by the amount of content that you've deployed. This effect is because, unlike clients that typically access content at different times during a deployment, all pull-distribution points request content at the same time. Pull-distribution points can request all available content, not just the content that is applicable to them. When you place a high processing load on a source distribution point, there can be unexpected delays in distributing the content to the target distribution points.  

### Fallback status point  

- Each fallback status point can support up to 100,000 clients.  

### Management point  

- Each primary site supports up to 15 management points.  

    > [!TIP]  
    > Don't install management points on servers that are across a slow link from the primary site server or the site database server.  

- Each secondary site supports a single management point that must be installed on the secondary site server.  

For information about the number of clients and devices that a management point can support, see the [Management points](#bkmk_mp) section.  

### Software update point  

Use the following recommendations as a baseline. This baseline helps you determine the information for the software updates capacity planning that is appropriate to your organization. The actual capacity requirements might vary from the recommendations listed in this article depending on the following criteria: 
- Your specific networking environment
- The hardware that you use to host the software update point site system
- The number of managed clients
- The other site system roles installed on the server  

#### <a name="BKMK_SUMCapacity"></a> Capacity planning for the software update point  

The number of supported clients depends on the version of Windows Server Update Services (WSUS) that runs on the software update point. It also depends on whether the software update point site system role coexists with another site system role:  

- The software update point can support up to 25,000 clients when WSUS runs on the software update point server, and the software update point coexists with another site system role.  

- The software update point can support up to 150,000 clients when a remote server meets WSUS requirements, WSUS is used with Configuration Manager, and you configure the following settings:

    IIS Application Pools:
    - Increase the WsusPool Queue Length to 2000
    - Increase the WsusPool Private Memory limit x4 times, or set to 0 (unlimited). For example, if the default limit is 1,843,200 KB, increase it to 7,372,800. For more information, see this [Configuration Manager support team blog post](https://www.phoenixtekk.com/configmgr-2012-support-tip-wsus-sync-fails-with-http-503-errors/).  

    For more information about hardware requirements for the software update point, see [Recommended hardware for site systems](/sccm/core/plan-design/configs/recommended-hardware#bkmk_ScaleSieSystems).  


#### <a name="bkmk_sum-capacity-obj"></a> Capacity planning for software updates objects  

Use the following capacity information to plan for software updates objects:  

- **Limit of 1000 software updates in a deployment** -Limit the number of software updates to 1000 for each software update deployment. When you create an automatic deployment rule (ADR), specify criteria that limits the number of software updates. The ADR fails when the specified criteria returns more than 1000 software updates. Check the status of the ADR from the **Automatic Deployment Rules** node in the Configuration Manager console. When you manually deploy software updates, don't select more than 1000 updates to deploy.  

  Also limit the number of software updates to 1000 in a configuration baseline. For more information, see [Create configuration baselines](/sccm/compliance/deploy-use/create-configuration-baselines).

- **Limit of 580 security scopes for automatic deployment rules** -<!--ado 4962928-->
Limit the number of security scopes on automatic deployment rules (ADRs) to less than 580. When you create an ADR, the security scopes that have access to it are automatically added. If there are more than 580 security scopes set, the ADR will fail to run and an error is logged in ruleengine.log.

## <a name="bkmk_clientnumbers"></a> Client numbers for sites and hierarchies

Use the following information to determine how many clients and which types of clients you can support at a site or in a hierarchy.  

### <a name="bkmk_cas"></a> Hierarchy with a central administration site

A central administration site supports a total number of devices that includes up to the number of devices listed for the following three groups:  

- 700,000 Windows desktops. Also see support for [embedded devices](#embedded).

- 25,000 devices that run Mac and Windows CE 7.0  

- 100,000 devices that you manage by using on-premises mobile device management (MDM)

For example, in a hierarchy you can support 700,000 desktops, up to 25,000 Mac and Windows CE 7.0 devices, and up to 100,000 devices managed by on-premises MDM. This hierarchy supports a total of 825,000 devices.

> [!IMPORTANT]  
> In a hierarchy where the central administration site uses a Standard edition of SQL Server, the hierarchy supports a maximum of 50,000 desktops and devices. To support more than 50,000 desktops and devices, you must use an Enterprise edition of SQL Server. This requirement applies only to a central administration site. It doesn't apply to a stand-alone primary site or a child primary site. The edition of SQL Server you use for a primary site doesn't limit its capacity to support the stated number of clients.

The edition of SQL Server that is in use at a stand-alone primary site doesn't limit that site's capacity to support up to the stated number of clients.  

### <a name="bkmk_chipri"></a> Child primary site

Each child primary site in a hierarchy with a central administration site supports the following number of clients:  

- 150,000 total clients and devices that aren't limited to a specific group or type, as long as support doesn't exceed the number that is supported for the hierarchy. Also see, support for [embedded devices](#embedded).

For example, a primary site supports 25,000 Mac and Windows CE 7.0 devices. That number is the limit for a hierarchy. This primary site can then support an additional 125,000 desktop computers. The total number of supported devices for the child primary site is the supported maximum limit of 150,000.

### <a name="bkmk_pri"></a> Stand-alone primary site

A stand-alone primary site supports the following number of devices:  

- 175,000 total clients and devices, not to exceed:  

    - 150,000 desktops (computers that run Windows, Linux, and UNIX). Also see, support for [embedded devices](#embedded).

    - 25,000 devices that run Mac and Windows CE 7.0

    - 50,000 devices that you manage by using on-premises MDM  

For example, a stand-alone primary site that supports 150,000 desktops and 10,000 Macs can only support an additional 15,000 mobile devices managed by on-premises MDM.

### <a name="embedded"></a> Primary sites and Windows Embedded devices

Primary sites support Windows Embedded devices that have File-Based Write Filters (FBWF) enabled. When embedded devices don't have write filters enabled, a primary site can support a number of embedded devices up to the allowed number of devices for that site. When embedded devices have FBWF or Unified Write Filters (UWF) enabled, a primary site can support a maximum of 10,000 Windows embedded devices. These devices must be configured with the exceptions listed in the important note found in the [Planning for client deployment to Windows Embedded devices](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices). A primary site supports only 3,000 Windows Embedded devices that have EWF enabled and that are not configured for the exceptions.

### <a name="bkmk_sec"></a> Secondary sites

Secondary sites support the following number of devices:  

- 15,000 desktops (computers that run Windows, Linux, and UNIX)  

### <a name="bkmk_mp"></a> Management points

Each management point can support the following number of devices:  

- 25,000 total clients and devices, not to exceed:  

    - 25,000 desktops (computers that run Windows, Linux, and UNIX)  

    - One of the following (not both):  

        - 10,000 devices that are managed by using on-premises MDM  

        - 10,000 devices that run Mac and Windows CE 7.0 clients
