---
title: Optimize Windows update delivery
titleSuffix: Configuration Manager
description: Learn how to use Configuration Manager to manage update content to stay current with Windows.
ms.date: 10/20/2021
ms.service: configuration-manager
ms.subservice: software-updates
ms.topic: conceptual
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Optimize Windows 10 or later update delivery with Configuration Manager

*Applies to: Configuration Manager (current branch)*

For many customers, a successful path to getting and staying current with Windows monthly updates starts with a good content distribution strategy using Configuration Manager. The size of the monthly quality updates can be a cause of concern for large organizations. There are a few technologies available that are intended to help reduce bandwidth and network load to optimize update delivery. This article explains these technologies, compares them, and provides recommendations to help you make decisions on which one to use.  
 
Windows provides several types of updates. For more information, see [Update types in Windows Update for Business](/windows/deployment/update/waas-manage-updates-wufb#types-of-updates-managed-by-windows-update-for-business). This article focuses on Windows *quality* updates with Configuration Manager. 


## Express update delivery

Windows quality update downloads can be large. Every package contains all previously released fixes to ensure consistency and simplicity. Microsoft has been able to reduce the size of Windows update content that each client downloads with a feature called express. Express is used today by millions of devices that pull updates directly from the Windows Update service and significantly reduces the download size. This benefit is also available to customers whose clients don't directly download from the Windows Update service. 

Configuration Manager supports [express installation files](manage-express-installation-files-for-windows-10-updates.md) of Windows 10 or later quality updates. For the best performance in download speeds, it's also recommended that you use Windows 10, version 1703 or later. 

> [!NOTE]  
> The express version content is considerably larger than the full-file version. An express installation file contains all of the possible variations for each file it's meant to update. As a result, the required amount of disk space increases for updates in the update package source and on distribution points when you enable express support in Configuration Manager. Even though the disk space requirement on the distribution points increases, the content size that clients download from these distribution points decreases. Clients only download the bits they require (deltas) but not the whole update.


## Peer-to-peer content distribution

Even though clients download only the parts of the content that they require, expedite Windows updates in your environment by utilizing peer-to-peer content distribution. Leveraging peers as a download source for quality updates can be beneficial for environments where local distribution points aren't present in remote offices. This behavior prevents the need for all clients to download content from a remote distribution point across a slow WAN link. Using peers can also be beneficial when clients fallback to the Windows Update service. Only one peer is needed to download update content from the cloud before making it available to other devices.

Configuration Manager supports many peer-to-peer technologies, including the following:
- Windows Delivery Optimization
- Configuration Manager peer cache
- Windows BranchCache  

The next sections provide further information on these technologies.

### Windows Delivery Optimization

[Delivery Optimization](/windows/deployment/update/waas-delivery-optimization) is the main download technology and peer-to-peer distribution method built into Windows 10 and later. Windows clients can get content from other devices on their local network that download the same updates. Using the [Windows options available for Delivery Optimization](/windows/deployment/update/waas-delivery-optimization-reference#delivery-optimization-options), you can configure clients into groups. This grouping allows your organization to identify devices that are possibly the best candidates to fulfill peer-to-peer requests. Delivery Optimization significantly reduces the overall bandwidth that's used to keep devices up-to-date while speeding up the download time.

> [!NOTE]  
> Delivery Optimization is a cloud-managed solution. Internet access to the Delivery Optimization cloud service is a requirement to utilize its peer-to-peer functionality. For information about the needed internet endpoints, see [Frequently asked questions for Delivery Optimization](/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions). 

For the best results, you may need to set the Delivery Optimization [download mode](/windows/deployment/update/waas-delivery-optimization-reference#download-mode) to **Group (2)** and define *Group IDs*. In group mode, peering can cross internal subnets between devices that belong to the same group including devices in remote offices. Use the [Group ID option](/windows/deployment/update/waas-delivery-optimization-reference#select-the-source-of-group-ids) to create your own custom group independently of domains and AD DS sites. Group download mode is the recommended option for most organizations looking to achieve the best bandwidth optimization with Delivery Optimization.

Manually configuring these Group IDs is challenging when clients roam across different networks. Configuration Manager version 1802 added a new feature to simplify management of this process by [integrating boundary groups with Delivery Optimization](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization). When a client wakes up, it talks to its management point to get policies, and provides its network and boundary group information. Configuration Manager creates a unique ID for every boundary group. The site uses the client's location information to automatically configure the client's Delivery Optimization Group ID with the Configuration Manager boundary ID. When the client roams to another boundary group, it talks to its management point, and is automatically reconfigured with a new boundary group ID. With this integration, Delivery Optimization can utilize the Configuration Manager boundary group information to find a peer from which to download updates.

### <a name="bkmk_DO-1910"></a> Delivery Optimization with Configuration Manager
<!--4699118-->
With Configuration Manager, you can use Delivery Optimization for the distribution of all Windows update content for clients running Windows 10 version 1709 or later, not just express installation files.

To use Delivery Optimization for all Windows update installation files, enable the following [software updates client settings](../../core/clients/deploy/about-client-settings.md#software-updates):

- **Allow clients to download delta content when available** set to **Yes**.
- **Port that clients use to receive requests for delta content** set to 8005 (default) or a custom port number.
 
> [!IMPORTANT]
> - Delivery Optimization must be enabled (default) and not bypassed. For more information, see [Windows Delivery Optimization reference](/windows/deployment/update/waas-delivery-optimization-reference).
> - Verify your [Delivery Optimization client settings](../../core/clients/deploy/about-client-settings.md#delivery-optimization) when changing your [software updates client settings](../../core/clients/deploy/about-client-settings.md#software-updates) for delta content.

#### Limitations

- Delivery Optimization can't be used for Microsoft 365 Apps client updates if Office COM is enabled. Office COM is used by Configuration Manager to manage updates for Microsoft 365 Apps clients. You can deregister Office COM to allow the use of Delivery Optimization for Microsoft 365 Apps updates. When Office COM is disabled, software updates for Microsoft 365 Apps are managed by the default Office Automatic Updates 2.0 scheduled task. This means that Configuration Manager doesn't dictate or monitor the installation process for Microsoft 365 Apps updates. Configuration Manager will continue to collect information from hardware inventory to populate Office 365 Client Management Dashboard in the console. For information about how to deregister Office COM, see [Enable Office 365 clients to receive updates from the Office CDN instead of Configuration Manager](/deployoffice/manage-office-365-proplus-updates-with-configuration-manager#enable-office-365-clients-to-receive-updates-from-the-office-cdn-instead-of-configuration-manager).

 - When using a CMG for content storage, the content for third-party updates won't download to clients if the **Download delta content when available** [client setting](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) is enabled. <!--6598587-->
 
- Download of [feature updates](../get-started/configure-classifications-and-products.md) for Windows may take a long time depending on the network and if additional content is determined to be needed for installation. This additional download time may also cause the installation to fail because it exceed the [maximum runtime](../get-started/manage-settings-for-software-updates.md#BKMK_SetMaxRunTime). <!--7328656-->

#### Configuration recommendations for clients downloading delta content
<!--7913814-->
When the **Allow clients to download delta content when available** [client setting](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) is enabled on clients for software update content, there are limitations in the [distribution point fallback](../../core/servers/deploy/configure/boundary-group-procedures.md#configure-a-fallback-site-for-automatic-site-assignment) behavior. To ensure these clients can properly download software update content, we recommend the following configurations:

- Ensure that clients are in a boundary group and that there's a reliable distribution point that has the needed content associated with that boundary group.
- Deploy software updates with fallback to Microsoft Update enabled for clients that are able to download directly from the internet.
   - The deployment setting for this fallback behavior is **If software updates are not available on distribution point in current, neighbor or site boundary groups, download content from Microsoft Updates** and it's found on the **Download Settings** page. For more information, see [Deploy software updates](manually-deploy-software-updates.md#process-to-manually-deploy-the-software-updates-in-a-software-update-group).

If either of the above options aren't viable, **Allow clients to download delta content when available** can be disabled in the client settings to allow fallbacks functionality. Delivery Optimization peering won't be leveraged in this case since the client won't use the delta channel.

> [!Tip]
> Starting in Configuration Manager version 2010, if delta content is unavailable from distribution points in the current boundary group, you can immediately fallback to a neighbor or the site default. For more information, see [Client settings for software updates](../../core/clients/deploy/about-client-settings.md#software-updates).

### Configuration Manager peer cache

[Peer cache](../../core/plan-design/hierarchy/client-peer-cache.md) is a feature of Configuration Manager that enables clients to share with other clients content directly from their local Configuration Manager cache. Peer cache doesn't replace the use of other peer caching solutions like Windows BranchCache. It works together with them to provide more options for extending traditional content deployment solutions such as distribution points. Peer cache doesn't rely upon BranchCache. If you don't enable or use BranchCache, peer cache still works.

> [!NOTE]  
> Clients can only download content from peer cache clients that are in their current boundary group.  


### Windows BranchCache
[BranchCache](/windows-server/networking/branchcache/branchcache) is a bandwidth optimization technology in Windows. Each client has a cache, and acts as an alternate source for content. Devices on the same network can request this content. [Configuration Manager can use BranchCache](../../core/plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache) to allow peers to source content from each other versus always having to contact a distribution point. Using BranchCache, files are cached on each individual client, and other clients can retrieve them as needed. This approach distributes the cache rather than having a single point of retrieval. This behavior saves a significant amount of bandwidth, while reducing the time for clients to receive the requested content.



## Selecting the right peer caching technology

Selecting the right peer caching technology for express installation files depends upon your environment and requirements. Even though Configuration Manager supports all of the above peer-to-peer technologies, you should use those that make the most sense for your environment. For most customers, assuming clients can meet the internet requirements for Delivery Optimization, the Windows 10 or later built-in peer caching with Delivery Optimization should be sufficient. If your clients can't meet these internet requirements, consider using the Configuration Manager peer cache feature. If you're currently using BranchCache with Configuration Manager and it meets all your needs, then express files with BranchCache may be the right option for you. 

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



## Conclusion

Microsoft recommends that you optimize Windows 10 or later quality update delivery using Configuration Manager with express installation files and a peer caching technology, as needed. This approach should alleviate the challenges associated with Windows devices downloading large content for installing quality updates. Keeping Windows devices current by deploying quality updates each month is also recommended. This practice reduces the delta of quality update content needed by devices each month. Reducing this content delta causes smaller size downloads from distribution points or peer sources. 

Due to the nature of express installation files, their content size is considerably larger than traditional self-contained files. This size results in longer update download times from the Windows Update service to the Configuration Manager site server. The amount of disk space required for both the site server and distribution points also increases. The total time required to download and distribute quality updates could be longer. However, the device-side benefits should be noticeable during the download and installation of quality updates by the devices. For more information, see [Using Express Installation Files](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc708456(v=ws.10)#using-express-installation-files).

If the server-side tradeoffs of larger-size updates are blockers for the adoption of express support, but the device-side benefits are critical to your business and environment, Microsoft recommends that you use [Windows Update for Business](integrate-windows-update-for-business-windows-10.md) with Configuration Manager. Windows Update for Business provides all of the benefits of express without the need to download, store, and distribute express installation files throughout your environment. Clients download content directly from the Windows Update service, thus can still use Delivery Optimization.



## <a name="bkmk_faq"></a> Frequently asked questions

#### How do Windows express downloads work with Configuration Manager?

The Windows update agent (WUA) requests express content first. If it fails to install the express update, it can fall back to the full-file update.  

1. The Configuration Manager client tells WUA to download the update content. When WUA initiates an express download, it first downloads a stub (for example, `Windows10.0-KB1234567-<platform>-express.cab`), which is part of the express package.  

2. WUA passes this stub to the Windows update installer, component-based servicing (CBS). CBS uses the stub to do a local inventory, comparing the deltas of the file on the device with what is needed to get to the latest version of the file being offered.  

3. CBS then asks WUA to download the required ranges from one or more express .psf files.  

4. If Delivery Optimization is enabled and peers are discovered to have the needed ranges, the client will download from peers independently of the ConfigMgr client. If Delivery Optimization is disabled or no peers have the needed ranges, the ConfigMgr client will download these ranges from a local distribution point (or a peer or Microsoft Update). The ranges are passed to the Windows Update Agent which makes them available to CBS to apply the ranges.


#### Why are the express files (.psf) so large when stored on Configuration Manager peer sources in the ccmcache folder?

The express files (.psf) are sparse files. To determine the actual space being used on disk by the file, check the **Size on disk** property of the file. The Size on disk property should be considerably smaller than the Size value.  


#### Does Configuration Manager support express installation files with Windows feature updates?

No, Configuration Manager currently only supports express installation files with Windows 10 or later quality updates.  


#### How much disk space is needed per quality update on the site server and distribution points?

It depends. For each quality update, both the full-file and express version of the update are stored on servers. Windows quality updates are cumulative, so the size of these files increases each month. Plan for a minimum of 5 GB per update per language. 


#### Do Configuration Manager clients still benefit from express installation files when falling back to the Windows Update service?

Yes. If you use the following software update deployment option, then clients still use express updates and Delivery Optimization when they fall back to the cloud service:  

**If software updates are not available on distribution point in current, neighbor or site groups, download content from Microsoft Updates**


#### Why is express file content not downloaded for existing updates after I enable express file support? 

The changes only take effect for any new updates synchronized and deployed after enabling support.


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
