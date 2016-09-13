---
title: "Size and scale numbers for System Center Configuration Manager"
ms.custom: na
ms.date: 2016-07-22
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c5a42100-2f60-4952-b495-918025ea6559
caps.latest.revision: 4
author: Brenduns
---
# Size and scale numbers for System Center Configuration Manager


Each System Center Configuration Manager deployment will have a maximum number of sites, site system roles, and devices that it can support. These numbers vary depending on your hierarchy structure (what types and numbers of sites you use) and the site system roles you deploy.  The information in the following subjects can help you identify the number of site system roles and sites you will need to support the devices you expect to manage with your environment.

Use the information in this topic with the information in the following articles:
-   [Recommended hardware](../../../core/plan-design/configs/recommended-hardware.md)
-   [Supported operating systems for site system serveres](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
-   [Supported operating systems for clients and devices](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)
-   [Site and site system prerequisites](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)

These support numbers in this article are based on using the recommended hardware for Configuration Manager. When you do not use the recommended hardware, the performance of site systems can be degraded and might not meet the stated levels of support.

##  <a name="bkmk_SiteSystemScale"></a> Site types  
 **Central administration site:**  

-   A central administration site supports up to 25 child primary sites.  

**Primary site:**  

-   Each primary site supports up to 250 secondary sites.  

-   The number of secondary sites per primary site is based on continuously connected and reliable wide area network (WAN) connections. For locations that have fewer than 500 clients, consider a distribution point instead of a secondary site.  

 For information about the numbers of clients and devices a primary site can support, see [Client numbers for sites and hierarchies](#bkmk_ClientNumbers) in this topic.  

**Secondary site:**  

-   Secondary sites do not support child sites.  

-   A central administration site supports up to 25 child primary sites.  

**Application Catalog website point:**  

-   You can install multiple instances of the Application Catalog website point at primary sites.  

    > [!TIP]  
    >  As a best practice, install the Application Catalog website point and Application Catalog web service point together on the same site system when they provide service to clients that are on the intranet.  

    -   For improved performance, plan to support up to 50,000 clients per instance.  

    -   Each instance of this site system role supports the maximum number of clients supported by the hierarchy.  

# <a name="bkmk_roles"></a> Site system roles    

**Application Catalog web service point:**  

-   You can install multiple instances of the Application Catalog web service point at primary sites.  

    > [!TIP]  
    >  As a best practice, install the Application Catalog website point and Application Catalog web service point together on the same site system when they provide service to clients that are on the intranet.  

    -   For improved performance, plan to support up to 50,000 clients per instance.  

    -   Each instance of this site system role supports the maximum number of clients supported by the hierarchy.  

**Distribution Point:**  

-   Distribution points per site:  

    -   Each primary and secondary site supports up to 250 distribution points.  

    -   Each primary and secondary site supports up to 2000 additional distribution points configured as pull-distribution points. **For example**, a single primary site supports 2250 distribution points when 2000 of those distribution points are configured as pull-distribution points.  

    -   Each distribution point supports connections from up to 4,000 clients.  

    -   A pull-distribution point acts like a  client when it accesses content from a source distribution point.  

-   Each primary site supports a combined total of up to 5,000 distribution points. This total includes all the distribution points at the primary site and all distribution points that belong to the primary site’s child secondary sites.  

-   Each distribution point supports a combined total of up to 10,000 packages and applications.  

> [!WARNING]  
>  The actual number of clients that one distribution point can support depends on the speed of the network, and the hardware configuration of the distribution point computer.  
>   
>  The number of pull-distribution points that one source distribution point can support similarly depends on the speed of the network and hardware configuration of the source distribution point computer, but is also affected by the amount of content you have deployed. This is because unlike clients that typically access content at different times over the course of a deployments window, all pull-distribution point request content at the same time and can request all available content and not just the content that is applicable to them, as would a client. When too much of a processing load is placed on a source distribution point, this can cause unexpected delays in distributing the content to the expected distribution points in your environment.  


**Fallback status point:**  

-   Each fallback status point can support up to 100,000 clients.  

**Management point:**  

-   Each primary site supports up to 15 management points.  

    > [!TIP]  
    >  Do not install management points on servers that are across a slow link from the primary site server or from the site database server.  

-   Each secondary site supports a single management point that must be installed on the secondary site server.  

 For information about the numbers of clients and devices a management point can support, see the [Management points](#bkmk_mp) section in this topic.  

**Software update point:**  

-   A software update point that is installed on the site server can support up to 25,000 clients.  

-   A software update point that is remote from the site server can support up to 150,000 clients when the remote computer meets the WSUS requirements to support this number of clients.  

-   By default, Configuration Manager does not support configuring software update points as NLB clusters. However, you can use the Configuration Manager SDK to configure up to four software update points on a NLB cluster.  

##  <a name="bkmk_ClientNumbers "></a> Client numbers for sites and hierarchies  
 Use the following information to determine how many clients, and of which types, you can support at a site or in a hierarchy.  

###  <a name="bkmk_cas"></a> Hierarchy with a central administration site  
A central administration site supports a total number of devices that includes up to the number of devices listed for the following three groups:  

-   700,000 desktops (computers that run Windows, Linux and UNIX)  

-   25,000 devices that run Mac and Windows CE 7.0  

-   One of the following, depending on how your deployment supports mobile device management:  

    -   100,000 devices you manage with On-Premises MDM  

    -   300,000 cloud-based devices  

 For example, in a hierarchy you can support 700,000 desktops, up to 25,000 Mac  and Windows CE 7.0 clients, and up to 300,000 cloud-based devices when you integrate Microsoft Intune, for a total of 1,025,000 devices.  If you support devices managed by on-premises MDM, the total for the hierarchy is 825,000 devices.  

> [!IMPORTANT]  
>  In a hierarchy where the central administration site uses  a Standard edition of SQL Server, the hierarchy supports a maximum of 50,000 desktops and devices. The edition of SQL Server in use at a stand-alone primary site does not limit that sites capacity to support up to the stated number of clients.  


###  <a name="bkmk_chipri"></a> Child primary site  
Each child primary site in a hierarchy with a central administration site supports the following:  

-   150,000 total clients and devices, not limited to a specific group or type, so long as support does not exceed the number supported for the hierarchy  

For example, a primary site that supports 25,000 computers that run Mac and Windows CE 7.0 (because that is the limit for a hierarchy), can then support an additional 125,000 desktop computers, which brings the total number of supported devices up to the child primary sites supported maximum limit of 150,000.

###  <a name="bkmk_pri"></a> Stand-alone primary site  
A stand-alone primary site supports the following number of devices:  

-   175,000 total clients and devices, not to exceed:  

    -   150,000 desktops (computers that run Windows, Linux and UNIX)  

    -   25,000 devices that run Mac and Windows CE 7.0  

    -   One of the following, depending on how your deployment supports mobile device management:  

        -   50,000 devices you manage with On-Premises MDM  

        -   150,000 cloud-based devices  

For example, a stand-alone primary site that supports 150,000 desktops and 10,000 Mac or Windows CE 7.0 clients can support only an additional 15,000 devices. Those devices can be either cloud-based or managed using on-premises MDM.  

###  <a name="bkmk_sec"></a> Secondary sites  
Secondary sites support the following:  

-   15,000 desktops (computers that run Windows, Linux and UNIX)  

###  <a name="bkmk_mp"></a> Management points  
Each management can support the following number of devices:  

-   25,000 total clients and devices, not to exceed:  

    -   25,000 desktops (computers that run Windows, Linux and UNIX)  

    -   One of the following (not both):  

        -   10,000 devices managed using On-Premises MDM  

        -   10,000 devices that run Mac and Windows CE 7.0  


## See Also
 [Supported configurations for System Center Configuration Manager](../../../core/plan-design/configs/supported-configurations.md)
