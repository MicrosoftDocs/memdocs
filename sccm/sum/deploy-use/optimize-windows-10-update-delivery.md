---
title: Optimize Windows 10 update delivery
titleSuffix: Configuration Manager
description: Learn how to use Configuration Manager to manage update content to stay current with Windows 10.  
ms.date: 06/15/2018
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: b670cfaf-96a4-4fcb-9caa-0f2e8c2c6198
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Optimize Windows 10 update delivery with Configuration Manager

*Applies to: System Center Configuration Manager (current branch)*

For many customers, a successful path to getting and staying current with Windows 10 monthly updates starts with a good content distribution strategy using Configuration Manager. The size of the monthly quality updates can be a cause of concern for large organizations. There are a few technologies available that are intended to help reduce bandwidth and network load to optimize update delivery. This article explains these technologies, compares them, and provides recommendations to help you make decisions on which one to use.  
 
Windows 10 provides several types of updates. For more information, see [Update types in Windows Update for Business](https://docs.microsoft.com/windows/deployment/update/waas-manage-updates-wufb#update-types). This article focuses on Windows 10 *quality* updates with Configuration Manager. 


## Express update delivery

Windows 10 quality update downloads can be large. Every package contains all previously released fixes to ensure consistency and simplicity. Microsoft has been able to reduce the size of Windows 10 update content that each client downloads with a feature called express. Express is used today by millions of devices that pull updates directly from the Windows Update service and significantly reduces the download size. This benefit is also available to customers whose clients don't directly download from the Windows Update service. 

Configuration Manager added support for [express installation files](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates) of Windows 10 quality updates in version 1702. However, for the best experience it's recommended that you use Configuration Manager version 1802 or later. For the best performance in download speeds, it's also recommended that you use Windows 10, version 1703 or later. 

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

[Delivery Optimization](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) is the main download technology and peer-to-peer distribution method built into Windows 10. Windows 10 clients can get content from other devices on their local network that download the same updates. Using the [Windows options available for Delivery Optimization](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#delivery-optimization-options), you can configure clients into groups. This grouping allows your organization to identify devices that are possibly the best candidates to fulfill peer-to-peer requests. Delivery Optimization significantly reduces the overall bandwidth that's used to keep devices up-to-date while speeding up the download time.

> [!NOTE]  
> Delivery Optimization is a cloud-managed solution. Internet access to the Delivery Optimization cloud service is a requirement to utilize its peer-to-peer functionality.  

For the best results, you may need to set the Delivery Optimization [download mode](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#download-mode) to **Group (2)** and define *Group IDs*. In group mode, peering can cross internal subnets between devices that belong to the same group including devices in remote offices. Use the [Group ID option](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#select-the-source-of-group-ids) to create your own custom group independently of domains and AD DS sites. Group download mode is the recommended option for most organizations looking to achieve the best bandwidth optimization with Delivery Optimization.

Manually configuring these Group IDs is challenging when clients roam across different networks. Configuration Manager version 1802 added a new feature to simplify management of this process by [integrating boundary groups with Delivery Optimization](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#delivery-optimization). When a client wakes up, it talks to its management point to get policies, and provides its network and boundary group information. Configuration Manager creates a unique ID for every boundary group. The site uses the client's location information to automatically configure the client's Delivery Optimization Group ID with the Configuration Manager boundary ID. When the client roams to another boundary group, it talks to its management point, and is automatically reconfigured with a new boundary group ID. With this integration, Delivery Optimization can utilize the Configuration Manager boundary group information to find a peer from which to download updates.


### Configuration Manager peer cache

[Peer cache](/sccm/core/plan-design/hierarchy/client-peer-cache) is a feature of Configuration Manager that enables clients to share with other clients content directly from their local Configuration Manager cache. Peer cache doesn't replace the use of other peer caching solutions like Windows BranchCache. It works together with them to provide more options for extending traditional content deployment solutions such as distribution points. Peer cache doesn't rely upon BranchCache. If you don’t enable or use BranchCache, peer cache still works.

> [!NOTE]  
> Clients can only download content from peer cache clients that are in their current boundary group.  


### Windows BranchCache
[BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) is a bandwidth optimization technology in Windows. Each client has a cache, and acts as an alternate source for content. Devices on the same network can request this content. [Configuration Manager can use BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#bkmk_branchcache) to allow peers to source content from each other versus always having to contact a distribution point. Using BranchCache, files are cached on each individual client, and other clients can retrieve them as needed. This approach distributes the cache rather than having a single point of retrieval. This behavior saves a significant amount of bandwidth, while reducing the time for clients to receive the requested content. 



## Selecting the right peer caching technology

Selecting the right peer caching technology for express installation files depends upon your environment and requirements. Even though Configuration Manager supports all of the above peer-to-peer technologies, you should use those that make the most sense for your environment. For most customers, assuming clients can meet the internet requirements for Delivery Optimization, the Windows 10 built-in peer caching with Delivery Optimization should be sufficient. If your clients can't meet these internet requirements, consider using the Configuration Manager peer cache feature. If you're currently using BranchCache with Configuration Manager and it meets all your needs, then express files with BranchCache may be the right option for you. 

### Peer cache comparison chart


| Functionality  | Delivery Optimization  | Peer cache  | BranchCache  |
|---------|---------|---------|---------|
| Supported across subnets | Yes | Yes | No |
| Bandwidth throttling | Yes (Native) | Yes (via BITS) | Yes (via BITS) |
| Partial content support | Yes | Only for Office 365 and Express Updates | Yes |
| Cache size on disk control | Yes | Yes | Yes |
| Discovery of a peer source | Automatic | Manual (client agent setting) | Automatic |
| Peer discovery | Via Delivery Optimization cloud service (requires internet access) | Via management point (based on client boundary groups) | Multicast |
| Reporting | Yes (using Windows Analytics) | ConfigMgr client data sources dashboard | ConfigMgr client data sources dashboard |
| WAN usage control | Yes (native, can be controlled via group policy settings) | Boundary groups | Subnet support only |
| Supported content types | - Express updates (through ConfigMgr)</br> - Windows and security updates</br> - Drivers</br> - Windows Store apps</br> - Windows Store for Business apps | All ConfigMgr content types, including images downloaded in [Windows PE](/sccm/osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic) | All ConfigMgr content types, except images |
| Management through ConfigMgr | Partial (client agent setting) | Yes (client agent setting) | Yes (client agent setting) |



## Conclusion

Microsoft recommends that you optimize Windows 10 quality update delivery using Configuration Manager with express installation files and a peer caching technology, as needed. This approach should alleviate the challenges associated with Windows 10 devices downloading large content for installing quality updates. Keeping Windows 10 devices current by deploying quality updates each month is also recommended. This practice reduces the delta of quality update content needed by devices each month. Reducing this content delta causes smaller size downloads from distribution points or peer sources. 

Due to the nature of express installation files, their content size is considerably larger than traditional full-file content. This size results in longer update download times from the Windows Update service to the Configuration Manager site server. The amount of disk space required for both the site server and distribution points also increases. The total time required to download and distribute quality updates could be longer. However, the device-side benefits should be noticeable during the download and installation of quality updates by the Windows 10 devices.

If the server-side tradeoffs of larger-size updates are blockers for the adoption of express support, but the device-side benefits are critical to your business and environment, Microsoft recommends that you use [Windows Update for Business](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10) with Configuration Manager. Windows Update for Business provides all of the benefits of express without the need to download, store, and distribute express installation files throughout your environment. Clients download content directly from the Windows Update service, thus can still use Delivery Optimization.



## <a name="bkmk_faq"></a> Frequently asked questions

#### How do Windows express downloads work with Configuration Manager?

The Windows update agent (WUA) requests express content first. If it fails to install the express update, it can fall back to the full-file update.  

1. The Configuration Manager client tells WUA to download the update content. When WUA initiates an express download, it first downloads a stub (for example, `Windows10.0-KB1234567-<platform>-express.cab`), which is part of the express package.  

2. WUA passes this stub to the Windows update installer, component-based servicing (CBS). CBS uses the stub to do a local inventory, comparing the deltas of the file on the device with what is needed to get to the latest version of the file being offered.  

3. CBS then asks WUA to download the required ranges from one or more express .psf files.  

4. Delivery Optimization coordinates with Configuration Manager and downloads the ranges from a local distribution point or peers if available. If Delivery Optimization is disabled, the Background Intelligent Transfer Service (BITS) is used in the same manner with Configuration Manager coordinating peer cache sources. Delivery Optimization or BITS passes the ranges to WUA, which makes them available to CBS to apply and install.  


#### Why are the express files (.psf) so large when stored on Configuration Manager peer sources in the ccmcache folder?

The express files (.psf) are sparse files. To determine the actual space being used on disk by the file, check the **Size on disk** property of the file. The Size on disk property should be considerably smaller than the Size value.  


#### Does Configuration Manager support express installation files with Windows 10 feature updates?

No, Configuration Manager currently only supports express installation files with Windows 10 quality updates.  


#### How much disk space is needed per quality update on the site server and distribution points?

It depends. For each quality update, both the full-file and express version of the update are stored on servers. Windows 10 quality updates are cumulative, so the size of these files increases each month. Plan for a minimum of 5 GB per update per language. 


#### Do Configuration Manager clients still benefit from express installation files when falling back to the Windows Update service?

Yes. If you use the following software update deployment option, then clients still use express updates and Delivery Optimization when they fall back to the cloud service:  

**If software updates are not available on distribution point in current, neighbor or site groups, download content from Microsoft Updates**


#### Why is express file content not downloaded for existing updates after I enable express file support? 

The changes only take effect for any new updates synchronized and deployed after enabling support.


#### Is there any way to see how much content is downloaded from peers using Delivery Optimization?
Windows 10, version 1703 (and later) includes two new PowerShell cmdlets, **Get-DeliveryOptimizationPerfSnap** and **Get-DeliveryOptimizationStatus**. These cmdlets provide more insight into Delivery Optimization and cache usage. For more information, see [Windows PowerShell cmdlets for analyzing usage](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#windows-powershell-cmdlets-for-analyzing-usage)


#### How do clients communicate with Delivery Optimization over the network?
For more information about the network ports, proxy requirements, and hostnames for firewalls, see [FAQs for Delivery Optimization](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions).

