---
title: Client Peer Cache
titleSuffix: Configuration Manager
description: Use Peer Cache for client content source locations when deploying content with System Center Configuration Manager.
ms.custom: na
ms.date: 04/10/2018
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
caps.latest.revision: 3
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Peer Cache for Configuration Manager clients

*Applies to: System Center Configuration Manager (Current Branch)*

<!--1101436-->
Use **Peer Cache** to help manage deployment of content to clients in remote locations. Peer Cache is a built-in Configuration Manager solution that enables clients to share content with other clients directly from their local cache.   

> [!TIP]  
> This feature was first introduced in version 1610 as a [pre-release feature](/sccm/core/servers/manage/pre-release-features). Beginning with version 1710, this feature is no longer a pre-release feature.  


> [!Note]  
> Configuration Manager doesn't enable this optional feature by default. You must enable this feature before using it. For more information, see [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


## Overview
A Peer Cache client is a Configuration Manager client that is enabled to use Peer Cache. A Peer Cache client that has content it can share with additional clients is a Peer Cache source.
 - 	You use client settings to enable clients to use Peer Cache.
 - 	To share content as a Peer Cache source, a Peer Cache client:
    -  Must be domain joined. However, a client that is not domain joined can get content from a domain joined Peer Cache source.
    -  Must be a member of the current boundary group of the client that's seeking the content. When a client uses fallback to seek content from a neighbor boundary group, the list of content source locations does not include a Peer Cache client in a neighbor boundary group. For more information about current and neighbor boundary groups, see [Boundary groups](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups##a-namebkmkboundarygroupsa-boundary-groups).
 - The Configuration Manager client serves every type of content in the cache to other clients by using Peer Cache. This content includes Office 365 files and expresses installation files.<!--SMS.500850-->
 -	Peer Cache does not replace the use of other solutions like BranchCache. Peer Cache works along with other solutions to give you more options for extending traditional content deployment solutions such as distribution points. Peer Cache is a custom solution with no reliance on BranchCache. If you don’t enable or use Windows BranchCache, Peer Cache still works.

### Operations

To enable peer cache, deploy the client settings to a collection. Then members of that collection act as a peer content source for other clients in the same boundary group.
 -	A client that operates as a peer content source submits a list of available cached content to its management point.
 -	When the next client in that boundary group requests that content, each peer cache source, which has the content and is online, is returned in the list of potential content sources. This list also includes  the distribution points and other content source locations in that boundary group.
 -	Per the normal process, the client that is seeking the content selects one source from the provided list. The client then attempts to get the content.

> [!NOTE]
> If the client falls back to a neighbor boundary group for content, it does not add the Peer Cache content source locations from the neighbor boundary group to the list of potential content source locations.  


The best practice is to choose only clients best suited as peer cache sources. Evaluate client suitability based on attributes such as chassis type, disk space, and network connectivity. For more information that can help you select the best clients to use for Peer Cache, see [this blog by a Microsoft consultant](https://blogs.technet.microsoft.com/setprice/2016/06/29/pe-peer-cache-custom-reporting-examples/).

**Limited access to a peer cache source**  
Beginning with version 1702, a peer cache source computer rejects requests for content when the peer cache source computer meets any of the following conditions:  
  -  Is in low battery mode.
  -  CPU load exceeds 80% at the time the content is requested.
  -  Disk I/O has an *AvgDiskQueueLength* that exceeds 10.
  -  There are no more available connections to the computer.   

Configure these settings using the client configuration server WMI class for the peer source feature (*SMS_WinPEPeerCacheConfig*) in the Configuration Manager SDK.

When the computer rejects a request for the content, the requesting computer continues to seek content from the list of available content source locations.   



### Monitoring   
To help you understand the use of Peer Cache, you can view the Client Data Sources dashboard. See [Client Data Sources dashboard](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).

Beginning with version 1702, you can use three reports to view peer cache use. In the console, go to **Monitoring** > **Reporting** > **Reports**. The reports all have a type of **Software Distribution Content**:
1.  **Peer cache source content rejection**:  
Use this report to understand how often the peer cache sources in a boundary group reject a content request.
 - **Known issue:** When drilling down on results like *MaxCPULoad* or *MaxDiskIO*, you might receive an error that suggests the report or details cannot be found. To work around this issue, use the following two reports that directly show the results.

2. **Peer cache source content rejection by condition**:  
Use this report to understand rejection details for a specified boundary group or rejection type. You can specify

  - **Known issue:** You cannot select from available parameters and instead must enter them manually. Enter the values for *Boundary Group Name* and *Rejection Type* as seen in the first report. For example, for *Rejection Type* you might enter *MaxCPULoad* or *MaxDiskIO*.

3. **Peer cache source content rejection details**:   
  Use this report to understand the content that the client was requesting when rejected.

 - **Known issue:** You cannot select from available parameters and instead must enter them manually. Enter the value for *Rejection Type* as displayed in the **Peer cache source content rejection** report. Then enter the *Resource ID* for the content source about which you want more information. To find the Resource ID of the content source:  

    1. Find the computer name that displays as the *Peer cache source* in the results of the **Peer cache source content rejection by condition** report.  
    2. Next, go to **Assets and Compliance** > **Devices** and then search for that computers name. Use the value from the Resource ID column.  


## Requirements and considerations for Peer Cache
-   Peer Cache is supported on any Windows OS that is supported as Configuration Manager client. Non-Windows operating systems are not supported for Peer Cache.

-   Clients can only transfer content from Peer Cache clients that are in their current boundary group.

-   Prior to version 1706, each site where clients use Peer Cache must be configured with a [Network Access Account](/sccm/core/plan-design/hierarchy/manage-accounts-to-access-content#a-namebkmknaaa-network-access-account). Beginning with version 1706, that account is no longer required with one exception. The exception scenario is when a peer cache-enabled client runs a task sequence from the Software Center, and that task sequence reboots to a boot image. In this scenario, the client still requires the Network Access Account. When the client is in Windows PE, it uses the Network Access Account to get content from the peer cache source.

    When required, the Peer Cache source computer uses the Network Access Account to authenticate download requests from peers. This account requires only domain user permissions for this purpose.

- 	The client's last hardware inventory submission determines the current boundary of a Peer Cache content source. A client that roams to a different boundary group might still be a member of its former boundary group for the purposes of Peer Cache. This behavior results in a client being offered a Peer Cache content source that is not in its immediate network location. We recommend excluding clients that are prone to this configuration from participating as a Peer Cache source.
-    Beginning with version 1706, the peer cache client first validates that the peer cache content source is online before attempting to download content. <!--sms.498675-->

## To configure Client Peer Cache client settings
For information about configuring the client settings, see [Client cache settings](/sccm/core/clients/deploy/about-client-settings#client-cache-settings). For more information, see [How to configure client settings](/sccm/core/clients/deploy/configure-client-settings).

On peer cache-enabled clients that uses the Windows Firewall, Configuration Manager configures the firewall ports that you specify in client settings.
