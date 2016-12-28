---
title: "Client Peer Cache | System Center Configuration Manager"
description: "Use Peer Cache for client content source locations when deploying content with System Center Configuration Manager."
ms.custom: na
ms.date: 12/28/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
caps.latest.revision: 3
author: Brendunsms.author: brendunsmanager: angrobe
---
# Peer Cache for Configuration Manager clients*Applies to: System Center Configuration Manager (Current Branch)*
Beginning with System Center Configuration Manager version 1610, you can use **Peer Cache** to help manage deployment of content to clients in remote locations. Peer Cache is a built-in Configuration Manager solution for clients to share content with other clients directly from their local cache.   

> [!TIP]  
> With version 1610, Peer Cache and the Client Data Sources dashboard are pre-release features. To enable them, see [Use pre-release features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

 - 	You use client settings to enable clients to use Peer Cache.
 - 	To share content, Peer Cache clients must both be members of the current boundary group of the client seeking the content. Peer Cache clients in neighbor boundary groups are not included with the pool of available content source locations when a client uses fallback to seek content from a neighbor boundary group. For more information about current and neighbor boundary groups, see [Boundary groups](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups##a-namebkmkboundarygroupsa-boundary-groups).
 -  Every type of content that is held in the cache of a Configuration Manager client can be served to other clients using Peer Cache.
 -	Peer Cache does not replace the use of other solutions like BranchCache but instead works side-by-side to give you more options to extend traditional content deployment solutions like distribution points. As a custom solution with no reliance on BranchCache, if you don’t enable or use Windows BranchCache, this solution still works.

After you deploy client settings that enable Peer Cache to a collection, members of that collection can act as a peer content source for other clients in the same boundary group:
 -	A client that operates as a peer content source will submit a list of available content it has cached to its management point.
 -	Then, when the next client in that boundary group requests that content, each peer cache source which has the content is returned as a potential content source along with the distribution points and other content source locations in that boundary group.
 -	Per the normal operating process, the client seeking the content selects one content source from the pool of sources it is provided, and proceeds to attempt to get the content.

> [!NOTE]
> If fallback to a neighbor boundary group for content occurs, the Peer Cache content source locations from the neighbor boundary group are  not added to the client's pool of potential content source locations.  

Even though you could make all clients participate in Peer Cache, it is best practice to choose only clients that are best suited for being peer cache sources.  Suitability of clients can be evaluated based on a client’s chassis type, disk space, network connectivity, and more. For more information that can help you select the best clients to use for Peer Cache, see [this blog by a Microsoft Consultant](https://blogs.technet.microsoft.com/setprice/2016/06/29/pe-peer-cache-custom-reporting-examples/).

To help you understand the use of Peer Cache, you can view the Client Data Sources dashboard. See [Client Data Sources dashboard](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).


## Requirements and considerations for Peer Cache:
- You must configure your site with a **Network Access Account** that has **Full Control** to the cache folder on each client. By default, this is ***%windir%\ccmcache***.

- Clients can only transfer content from Peer Cache clients that are in their current boundary group.

- 	Because the current boundary of a Peer Cache content source is determined by that clients last hardware inventory submission, a client that roams to a network location that is in a different boundary group might still be considered a member of its former boundary group for the purpose of Peer Cache. This can result in a client being offered a Peer Cache content source that is not in its immediate network location. We recommend excluding clients that are prone to this configuration from participating as a Peer Cache source.

## To configure Client Peer Cache client settings
1.	In the Configuration Manager console, go to **Administration** > **Client Settings**, and then open device client settings object you want to use. You can also modify the Default Client Settings object.
2.	From the list of available settings, select **Client Cache Settings**.
3.	Set **Enable Configuration Manager client in full OS to share content** to **Yes**.
4.	Configure the following settings to define the ports you want to use for Peer Cache:  
  -  **Port for initial network broadcast**
  -  **Enable HTTPS for client peer communication**
  -  **Port for content download from peer (HTTP/HTTPS)**

On each computer enabled for Peer Cache, if the Windows Firewall is in use, Configuration Manager configures it to allow use of the ports you configure.
