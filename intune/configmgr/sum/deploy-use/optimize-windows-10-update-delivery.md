---
title: Optimize Windows update delivery
titleSuffix: Configuration Manager
description: Learn how to use Configuration Manager to manage update content to stay current with Windows.
ms.date: 02/11/2025
ms.service: configuration-manager
ms.subservice: software-updates
ms.topic: how-to
author: LauraWi
ms.author: laurawi
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart
ms.collection: tier3
---

# Software Update content delivery with Configuration Manager

> [!WARNING]
> Express Updates are no longer valid in Configuration Manager and should not be selected in the console. This functionality has been replaced by UUP for Windows 11 / Server 2025. In upcoming versions of the product, the Express Update option will be removed completely.


## Express update delivery

This feature is no longer available and has been replaced by UUP.


### Windows Delivery Optimization

Configuration Manager version 1802 added an optional client setting to simplify management of this process by [integrating boundary groups with Delivery Optimization](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization). When this client setting is enabled, Configuration Manager creates a unique ID for every boundary group. The site uses the client's location information to automatically configure the client's Delivery Optimization Group ID with the Configuration Manager boundary ID. When the client roams to another boundary group, it talks to its management point, and is automatically reconfigured with a new boundary group ID. With this integration, Delivery Optimization can utilize the Configuration Manager boundary group information to find a peer from which to download updates.

> [!IMPORTANT]
> - When using Configuration Manager to manage software updates, the Delivery Optimization service must be enabled (default) and not bypassed or configured by any domain GPO. For more information, see [Windows Delivery Optimization reference](/windows/deployment/update/waas-delivery-optimization-reference).
- The client setting for Delivery Optimization is not needed for UUP updates and in most cases this client setting should not be enabled.


### <a name="bkmk_DO-1910"></a>Delta Download client setting

<!--4699118-->
Starting in Configuration Manager 2203, the Delta Download option in the [software updates client settings](../../core/clients/deploy/about-client-settings.md#software-updates) must be configured as follows:

- **Allow clients to download delta content when available** set to **No**.
- **Port that clients use to receive requests for delta content** set to 8005 (default) or a custom port number.


#### Limitations

- Delivery Optimization can't be used for Microsoft 365 Apps client updates if Office COM is enabled. Office COM is used by Configuration Manager to manage updates for Microsoft 365 Apps clients. You can deregister Office COM to allow the use of Delivery Optimization for Microsoft 365 Apps updates. When Office COM is disabled, software updates for Microsoft 365 Apps are managed by the default Office Automatic Updates 2.0 scheduled task. This means that Configuration Manager doesn't dictate or monitor the installation process for Microsoft 365 Apps updates. Configuration Manager will continue to collect information from hardware inventory to populate Office 365 Client Management Dashboard in the console. For information about how to deregister Office COM, see [Enable Office 365 clients to receive updates from the Office CDN instead of Configuration Manager](/deployoffice/manage-office-365-proplus-updates-with-configuration-manager#enable-office-365-clients-to-receive-updates-from-the-office-cdn-instead-of-configuration-manager).

 - When using a CMG for content storage, the content for third-party updates won't download to clients if the **Download delta content when available** [client setting](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) is enabled. <!--6598587-->

- Download of [feature updates](../get-started/configure-classifications-and-products.md) for Windows may take a long time depending on the network and if additional content is determined to be needed for installation. This additional download time may also cause the installation to fail because it exceed the [maximum runtime](../get-started/manage-settings-for-software-updates.md#BKMK_SetMaxRunTime). <!--7328656-->

### Configuration Manager peer cache

[Peer cache](../../core/plan-design/hierarchy/client-peer-cache.md) is a feature of Configuration Manager that enables clients to share with other clients content directly from their local Configuration Manager cache. Peer cache has several limitations and doesn't replace the use of distribution points. It's only ideal for special circumstances, such as a remote office with just a few employees. The number of peer cache sources must be kept to a minimum or performance issues can occur in the site and with the SQL database.

> [!NOTE]
> Clients can only download content from peer cache clients that are in their current boundary group.


### Windows BranchCache
[BranchCache](/windows-server/networking/branchcache/branchcache) is a bandwidth optimization technology in Windows. Each client has a cache, and acts as an alternate source for content. Devices on the same network can request this content. [Configuration Manager can use BranchCache](../../core/plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache) to allow peers to source content from each other versus always having to contact a distribution point. Using BranchCache, files are cached on each individual client, and other clients can retrieve them as needed. This approach distributes the cache rather than having a single point of retrieval. This behavior saves a significant amount of bandwidth, while reducing the time for clients to receive the requested content.



## Selecting the right technology

Even though Configuration Manager supports all of the above peer-to-peer technologies, you should use those that make the most sense for your environment. For most customers, assuming clients can meet the internet requirements for Delivery Optimization, the Windows 10 or later built-in Delivery Optimization settings will be sufficient. Distribution Points and content enabled CMG's are always the preferred content delivery method.

### Peer cache comparison chart


| Functionality  | Delivery Optimization  | Peer cache  | BranchCache  |
|---------|---------|---------|---------|
| Supported across subnets | Yes | Yes | No |
| Bandwidth throttling | Yes (Native) | Yes (via BITS) | Yes (via BITS) |
| Partial content support | Yes, for all supported content types listed in this column's next row. | Only for Microsoft 365 Apps and Express Updates | Yes, for all supported content types listed in this column's next row. |
| Supported content types | **Through ConfigMgr:** </br> - Express updates </br> - All Windows updates (starting version 1910). This doesn't include Microsoft 365 Apps updates.</br> </br> **Through Microsoft cloud:**</br> - Windows and security updates</br> - Drivers</br> - Windows Store apps</br> - Windows Store for Business apps | All ConfigMgr content types, including images downloaded in [Windows PE](../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md) | All ConfigMgr content types, except images |
| Cache size on disk control | Yes | Yes | Yes |
| Discovery of a peer source | Automatic | Manual (client agent setting) | Automatic |
| Peer discovery | Via Delivery Optimization cloud service (requires internet access) | Via management point (based on client boundary groups) | Multicast |
| Reporting | [Update Compliance](/windows/deployment/update/update-compliance-get-started) | ConfigMgr client data sources dashboard | ConfigMgr client data sources dashboard |
| WAN usage control | Yes (native, can be controlled via group policy settings) | Boundary groups | Subnet support only |
| Management through ConfigMgr | Partial (client agent setting) | Yes (client agent setting) | Yes (client agent setting) |



## <a name="bkmk_faq"></a>Frequently asked questions

#### Does Configuration Manager support express installation files?

No, Configuration Manager no longer support Express Updates.

#### How much disk space is needed per quality update on the site server and distribution points?

It depends. For each quality update, both the full-files of the update are stored on servers. Windows quality updates are cumulative, so the size of these files increases each month. Plan for a minimum of 5 GB per update per language. The size of UUP updates may be larger than traditional non-UUP updates.

#### Is there any way to see how much content is downloaded from peers using Delivery Optimization?
Windows includes two PowerShell cmdlets, **Get-DeliveryOptimizationPerfSnap** and **Get-DeliveryOptimizationStatus**. These cmdlets provide more insight into Delivery Optimization and cache usage. For more information, see [Delivery Optimization for Windows updates](/windows/deployment/update/waas-delivery-optimization#the-cloud-service-doesnt-see-other-peers-on-the-network)


#### How do clients communicate with Delivery Optimization over the network?
For more information about the network ports, proxy requirements, and hostnames for firewalls, see [FAQs for Delivery Optimization](/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions).

## Log files

Use the following log files to monitor delta downloads:

- WUAHandler.log
- DeltaDownload.log

## Next steps

- [Deploy software updates](deploy-software-updates.md)
- [Automatically deploy software updates](automatically-deploy-software-updates.md)

