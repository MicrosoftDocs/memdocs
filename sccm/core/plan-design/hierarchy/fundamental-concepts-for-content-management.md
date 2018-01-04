---
title: "Content management fundamentals"
titleSuffix: "Configuration Manager"
description: "Use tools and options in System Center Configuration Manager to manage the content that you deploy."
ms.custom: na
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c201be2a-692c-4d67-ac95-0a3afa5320fe
caps.latest.revision: 28
caps.handback.revision: 0
author: aczechowski
ms.author: aaroncz
manager: angrobe

---
# Fundamental concepts for content management in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager supports a robust system of tools and options to manage the content you deploy as applications, packages, software updates, and operating system deployments.  

The content that you deploy is stored on both site servers and on distribution point site system servers. This content can require a large amount of network bandwidth when it's being transferred between locations. To effectively plan and use content management infrastructure, we recommend that you understand the available options and configurations, and then consider how to use them to best fit your networking environment and content deployment needs.  

> [!TIP]    
> You can learn more about the content distribution process and find help in diagnosing and resolving general content distribution problems. See [Understanding and Troubleshooting Content Distribution in Microsoft Configuration Manager](https://support.microsoft.com/help/4000401/content-distribution-in-mcm) at support.microsoft.com.

Following are key concepts for content management. When a concept requires additional or complex information, links are provided to direct you to those details.

## Accounts used for content management  
 The following accounts can be used with content management:  

-   **Network access account**: Used by clients to connect to a distribution point and access content. By default, the computer account is tried first.  

     This account is also used by pull-distribution points to obtain content from a source distribution point in a remote forest.  

-   **Package access account**: By default, Configuration Manager grants access to content on a distribution point to the generic access accounts Users and Administrators. However, you can configure additional permissions to restrict access.   

-   **Multicast connection account**: Used for operating system deployments.  

For more information about these accounts, see [Manage accounts to access content](../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md).

## Bandwidth throttling and scheduling  
 Both throttling and scheduling are options that help you control when content is distributed from a site server to distribution points. This is similar to, but not directly related to bandwidth controls for site to site file-based replication.  

 For more information, see [Manage network bandwidth](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).

## Binary differential replication  
 A prerequisite for distribution points, binary differential replication (BDR), which is sometimes known as delta replication, is automatically used to reduce bandwidth use when you're distributing updates to content that you previously deployed to other sites or to remote distribution points.  

 BDR   minimizes the network bandwidth that is used to send updates for distributed content by resending only the new or changed content instead of sending the entire set of content source files each time a change to those files is made.  

 When binary differential replication is used, Configuration Manager identifies the changes that occur to source files for each set of content that has previously been distributed.  

-   When files in the source content change, Configuration Manager creates a new incremental version of the content set and replicates only the changed files to destination sites and distribution points. A file is considered changed if it has been renamed or moved, or if the contents of the file have changed. For example, if you replace a single driver file for an operating system deployment package that you previously distributed to several sites, only the changed driver file is replicated to those destination sites.  

-   Configuration Manager supports up to five incremental versions of a content set before it resends the entire content set. After the fifth update, the next change to the content set causes Configuration Manager to create a new version of the content set. Configuration Manager then distributes the new version of the content set to replace the previous set and any of its incremental versions. After the new content set is distributed, subsequent incremental changes to the source files are again replicated by binary differential replication.  


BDR is supported between each parent and child site in a hierarchy. Within a site, BDR is supported between the site server and its regular distribution points. However, pull-distribution points and cloud-based distribution points do not support binary differential replication to transfer content. Pull-distribution points support file-level deltas, transferring new files, but not blocks within a file.

Applications always use binary differential replication. For packages, binary differential replication is optional and is not enabled by default. To use binary differential replication for packages, you must enable this functionality for each package. To do so, select the option **Enable binary differential replication** when you create a new package or when you edit the **Data Source** tab of the package properties.  

## BranchCache  
 A Windows technology that enables clients that support BranchCache and have downloaded a deployment that is configured for Branch Cache to then serve as a content source to other BranchCache-enabled clients.  

 For example, when the first BranchCache-enabled client computer requests content from a distribution point that runs Windows Server 2012 and is configured as a BranchCache server, the client computer downloads that content and caches it.  

-   That client computer can then make the content available for additional BranchCache-enabled clients on the same subnet that also cache the content.  

-   In this way, subsequent clients on the same subnet do not have to download content from the distribution point, and the content is distributed across multiple clients for future transfers.  

## Peer Cache
Beginning with version 1610, client Peer Cache helps you manage deployment of content to clients in remote locations. Peer Cache is a built-in Configuration Manager solution that enables clients to share content with other clients directly from their local cache.

After you deploy client settings that enable Peer Cache to a collection, members of that collection can act as a peer content source for other clients in the same boundary group.

For more information, see [Peer Cache for Configuration Manager clients](/sccm/core/plan-design/hierarchy/client-peer-cache).


## Windows PE peer cache
When you deploy a new operating system in System Center Configuration Manager, computers that run the task sequence can use Windows PE Peer Cache to obtain content from a local peer (a peer cache source) instead of downloading content from a distribution point. This helps minimize wide area network (WAN) traffic in branch office scenarios where there is no local distribution point.

For more information, see [Windows PE peer cache](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).


## Client locations  
 The following are locations that clients access content from:  

-   **Intranet** (on-premises):  

    -   Distribution points can use HTTP or HTTPs.  

    -   Only use a cloud-based distribution point for fallback when on-premises distribution points are not available.  

-   **Internet**:  

    -   Requires distribution points to accept HTTPS.  

    -   Can use a cloud-based distribution point for fallback.  

-   **Workgroup**:  

    -   Requires distribution points to accept HTTPS.  

    -   Can use a cloud-based distribution point for fallback.  



## Content library  
 The content library is the single-instance store of content that Configuration Manager uses to reduce the overall size of the combined body of content that you distribute.  

- Learn more about the [content library](../../../core/plan-design/hierarchy/the-content-library.md).
- Use the [content library cleanup tool](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) to remove content that is no longer associated with an application.  


## Distribution points  
 Configuration Manager uses distribution points to store files that are required for software to run on client computers. Clients must have access to at least one distribution point from which they can download the files for content that you deploy.  

 The basic (non-specialized) distribution point is commonly referred to as a standard distribution point. There are two  variations on the standard distribution point that receive special attention:  

-   **Pull-distribution point**: A variation of a distribution point where the distribution point obtains content from another distribution point (a source distribution point). This process is similar to how clients download content from distribution points. Pull-distribution points can help you avoid network bandwidth bottlenecks that occur when the site server must directly distribute content to each distribution point.  [Use a pull-distribution point with System Center Configuration Manager](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).

-   **Cloud-based distribution point**: A variation of a distribution point that's installed on Microsoft Azure. [Learn how to use a cloud-based distribution point with System Center Configuration Manager](../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md).  


Standard distribution points support a range of configurations and features, such as throttling and scheduling, PXE and Multicast, or prestaged content.  

-   You can use controls such as **schedules** or **bandwidth throttling** to help control this transfer.  

-   You can also use other options, including **prestaged content**, and **pull-distribution points**. In addition, you can leverage **BranchCache** to reduce the network bandwidth that's used when you deploy content.  

-   Distribution points support different configurations, such as **[PXE](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)** and **[Multicast](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast)** for operating system deployments, or configurations to support **mobile devices**.  

 Cloud-based and pull distribution points support many of these same configurations, but have limitations that are specific to each distribution point variation.  

## Distribution point groups  
 Distribution point groups are logical groupings of distribution points that can simplify content distribution.  

 For more information, see [Manage distribution point groups](../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage).

## Distribution point priority  
 The distribution point priority value is based on how long it took to transfer previous deployments to that distribution point.  

-   This is a self-tuning value that's assigned to a distribution point that helps Configuration Manager transfer content to more distribution points in a shorter period of time.  

-   When you distribute content to multiple distributions points at the same time or to a distribution point group, Configuration Manager sends the content to the distribution point with the highest priority before it sends that same content to a distribution point with a lower priority.  

-   This does not replace the distribution priority for packages, which remains the deciding factor in the sequence of when different distributions are transferred.  


For example, if you distribute content that has a high distribution priority to a distribution point that has a low distribution point priority, this high distribution priority package always transfers before a package that has a lower distribution priority. The distribution priority applies even if packages that have a lower distribution priority are distributed to distribution points that have higher distribution point priorities.

The high distribution priority of the package ensures that Configuration Manager distributes that content to its applicable distribution points before any packages with a lower distribution priority are sent.  

> [!NOTE]  
>  Pull-distribution points also use a concept of priority to order the sequence of their source distribution points.  
>   
>  -   The distribution point priority for content transfers to the distribution point is distinct from the priority that pull-distribution points use when they search for content from a source distribution point.  
>  -   For more information, see [Use a pull-distribution point with System Center Configuration Manager](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).  


## Fallback  
 Beginning with version 1610, several things have changed in the way that clients find a distribution point that has content, including fallback. Use the following information that applies to the version you use:

**Version 1610 and later**   
Clients that cannot find content from a distribution point that's associated with their current boundary group can fall back to use content source locations that are associated with neighbor boundary groups. To be used for fallback, a neighbor boundary group must have a defined relationship with the client’s current boundary group. This relationship includes a configured time which must pass before a client that cannot find content locally can include content sources from the neighbor boundary group as part of its search.

The concepts of preferred distribution points are no longer used, and settings for **Allow fallback source locations for content** are no longer available or enforced.

For more information, see [Boundary groups](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).


**Version 1511, 1602, and 1606**   
Fallback settings are related to the use of **preferred distribution points** and to content source locations that are used by clients.

-   By default, clients only download content from a preferred distribution point (one that is associated with the client's boundary groups).  

-   However, when a distribution point is configured with **Allow clients to use this site system as a fallback source location for content**, that distribution point is only offered as a valid content source to any client that cannot get a deployment from one of its preferred distribution points.  


For information about the different content location and fallback scenarios, see [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md). For information about boundary groups, see [Boundary groups for versions 1511,1602, and 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).

## Network bandwidth  
 To help manage the amount of network bandwidth that's used when you distribute content, you can use the following options:  

-   **Prestaged content**:  A process of transferring content to a distribution point without relying on  Configuration Manager to distribute the content across the network.  

-   **Scheduling and throttling**: Configurations that help you control when and how content is distributed to distribution points.  

For more information, see [Manage network bandwidth](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).

## Network connection speed to content source  
Beginning with version 1610, several things have changed in the way that clients find a distribution point that has content, including the network connection speed to a content source. Use the following information that applies to the version you use:

**Version 1610 and later**   
Network connection speeds that define a distribution point as **Fast** or **Slow** are no longer used. Instead, each site system that's associated with a boundary group is treated the same.

For more information, see [Boundary groups](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).


**Version 1511, 1602, and 1606**   
 You can configure the network connection speed of each distribution point in a boundary group:  

-   Clients use this value when they connect to the distribution point.

-   By default, the network connection speed is configured as **Fast**, but it can also be set as **Slow**.  

-   The **network connection speed**, along with the configuration of a deployment, determine if a client can download content from a distribution point when the client is in an associated boundary group  

For information about the different content location and fallback scenarios, see [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md). For information about boundary groups, see [Boundary groups for versions 1511,1602, and 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).

## On-demand content distribution  
 On-demand content distribution is an option you can set for individual applications and packages (deployments) to enable on-demand content distribution to preferred distribution points.  

-   To enable this for a deployment,  enable **Distribute the content for this package to preferred distribution points**.  

-   When this option is enabled for a deployment and a client attempts to request that content but the content is not available on any of the client's preferred distribution points, Configuration Manager automatically distributes that content to the client's preferred distribution points.  

-   Although this triggers Configuration Manager to automatically distribute the content to that client's preferred distribution points, the client might obtain that content from other distribution points before the preferred distribution points for the client receive the deployment. When this occurs, the content will then be present on that distribution point for use by the next client that seeks that deployment.  

If you use version 1610 or later, see [Boundary groups](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).
If you use version 1511, 1602, or 1606, see  [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md) for information about the different content location and fallback scenarios.  



## Package Transfer Manager  
 Package Transfer Manager is the site server component that transfers content to distribution points on other computers.  

 Learn more about the [Package Transfer Manager](../../../core/plan-design/hierarchy/package-transfer-manager.md).  

## Preferred distribution point  
 A preferred distribution point includes any distribution points that are associated with a client's current boundary groups.  

 You have the option to associate each distribution point with one or more boundary groups:  

-   This association helps the client identify distribution points from which it can download content.  
-   By default, clients can only download content from a preferred distribution point.  


For more information:
 - If you use version 1610 or later, see [Boundary groups](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).
 - If you use version 1511, 1602, or 1606, see [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md).

## Prestage content  
 Prestaging content is a process of transferring content to a distribution point without relying on Configuration Manager to distribute the content across the network.  

 For more information, see [Manage network bandwidth](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).
