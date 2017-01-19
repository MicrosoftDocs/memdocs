---
title: "Capabilities in Technical Preview 1701 for System Center Configuration Manager | Microsoft Docs"
description: "Learn about features available in the Technical Preview for System Center Configuration Manager, version 1701."
ms.custom: na
ms.date: 1/20/2017
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 18598eaa-1131-44ff-8f8b-6093e87ac7a1
caps.latest.revision: 5
author: Brendunsms.author: brendunsmanager: angrobe
---
# Capabilities in Technical Preview 1701 for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*



This article introduces the features that are available in the Technical Preview for System Center Configuration Manager, version 1701. You can install this version to update and add new capabilities to your Configuration Manager technical preview site. Before installing this version of the technical preview, review the introductory topic, [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md), to become familiar with general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.    


**The following are new features you can try out with this version.**  

## Boundary groups improvements for software update points
Beginning with this preview, you now use boundary groups to associate clients with software update points. This is part of continuing work to expand the changes for boundary groups to manage additional site system roles.  Changes for boundary groups was first introduced in Technical Preview 1609 and the Current Branch in version 1610.  

With this preview, you use the new boundary group behavior to manage which software update points a client can use, similar to how you manage which distribution point a client can use:  

- You configure boundary groups to associate one or more servers that host a software update point.
- Clients that are seeking a new software update point will try to use one that is associated with their current boundary group.
- When the client fails to reach their current software update point and cannot find one from their current boundary group, the client uses Fallback behavior to expand the available pool of software update points it can use.    

For more information on boundary groups, see [Boundary groups](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#BKMK_BoundaryGroups) in the content for the Current Branch.

However, with this preview, boundary groups for software update points are only partially implemented. You can add software update points and configure neighbor boundary groups that contain software update points, but the fallback time for software update points is not yet supported, and clients will wait two hours before starting fallback.

The following describes the behavior for software update points with this technical preview:  

-	**New clients use boundary groups to select software update points,**
A client that you install after you install version 1701 selects a software update point from those associated with the client’s boundary group.

  This replaces the previous behavior where clients select a software update point randomly from a list of those that share the clients forest.   

-	**Previously installed clients continue to use their current software update point until they fallback to find a new one.**
Clients that were previously installed and that already have a software update point will continue to use that software update point until they fallback. This includes software update points that are not associated with the client’s current boundary group. They do not immediately attempt to find and use a software update point from their current boundary group.

  A client that already has a software update point begins to use this new boundary group behavior only after the client fails to reach its current software update point and starts fallback.
This delay in switching over to the new behavior is intentional. This is because a change of software update point can result in a large use of network bandwidth as the client synchronizes data with the new software update point. The delay in transition can help to avoid saturating your network should all your clients switch to new software update points at the same time.

-	**Configurations for fallback time:**
Configurations for when clients start fallback to search for a new software update point are not supported in this technical preview. This includes configurations for **Fallback times (in minutes)** and **Never fallback**, that you might configure for different boundary group relationships.

  Instead, clients retain their current behavior where a client attempts to connect to its current software update point for two hours before it starts fallback, to find a new software update point it can use.

  When a client does use fallback, it will use the boundary group configurations for fallback to create a pool of available software update points. This pool includes all software update points from the clients *current boundary group*, *neighbor boundary groups*, and the clients *site default boundary group*.

- **Configure the default site boundary group:**  
 Consider adding a software update point to the *Default-Site-Boundary-Group&lt;sitecode>*. This ensures that clients that are not members of another boundary group can fallback to find a software update point.


To manage software update points for boundary groups, use the [procedures from the Current Branch documentation](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#procedures-for-boundary-groups), but remember that fallback times you might configure are not yet used for software update points.

## Host software updates on cloud-based distribution points
Beginning with this preview version, you can use a cloud-based distribution point to host a software update package. However, because you can configure clients to download software updates directly from Microsoft Update, consider the additional costs that deploying a software update package to a cloud-based distribution point can incur.

For information about using cloud-based distribution points, see [Use a cloud-based distribution point](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point) in the content for the Current Branch of Configuration Manager.
