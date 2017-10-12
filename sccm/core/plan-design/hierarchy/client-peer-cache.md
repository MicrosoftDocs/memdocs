---
title: "Client Peer Cache"
titleSuffix: "Configuration Manager"
description: "Use Peer Cache for client content source locations when deploying content with System Center Configuration Manager."
ms.custom: na
ms.date: 7/31/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
---

# Peer Cache for Configuration Manager clients

*Applies to: System Center Configuration Manager (Current Branch)*

Beginning with System Center Configuration Manager version 1610, you can use **Peer Cache** to help manage deployment of content to clients in remote locations. Peer Cache is a built-in Configuration Manager solution that enables clients to share content with other clients directly from their local cache.   

> [!TIP]  
> Introduced with version 1610, Peer Cache and the Client Data Sources dashboard are pre-release features. To enable them, see [Use pre-release features from updates](/sccm/core/servers/manage/pre-release-features).

## Overview
A Peer Cache client is a Configuration Manager client that is enabled to use Peer Cache. A Peer Cache client that has content it can share with additional clients is a Peer Cache source.
 - 	You use client settings to enable clients to use Peer Cache.
 - 	To share content as a Peer Cache source, a Peer Cache client:
    -  Must be domain joined. However, a client that is not domain joined can get content from a domain joined Peer Cache source.
    -  Must be a member of the current boundary group of the client that's seeking the content. A Peer Cache client in a neighbor boundary group is not included with the pool of available content source locations when a client uses fallback to seek content from a neighbor boundary group. For more information about current and neighbor boundary groups, see [Boundary groups](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups##a-namebkmkboundarygroupsa-boundary-groups).
 - Every type of content that is held in the cache of a Configuration Manager client can be served to other clients by using Peer Cache.
 -	Peer Cache does not replace the use of other solutions like BranchCache but instead works side-by-side with it to give you more options for extending traditional content deployment solutions such as distribution points. This is a custom solution with no reliance on BranchCache, so if you don’t enable or use Windows BranchCache, it still works.

### Operations

After you deploy client settings that enable Peer Cache to a collection, members of that collection can act as a peer content source for other clients in the same boundary group:
 -	A client that operates as a peer content source submits a list of available cached content to its management point.
 -	Then, when the next client in that boundary group requests that content, each peer cache source which has the content is returned as a potential content source along with the distribution points and other content source locations in that boundary group.
 -	Per the normal operating process, the client that's seeking the content selects one content source from the pool of sources it has provided, and then proceeds to attempt to get the content.

> [!NOTE]
> If fallback to a neighbor boundary group for content occurs, the Peer Cache content source locations from the neighbor boundary group are not added to the client's pool of potential content source locations.  


Though you can make all clients participate as a peer cache source, it's a best practice to choose only clients that are best suited for being peer cache sources.  The suitability of clients can be evaluated based on a client’s chassis type, disk space, network connectivity, and more. For more information that can help you select the best clients to use for Peer Cache, see [this blog by a Microsoft consultant](https://blogs.technet.microsoft.com/setprice/2016/06/29/pe-peer-cache-custom-reporting-examples/).

**Limited access to a peer cache source**  
Beginning with version 1702, a peer cache source computer will reject a request for content when the peer cache source computer meets any of the following conditions:  
  -  Is in low battery mode.
  -  CPU load exceeds 80% at the time the content is requested.
  -  Disk I/O has an *AvgDiskQueueLength* that exceeds 10.
  -  There are no more available connections to the computer.   

You can configure these settings using the client configuration server WMI class for the peer source feature (*SMS_WinPEPeerCacheConfig*) when you use the System Center Configuration Manager SDK.

When the computer rejects a request for the content, the requesting computer will continue to seek content from alternate sources in its pool of available content source locations.   



### Monitoring   
To help you understand the use of Peer Cache, you can view the Client Data Sources dashboard. See [Client Data Sources dashboard](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).

Beginning with version 1702, you can use three reports to view peer cache use. In the console, go to **Monitoring** > **Reporting** > **Reports**. The reports all have a type of **Software Distribution Content**:
1.  **Peer cache source content rejection**:  
Use this report to understand how often the peer cache sources in a boundary group rejected a content request.
 - **Known issue:** When drilling down on results like *MaxCPULoad* or *MaxDiskIO*, you might receive an error that suggests the report or details cannot be found. To work around this, use the following two reports which show the results directly.

2. **Peer cache source content rejection by condition**:  
Use this report to understand rejection details for a specified boundary group or rejection type. You can specify

  - **Known issue:** You cannot select from available parameters and instead must enter them manually. Enter the values for *Boundary Group Name* and *Rejection Type* as seen in the first report. For example, for *Rejection Type* you might enter *MaxCPULoad* or *MaxDiskIO*.

3. **Peer cache source content rejection details**:   
  Use this report to understand the content that was being requested when it was rejected.

 - **Known issue:** You cannot select from available parameters and instead must enter them manually. Enter the value for *Rejection Type* as displayed in the first report (Peer cache source content rejection), and then enter the *Resource ID* for the content source that you want more information about.  To find the Resource ID of the content source:  

    1. Find the computer name which displays as the *Peer cache source* in the results of the 2nd report (Peer cache source content rejection by condition).  
    2. Next, go to **Assets and Compliance** > **Devices** and then search for that computers name. Use the value from the Resource ID column.  


## Requirements and considerations for Peer Cache
-   Peer Cache is supported on any Windows OS that is supported as Configuration Manager client. Non-Windows operating systems are not supported for Peer Cache.

-   Clients can only transfer content from Peer Cache clients that are in their current boundary group.

-   Prior to version 1706, each site where clients use Peer Cache must be configured with a [Network Access Account](/sccm/core/plan-design/hierarchy/manage-accounts-to-access-content#a-namebkmknaaa-network-access-account). Beginning with version 1706, that account is no longer required with one exception.  The exception is when a client uses peer cache to get and run a task sequence from the Software Center, and that task sequence reboots the client into WinPE.  In this scenario, the client still requires the Network Access Account when it is in WinPE so that it can access the peer cache source to get content.

    When it's required, the Network Access Account is used by the Peer Cache source computer to authenticate download requests from peers, and requires only domain user permissions for this purpose.

- 	Because the current boundary of a Peer Cache content source is determined by that client's last hardware inventory submission, a client that roams to a network location and is in a different boundary group might still be considered a member of its former boundary group for the purposes of Peer Cache. This can result in a client being offered a Peer Cache content source that is not in its immediate network location. We recommend excluding clients that are prone to this configuration from participating as a Peer Cache source.

## To configure Client Peer Cache client settings
1.	In the Configuration Manager console, go to **Administration** > **Client Settings**, and then open the device client settings object that you want to use. You can also modify the Default Client Settings object.
2.	From the list of available settings, choose **Client Cache Settings**.
3.	Set **Enable Configuration Manager client in full OS to share content** to **Yes**.
4.	Configure the following settings to define the ports you want to use for Peer Cache:  
  -  **Port for initial network broadcast**
  -  **Enable HTTPS for client peer communication**
  -  **Port for content download from peer (HTTP/HTTPS)**

On each computer that's enabled for Peer Cache, if the Windows Firewall is in use, Configuration Manager configures it to allow use of the ports that you configure.
