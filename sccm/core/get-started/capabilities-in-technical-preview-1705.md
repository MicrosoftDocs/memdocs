---
title: "Technical Preview 1705 | Microsoft Docs"
description: "Learn about features available in the Technical Preview vresion 1705 for System Center Configuration Manager."
ms.custom: na
ms.date: 05/19/2017
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 00684289-d21a-45f8-b1e3-c5c787d73096
author: Brenduns
ms.author: brenduns
manager: angrobe
---
# Capabilities in Technical Preview 1705 for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*

This article introduces the features that are available in the Technical Preview for System Center Configuration Manager, version 1705. You can install this version to update and add new capabilities to your Configuration Manager technical preview site. Before installing this version of the technical preview, review the introductory topic, [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md), to become familiar with general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.    

<!--  Known Issues Template
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**The following are new features you can try out with this version.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## Console display on high DPI devices
With this release, issues with how the Configuration Manager console scales and displays different parts of the UI when viewed on high DPI devices (like a Surface book) should be fixed.


## Peer Cache improvements
Beginning with this technical preview, Peer Cache [no longer uses the Network Access Account](/sccm/core/plan-design/hierarchy/client-peer-cache) to authenticate download requests from peers.


## Improved boundary groups for software update points
This release includes improvements for how software update points work with boundary groups. The following summarizes the new fallback behavior:
-   Fallback for software update points now uses a configurable time for fallback to neighbor boundary groups, with a minimum time of 120 minutes.

-   Independent of the fallback configuration, a client attempts to reach the last software update point it used for 120 minutes. After failing to reach that server for 120 minutes, the client then checks its pool of available software update points, so it can find a new one.

  -   All software update points in the clients current boundary group are added to the clients pool immediately.

  -   Because a client tries to use its original server for 120 minutes before seeking a new one, no additional servers are contacted until after two hours have elapsed.

  -   If fallback to a neighbor group is configured for the minimum of 120 minutes, software update points from that neighbor boundary group will be part of the client's pool of available servers.

-   After failing to reach its original server for two hours, the client switches to a five-minute cycle for contacting a new software update point.

    This means if a client fails to connect with a new server, after five minutes it selects the next server from its pool of available servers and attempts to contact that one.

  -   This cycle continues until the client connects to a software update point it can use.
  -   Until the client finds a software update point, additional servers are added to pool of available servers when the fallback time for each neighbor boundary group is met.

For more information, see [software update points](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points) in the Boundary Groups topic for the Current Branch.
