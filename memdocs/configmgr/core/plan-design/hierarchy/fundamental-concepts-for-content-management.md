---
title: Content management fundamentals
titleSuffix: Configuration Manager
description: Use tools and options in Configuration Manager to manage the content that you deploy.
ms.date: 04/06/2022
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Fundamental concepts for content management in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Configuration Manager supports a robust system of tools and options to manage software content. Software deployments such as applications, packages, software updates, and OS deployments all need content. Configuration Manager stores the content on both site servers and distribution points. This content requires a large amount of network bandwidth when it's being transferred between locations. To plan and use the content management infrastructure effectively, first understand the available options and configurations. Then consider how to use them to best fit your networking environment and content deployment needs.  

> [!TIP]  
> For more information about the content distribution process and to find help in diagnosing and resolving general content distribution problems, see [Understanding and Troubleshooting Content Distribution in Microsoft Configuration Manager](https://support.microsoft.com/help/4000401/content-distribution-in-mcm).

The following sections are key concepts for content management. When a concept requires additional or complex information, links are provided to direct you to those details.

## Accounts used for content management

The following accounts can be used with content management:  

### Network access account

Used by clients to connect to a distribution point and access content. If allowed, the client first tries anonymous authentication. Then it tries Windows-integrated authentication with the computer account or network access account. For more information, see [Client to distribution point communication](communications-between-endpoints.md#bkmk_client2dp).<!-- MEMDocs #1391 -->

This account is also used by pull-distribution points to download content from a source distribution point in a remote forest.  

Some scenarios no longer require a network access account. You can enable the site to use Enhanced HTTP with Azure Active Directory authentication.<!--1358228-->

For more information, see [Network access account](accounts.md#network-access-account).

### Package access account

By default, Configuration Manager grants access to content on a distribution point to the generic access accounts Users and Administrators. However, you can configure additional permissions to restrict access.

For more information, see [Package access account](accounts.md#package-access-account).


## Bandwidth throttling and scheduling

Both throttling and scheduling are options that help you control when content is distributed from a site server to distribution points. These capabilities are similar to, but not directly related to bandwidth controls for site-to-site file-based replication.  

For more information, see [Manage network bandwidth](manage-network-bandwidth.md).


## Binary differential replication

Configuration Manager uses binary differential replication (BDR) to update content that you previously distributed to other sites or to remote distribution points. To support BDR's reduction of bandwidth usage, install the **Remote Differential Compression** feature on distribution points. For more information, see [Distribution point prerequisites](../configs/site-and-site-system-prerequisites.md#distribution-point).

BDR minimizes the network bandwidth used to send updates for distributed content. It resends only the new or changed content instead of sending the entire set of content source files each time you change those files.  

When BDR is used, Configuration Manager identifies the changes that occur to source files for each set of content that you previously distributed.  

- When files in the source content change, the site creates a new incremental version of the content. It then replicates only the changed files to destination sites and distribution points. A file is considered changed if you renamed or moved it, or if you changed the contents of the file. For example, if you replace a single driver file for a driver package that you previously distributed to several sites, only the changed driver file is replicated.  

- Configuration Manager supports up to five incremental versions of a content set before it resends the entire content set. After the fifth update, the next change to the content set causes the site to create a new version of the content set. Configuration Manager then distributes the new version of the content set to replace the previous set and any of its incremental versions. After the new content set is distributed, later incremental changes to the source files are again replicated by BDR.  

BDR is supported between each parent and child site in a hierarchy. BDR is supported within a site between the site server and its regular distribution points. However, pull-distribution points and content-enabled cloud management gateways don't support BDR to transfer content. Pull-distribution points support file-level deltas, transferring new files, but not blocks within a file.

Applications always use binary differential replication. BDR is optional for packages and isn't enabled by default. To use BDR for packages, enable this functionality for each package. Select the option **Enable binary differential replication** when you create or edit a package.

### BDR or delta replication

<!-- SCCMDocs#1209 -->
The following lists summarize the differences between *binary differential replication* (BDR) and *delta replication*.

#### Summary of binary differential replication

- Configuration Manager's term for Windows **Remote Differential Compression**
- *Block*-level differences
- Always enabled for apps
- Optional on legacy packages
- If a file already exists on the distribution point, and there's a change, the site uses BDR to replicate the block-level change instead of the entire file. This behavior only applies when you enable the object to use BDR.<!-- SCCMDocs#2026 -->

#### Summary of delta replication

- *File*-level differences
- On by default, not configurable
- When a package changes, the site checks for changes to the individual files instead of the entire package.
    - If a file changes, use BDR to do the work
    - If there's a new file, copy the new file


## Peer caching technologies

<!-- SCCMDocs#1044 -->

Configuration Manager supports several options for managing content between peer devices on the same network:

- [BranchCache](#branchcache)
- [Delivery Optimization](#delivery-optimization)
- [Configuration Manager peer cache](#peer-cache)

Use the following table to compare major features of these technologies:

| Feature  | Peer&nbsp;cache  | Delivery&nbsp;Optimization  | BranchCache  |
|---------|---------|---------|---------|
| Across subnets | Yes | Yes | No |
| Throttle bandwidth | Yes (BITS) | Yes (native) | Yes (BITS) |
| Partial content | Yes | Yes | Yes |
| Control cache size on disk | Yes | Yes | Yes |
| Peer source discovery | Manual (client setting) | Automatic | Automatic |
| Peer discovery | Via management point using boundary groups | DO cloud service | Broadcast |
| Reporting | Client data sources dashboard | Client data sources dashboard | Client data sources dashboard |
| WAN usage control | Boundary groups | DO GroupID | Subnet only |
| Supported content | All ConfigMgr content | Windows updates, drivers, store apps | All ConfigMgr content |
| Policy control | Client agent settings | Client agent settings (partial) | Client agent settings |

### Recommendations

- Modern management: If you're already using modern tools such as Intune, implement Delivery Optimization

- Configuration Manager and co-management: Use a combination of peer cache and Delivery Optimization. Use peer cache with on-premises distribution points, and use Delivery Optimization for cloud scenarios.

- Existing BranchCache implemented: Use all three technologies in parallel. Use peer cache and Delivery Optimization for scenarios that aren't supported by BranchCache.


## BranchCache

[BranchCache](/windows-server/networking/branchcache/branchcache) is a Windows technology. Clients that support BranchCache, and have downloaded a deployment that you configure for BranchCache, then serve as a content source to other BranchCache-enabled clients.  

For example, you have a distribution point that runs Windows Server 2012 or later, and is configured as a BranchCache server. When the first BranchCache-enabled client requests content from this server, the client downloads that content and caches it.  

- That client then makes the content available for additional BranchCache-enabled clients on the same subnet that also cache the content.  
- Other clients on the same subnet don't have to download content from the distribution point.  
- The content is distributed across multiple clients for future transfers.  

For more information, see [Support for Windows BranchCache](../configs/support-for-windows-features-and-networks.md#bkmk_branchcache).

## Delivery Optimization

<!-- 1324696 -->
You use Configuration Manager boundary groups to define and regulate content distribution across your corporate network and to remote offices. [Windows Delivery Optimization](/windows/deployment/update/waas-delivery-optimization) is a cloud-based, peer-to-peer technology to share content between Windows 10 or later devices. Configure Delivery Optimization to use your boundary groups when sharing content among peers. Client settings apply the boundary group identifier as the Delivery Optimization group identifier on the client. When the client communicates with the Delivery Optimization cloud service, it uses this identifier to locate peers with the content. For more information, see [delivery optimization](../../clients/deploy/about-client-settings.md#delivery-optimization) client settings.

Delivery Optimization is the recommended technology to optimize Windows update delivery of express installation files for Windows quality updates. Internet access to the Delivery Optimization cloud service is a requirement to utilize its peer-to-peer functionality. For information about the needed internet endpoints, see [Frequently asked questions for Delivery Optimization](/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions). Optimization can be used for all Windows updates. For more information, see [optimize Windows update delivery](../../../sum/deploy-use/optimize-windows-10-update-delivery.md).

## Microsoft Connected Cache

<!--3555764-->
You can install a Microsoft Connected Cache server on your distribution points. By caching this content on-premises, your clients can benefit from the Delivery Optimization feature, but you can help to protect WAN links.

> [!NOTE]
> This feature was previously known as Delivery Optimization In-Network Cache.

This cache server acts as an on-demand transparent cache for content downloaded by Delivery Optimization. Use client settings to make sure this server is offered only to the members of the local Configuration Manager boundary group.

This cache is separate from Configuration Manager's distribution point content. If you choose the same drive as the distribution point role, it stores content separately.

For more information, see [Microsoft Connected Cache in Configuration Manager](microsoft-connected-cache.md).

## Peer cache

Client peer cache helps you manage deployment of content to clients in remote locations. Peer cache is a built-in Configuration Manager solution that enables clients to share content with other clients directly from their local cache.

First deploy client settings that enable peer cache to a collection. Then members of that collection can act as a peer content source for other clients in the same boundary group.

Client peer cache sources can divide content into parts. These parts minimize the network transfer to reduce WAN utilization. The management point provides more detailed tracking of the content parts. It tries to eliminate more than one download of the same content per boundary group.<!--1357346-->

For more information, see [Peer cache for Configuration Manager clients](client-peer-cache.md).

## Windows PE peer cache

When you deploy a new OS with Configuration Manager, computers that run the task sequence can use Windows PE peer cache. They download content from a peer cache source instead of from a distribution point. This behavior helps minimize WAN traffic in branch office scenarios where there's no local distribution point.

For more information, see [Windows PE peer cache](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).

## Windows LEDBAT

<!--1358112-->
Windows Low Extra Delay Background Transport (LEDBAT) is a network congestion control feature of Windows Server to help manage background network transfers. For distribution points running on supported versions of Windows Server, enable an option to help adjust network traffic. Then clients only use network bandwidth when it's available.

For more information on Windows LEDBAT in general, see the [New transport advancements](https://techcommunity.microsoft.com/t5/Networking-Blog/Announcing-Transport-Features-and-Performance-Advancements-in/ba-p/339726) blog post.

For more information on how to use Windows LEDBAT with Configuration Manager distribution points, see the setting to **Adjust the download speed to use the unused network bandwidth (Windows LEDBAT)** when you [Configure the general settings of a distribution point](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-general).

> [!Note]
> Staring in Configuration Manager version 2203, you can use LEDBAT with your software update points<!--4639895-->. If a site system has both the distribution point and software update point roles, you can configure LEDBAT independently on the roles. For more information, see the setting **Adjust the download speed to use the unused network bandwidth (Windows LEDBAT)** setting for [Installing software update points](../../../sum/get-started/install-a-software-update-point.md#bkmk_ledbat).  

## Client locations

The following are locations that clients access content from:

- **Intranet** (on-premises):

  - Distribution points can use HTTP or HTTPs.

  - Only use a content-enabled cloud management gateway for fallback when on-premises distribution points aren't available.

- **Internet**:

  - Requires internet-facing distribution points to accept HTTPS.

  - Can use a content-enabled cloud management gateway.

- **Workgroup**:

  - Requires distribution points to accept HTTPS.

  - Can use a content-enabled cloud management gateway.

## Content source priority

When a client needs content, it makes a content location request to the management point. The management point returns a list of source locations that are valid for the requested content. This list varies depending upon the specific scenario, technologies in use, site design, boundary groups, and deployment settings. For example, when a task sequence runs, the full Configuration Manager client isn't always running, so the behaviors may differ.<!-- SCCMDocs#1960 -->

The following list contains all of the possible content source locations that the Configuration Manager client can use, in the order in which it prioritizes them:  

1. The distribution point on the same computer as the client
2. A peer source in the same network subnet
3. A distribution point in the same network subnet
4. A peer source in the same boundary group
5. A distribution point in the current boundary group
6. A distribution point in a neighbor boundary group configured for fallback
7. A distribution point in the default site boundary group
8. The Windows Update cloud service
9. An internet-facing distribution point
10. A content-enabled cloud management gateway in Azure

Delivery Optimization isn't applicable to this source prioritization. This list is how the Configuration Manager client finds content. The Windows Update Agent downloads content for Delivery Optimization. If the Windows Update Agent can't find the content, then the Configuration Manager client uses this list to search for it.<!-- SCCMDocs#1607 -->

BranchCache applies to this list only when you enable a distribution point for BranchCache. For example, if a client gets to option #3 in the prioritization list, it first asks the distribution point for BranchCache metadata. The BranchCache-enabled distribution point is what provides the client information for BranchCache peer discovery. The client will download content from a BranchCache peer if it can. If it can't download the content via BranchCache, it then tries the distribution point itself, before continuing down the list of content sources. This behavior applies at any point in the priority list where the client uses a BranchCache-enabled distribution point. <!-- 8287190 -->

The configuration of [boundary group options](../../servers/deploy/configure/boundary-group-options.md) can modify the sort order of this priority list.

## Content library

The content library is the single-instance store of content in Configuration Manager. This library reduces the overall size of content that you distribute.  

- Learn more about the [content library](the-content-library.md).
- Use the [content library cleanup tool](content-library-cleanup-tool.md) to remove content that is no longer associated with an application.  


## Distribution points

Configuration Manager uses distribution points to store files that are required for software to run on client computers. Clients must have access to at least one distribution point from which they can download the files for content that you deploy.  

The basic (non-specialized) distribution point is commonly referred to as a standard distribution point. There are two variations on the standard distribution point that receive special attention:  

- **Pull-distribution point**: A variation of a distribution point where the distribution point obtains content from another distribution point (a source distribution point). This process is similar to how clients download content from distribution points. Pull-distribution points can help you avoid network bandwidth bottlenecks that occur when the site server must directly distribute content to each distribution point. For more information, see [Use a pull-distribution point](use-a-pull-distribution-point.md).

- **Content-enabled cloud management gateway**: A variation of a distribution point that's installed on Microsoft Azure. For more information, see [Cloud management gateway overview](../../clients/manage/cmg/overview.md).

Standard distribution points support a range of configurations and features:  

- Use controls such as **schedules** or **bandwidth throttling** to help control this transfer.  

- Use other options, including **prestaged content**, and **pull-distribution points** to minimize and control network consumption.  

- **BranchCache**, **peer cache**, and **Delivery Optimization** are peer-to-peer technologies to reduce the network bandwidth that's used when you deploy content.  

- There are different configurations for OS deployments, such as **[PXE](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#configuring-distribution-points-to-accept-pxe-requests)** and **[Multicast](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#configure-distribution-points-to-support-multicast)**  

- Options for **mobile devices**  
  
Cloud and pull distribution points support many of these same configurations, but have limitations that are specific to each distribution point variation.  


## Distribution point groups

Distribution point groups are logical groupings of distribution points that can simplify content distribution.  

For more information, see [Manage distribution point groups](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage).


## Distribution point priority

The distribution point priority value is based on how long it took to transfer previous deployments to that distribution point.  

- This value is self-tuning. It's set on each distribution point to help Configuration Manager more quickly transfer content to more distribution points.  

- When you distribute content to multiple distributions points at the same time, or to a distribution point group, the site first sends the content to the server with the highest priority. Then it sends that same content to a distribution point with a lower priority.  

- Distribution point priority doesn't replace the distribution priority for packages. Package priority remains the deciding factor of when the site sends different content.  

For example, you have a package that has a high package priority. You distribute it to a server with a low distribution point priority. This high priority package always transfers before a package that has a lower priority. The package priority applies even if the site distributes lower priority packages to servers with higher distribution point priorities.

The high priority of the package ensures that Configuration Manager distributes that content to distribution points before it sends any packages with a lower priority.  

> [!NOTE]  
> Pull-distribution points also use a concept of priority to order the sequence of their source distribution points.  
>
> - The distribution point priority for content transfers to the server is distinct from the priority that pull-distribution points use. Pull-distribution points use their priority when they search for content from a source distribution point.  
> - For more information, see [Use a pull-distribution point](use-a-pull-distribution-point.md).  


## Fallback

Several things have changed with Configuration Manager current branch in the way that clients find a distribution point that has content, including fallback.

Clients that can't find content from a distribution point that's associated with their current boundary group fall back to use content source locations associated with neighbor boundary groups. To be used for fallback, a neighbor boundary group must have a defined relationship with the client's current boundary group. This relationship includes a configured time that must pass before a client that can't find content locally includes content sources from the neighbor boundary group as part of its search.

The concepts of preferred distribution points are no longer used, and settings for **Allow fallback source locations for content** are no longer available or enforced.

For more information, see [Boundary groups](../../servers/deploy/configure/boundary-groups.md).


## Network bandwidth

To help manage the amount of network bandwidth that's used when you distribute content, you can use the following options:  

- **Prestaged content**: Transferring content to a distribution point without distributing the content across the network.  

- **Scheduling and throttling**: Configurations that help you control when and how content is distributed to distribution points.  

For more information, see [Manage network bandwidth](manage-network-bandwidth.md).


## Network connection speed to content source

Several things have changed with Configuration Manager current branch in the way that clients find a distribution point that has content. These changes include the network speed to a content source.

Network connection speeds that define a distribution point as **Fast** or **Slow** are no longer used. Instead, each site system that's associated with a boundary group is treated the same.

For more information, see [Boundary groups](../../servers/deploy/configure/boundary-groups.md).


## On-demand content distribution

On-demand content distribution is an option for individual application and package deployments. This option enables on-demand content distribution to preferred servers.  

- To enable this setting for a deployment, enable: **Distribute the content for this package to preferred distribution points**.  

- When you enable this option for a deployment, and a client requests that content but the content isn't available on any of the client's preferred distribution points, Configuration Manager automatically distributes that content to the client's preferred distribution points.  

- Although this triggers Configuration Manager to automatically distribute the content to that client's preferred distribution points, the client might obtain that content from other distribution points before the preferred distribution points for the client receive the deployment. When this behavior occurs, the content will then be present on that distribution point for use by the next client that seeks that deployment.  

For more information, see [Boundary groups](../../servers/deploy/configure/boundary-groups.md).


## Package transfer manager

Package transfer manager is the site server component that transfers content to distribution points on other computers.  

For more information, see [Package transfer manager](package-transfer-manager.md).  


## Prestage content

Prestaging content is a process of transferring content to a distribution point without distributing the content across the network.  

For more information, see [Manage network bandwidth](manage-network-bandwidth.md).
