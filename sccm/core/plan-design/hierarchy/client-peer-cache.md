---
title: Client Peer Cache
titleSuffix: Configuration Manager
description: Use client peer cache for source locations when deploying content with Configuration Manager.
ms.date: 09/19/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Peer cache for Configuration Manager clients

*Applies to: System Center Configuration Manager (Current Branch)*

<!--1101436-->
Use peer cache to help manage deployment of content to clients in remote locations. Peer cache is a built-in Configuration Manager solution that enables clients to share content with other clients directly from their local cache.   

> [!Note]  
> Configuration Manager doesn't enable this optional feature by default. You must enable this feature before using it. For more information, see [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  



## Overview

Definitions:  

- **Peer cache client**: Any Configuration Manager client that downloads content from a peer  

- **Peer cache source**: A Configuration Manager client that you enable for peer cache, and that has content to share with other clients  

Use client settings to enable clients to be peer cache sources. You don't need to enable peer cache clients. When you enable clients to be peer cache sources, the management point includes them in the list of content location sources.<!--510397--> For more information on this process, see [Operations](#operations).  

A peer cache source must be a member of the current boundary group of the peer cache client. The management point doesn't include peer cache sources from a neighbor boundary group in the list of content sources it provides the client. It only includes distribution points from a neighbor boundary group. For more information about current and neighbor boundary groups, see [Boundary groups](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups##a-namebkmkboundarygroupsa-boundary-groups).<!--SCCMDocs issue 685-->  

The Configuration Manager client uses peer cache to serve to other clients every type of content in the cache. This content includes Office 365 files and express installation files.<!--SMS.500850-->  

Peer cache doesn't replace the use of other solutions like Windows BranchCache or Delivery Optimization. Peer cache works along with other solutions. These technologies give you more options for extending traditional content deployment solutions such as distribution points. Peer cache is a custom solution with no reliance on BranchCache. If you don't enable or use BranchCache, peer cache still works.  

  > [!Note]  
  > Starting in version 1802, Windows BranchCache is always enabled on deployments. The setting to **Allow clients to share content with other clients on the same subnet** is removed.<!--SCCMDocs issue 539--> If the distribution point supports it, and it's enabled in client settings, clients use BranchCache. For more information, see [Configure BranchCache](/sccm/core/clients/deploy/about-client-settings#configure-branchcache).<!--SCCMDocs issue 735-->   



## Operations

To enable peer cache, deploy the [client settings](#bkmk_settings) to a collection. Then members of that collection act as a peer cache source for other clients in the same boundary group.  

 -	A client that operates as a peer content source submits a list of available cached content to its management point.  

 -	Another client in the same boundary group makes a content location request to the management point. The server returns the list of potential content sources. This list includes each peer cache source that has the content and is online. It also includes the distribution points and other content source locations in that boundary group. For more information, see [Content source priority](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#content-source-priority).  

 -	As usual, the client that's seeking the content selects one source from the provided list. The client then attempts to get the content.  

Starting in version 1806, boundary groups include additional settings to give you more control over content distribution in your environment. For more information, see [Boundary group options for peer downloads](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_bgoptions).<!--1356193-->

> [!NOTE]  
> If the client falls back to a neighbor boundary group for content, the management point doesn't add the peer cache sources from the neighbor boundary group to the list of potential content source locations.  

Choose only clients best suited as peer cache sources. Evaluate client suitability based on attributes such as chassis type, disk space, and network connectivity. For more information that can help you select the best clients to use for peer cache, see [this blog by a Microsoft consultant](https://blogs.technet.microsoft.com/setprice/2016/06/29/pe-peer-cache-custom-reporting-examples/).


### Limited access to a peer cache source  

A peer cache source rejects requests for content when it meets any of the following conditions at the time a peer requests content:  

  -  Low battery mode  

  -  Processor load exceeds 80%  

  -  Disk I/O has an *AvgDiskQueueLength* that exceeds 10  

  -  There are no more available connections to the computer  

> [!Tip]  
> Configure these settings using the client configuration server WMI class for the peer source feature (*SMS_WinPEPeerCacheConfig*) in the Configuration Manager SDK.  

When the peer cache source rejects a request for the content, the peer cache client continues to seek content from its list of content source locations.   



## Requirements

- Peer cache supports all Windows versions listed as supported in [Supported operating systems for clients and devices](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices). Non-Windows operating systems aren't supported as peer cache sources or peer cache clients.  

- A peer cache source must be a domain-joined Configuration Manager client. However, a client that's not domain-joined can get content from a domain-joined peer cache source.  

- Clients can only download content from peer cache sources in their current boundary group.  

- A [network access account](/sccm/core/plan-design/hierarchy/manage-accounts-to-access-content#a-namebkmknaaa-network-access-account) isn't required with the following exception:  

    - Configure a network access account in the site when a peer cache-enabled client runs a task sequence from Software Center, and it reboots to a boot image. When the device is in Windows PE, it uses the network access account to get content from the peer cache source.  

    - When required, the peer cache source uses the network access account to authenticate download requests from peers. This account requires only domain user permissions for this purpose.  

- With version 1802 and prior, the client's last heartbeat discovery submission determines the current boundary of a peer cache source. A client that roams to a different boundary group might still be a member of its former boundary group for the purposes of peer cache. This behavior results in a client being offered a peer cache source that isn't in its immediate network location. Don't enable roaming clients as a peer cache source.<!--SCCMDocs issue 641-->  

    > [!Important]  
    > Starting in version 1806, Configuration Manager is more efficient at determining if a peer cache source has roamed to another location. This behavior makes sure the management point offers it as a content source to clients in the new location and not the old location. If you're using the peer cache feature with roaming peer cache sources, after updating the site to version 1806, also update all peer cache sources to the latest client version. The management point doesn't include these peer cache sources in the list of content locations until they are updated to at least version 1806.<!--SCCMDocs issue 850-->  

- Before attempting to download content, the management point first validates that the peer cache source is online.<!--sms.498675--> This validation happens via the "fast channel" for client notification, which uses TCP port 10123.<!--511673-->  

> [!Note]  
> To take advantage of new Configuration Manager features, first update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.  



## <a name="bkmk_settings"></a> Peer cache client settings

For more information about the peer cache client settings, see [Client cache settings](/sccm/core/clients/deploy/about-client-settings#client-cache-settings). 

For more information on configuring these settings, see [How to configure client settings](/sccm/core/clients/deploy/configure-client-settings).

On peer cache-enabled clients that use the Windows Firewall, Configuration Manager configures the firewall ports that you specify in client settings.



## <a name="bkmk_parts"></a> Partial download support
<!--1357346-->
Starting in version 1806, client peer cache sources can now divide content into parts. These parts minimize the network transfer to reduce WAN utilization. The management point provides more detailed tracking of the content parts. It tries to eliminate more than one download of the same content per boundary group. 


### Example scenario

Contoso has a single primary site with two boundary groups: Headquarters (HQ) and Branch Office. There's a 30-minute fallback relationship between the boundary groups. The management point and distribution point for the site are only in the HQ boundary. The branch office location has no local distribution point. Two of the four clients at the branch office are configured as peer cache sources. 

![Diagram of network configuration as described for the example scenario](media/1357346-peer-cache-source-parts.png)

1. You target a deployment with content to all four clients in the branch office. You only distributed the content to the distribution point.  

2. Client3 and Client4 don't have a local source for the deployment. The management point instructs the clients to wait 30 minutes before falling back to the remote boundary group.  

3. Client1 (PCS1) is the first peer cache source to refresh policy with the management point. Because this client is enabled as a peer cache source, the management point instructs it to immediately start downloading part A from the distribution point.  

4. When Client2 (PCS2) contacts the management point, as part A is already in progress but not yet complete, the management point instructs it to immediately start downloading part B from the distribution point.  

5. PCS1 finishes downloading part A, and immediately notifies the management point. As part B is already in progress but not yet complete, the management point instructs it to start downloading part C from the distribution point.  

6. PCS2 finishes downloading part B, and immediately notifies the management point. The management point instructs it to start downloading part D from the distribution point.  

7. PCS1 finishes downloading part C, and immediately notifies the management point. The management point informs it that there are no more parts available from the remote distribution point. The management point instructs it to download part B from its local peer, PCS2.  

8. This process continues until both client peer cache sources have all of the parts from each other. The management point prioritizes parts from the remote distribution point before instructing the peer cache sources to download parts from local peers.  

9. Client3 is the first to refresh policy after the 30-minute fallback period expires. It now checks back with the management point, which informs the client of new local sources. Instead of downloading the content in full from the distribution point across the WAN, it downloads the content in full from one of the client peer cache sources. Clients prioritize local peer sources. 

> [!Note]  
> If the number of client peer cache sources is greater than the number of content parts, then the management point instructs the additional peer cache sources to wait for fallback like a normal client. 


### Configure partial download

1. Set up [boundary groups](/sccm/core/servers/deploy/configure/boundary-groups) and peer cache sources per normal.  

2. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select **Sites**. Click **Hierarchy Settings** in the ribbon.  

3. On the **General** tab, enable the option to **Configure client peer cache sources to divide content into parts**.  

4. Create a required deployment with content.  

   > [!Note]  
   > This functionality only works when the client downloads content in the background, such as with a required deployment. On-demand downloads, such as when the user installs an available deployment in Software Center, behaves as usual.  

To see them handling the download of content in parts, examine the **ContentTransferManager.log** on the client peer cache source and the **MP_Location.log** on the management point.  



## Guidance for cache management
<!--510645-->
Peer cache relies on the Configuration Manager client cache to share content. Consider the following points for managing the client cache in your environment:  

- The Configuration Manager client cache isn't like the content library on a distribution point. While you manage the content that you distribute to a distribution point, the Configuration Manager client automatically manages the content in its cache. There are settings and methods to help control what content is in the cache of a peer cache source. For more information, see [Configure the client cache for Configuration Manager clients](/sccm/core/clients/manage/manage-clients#BKMK_ClientCache).  

- Normal cache size and maintenance applies to peer cache sources. For more information, see [Configure client cache size](/sccm/core/clients/deploy/about-client-settings#configure-client-cache-size). Consider the size of larger content such as OS upgrade packages or Windows 10 express update files. Compare your need for this content against the available disk space on peer cache sources.  

- The peer cache source client updates the last referenced time of content in the cache when a peer downloads it. The client uses this timestamp when it automatically maintains its cache, removing older content first. So it should wait to remove content that peer cache clients more frequently download, if at all.  

- If necessary, during an OS deployment task sequence, use the **SMSTSPreserveContent** variable to keep content in the client cache. For more information, see [Task sequence variables](/sccm/osd/understand/task-sequence-variables#SMSTSPreserveContent).  

- If necessary, when creating the following software, use the option to **Persist content in the client cache**:  
    - Applications
    - Packages
    - OS images
    - OS upgrade packages
    - Boot images



## Monitoring   

To help you understand the use of peer cache, view the **Client Data Sources** dashboard. For more information, see [Client data sources dashboard](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).

Also use reports to view peer cache use. In the console, go to the **Monitoring** workspace, expand **Reporting**, and select the **Reports** node. The following reports all have a type of **Software Distribution Content**:  

1.  **Peer cache source content rejection**: How often the peer cache sources in a boundary group reject a content request.  

    > [!Note]  
    > **Known issue**<!--486652-->: When drilling down on results like *MaxCPULoad* or *MaxDiskIO*, you might receive an error that suggests the report or details can't be found. To work around this issue, use the other two reports that directly show the results.  

2. **Peer cache source content rejection by condition**: Shows rejection details for a specified boundary group or rejection type. 

    > [!Note]  
    > **Known issue**<!--486652-->: You can't select from available parameters and instead must enter them manually. Enter the values for *Boundary Group Name* and *Rejection Type* as seen in the **Peer cache source content rejection** report. For example, for *Rejection Type* you might enter *MaxCPULoad* or *MaxDiskIO*.  

3. **Peer cache source content rejection details**: Show the content that the client was requesting when rejected.  

    > [!Note]  
    > **Known issue**<!--486652-->: You can't select from available parameters and instead must enter them manually. Enter the value for *Rejection Type* as displayed in the **Peer cache source content rejection** report. Then enter the *Resource ID* for the content source about which you want more information. 
    > 
    > To find the Resource ID of the content source:  
    > 
    > 1. Find the computer name that displays as the *Peer cache source* in the results of the **Peer cache source content rejection by condition** report.  
    > 
    > 2. Go to the **Assets and Compliance** workspace, select the **Devices** node, and search for that computer's name. Use the value from the Resource ID column.  

