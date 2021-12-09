---
title: Boundary groups and software update points
titleSuffix: Configuration Manager
description: Understand how clients and software update points behave with boundary groups.
ms.date: 08/02/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# Boundary groups and software update points

*Applies to: Configuration Manager (current branch)*

Clients use boundary groups to find a new software update point. To control which servers a client can find, add individual software update points to different boundary groups.

If you add all existing software update points to the default site boundary group, the client selects a software update point from the pool of available servers. This behavior is similar to earlier versions of Configuration Manager current branch. For controlled selection and fallback behavior, add individual software update points to different boundary groups.

If you install a new site, software update points aren't added to the default site boundary group. Assign software update points to a boundary group so that clients can find and use them.

## Fallback

Configure software update point fallback like other site system roles, but with the following caveats.

### New clients use boundary groups to select software update points

When you install new clients, they select a software update point from those servers associated with the boundary groups you configure. This behavior replaces the previous behavior where clients select a software update point randomly from a list of the servers that share the client's forest.

### Clients continue to use a last known-good software update point until they fall back to find a new one

Clients that already have a software update point continue to use it until it can't be reached. This behavior includes continued use of a software update point that isn't associated with the client's current boundary group.

This behavior is intentional. The client continues to use an existing software update point, even when it isn't in the client's current boundary group. When the software update point changes, the client synchronizes data with the new server, which causes significant network usage. If all clients switch to a new server at the same time, the delay in transition helps to avoid saturating your network.

### A client always tries to reach its last known-good software update point for 120 minutes before starting fallback

After 120 minutes, if the client hasn't established contact, it then begins fallback. When fallback starts, the client receives a list of all software update points in its current boundary group. Other software update points in neighbor and site default boundary groups are available based on fallback configurations.

## Fallback configurations

You can configure **Fallback times (in minutes)** for software update points to be less than 120 minutes. However, the client still tries to reach its original software update point for 120 minutes. Then it expands its search to other servers. Boundary group fallback times start when the client first fails to reach its original server. When the client expands its search, the site provides any boundary groups configured for less than 120 minutes.

To block fallback for a software update point to a neighbor boundary group, configure the setting to **Never fallback**.

After failing to reach its original server for two hours, the client then uses a shorter cycle to establish a connection to a new software update point. This behavior enables the client to rapidly search through the expanding list of potential software update points.

### Example

You configure software update points in boundary group *A* to fall back after **10** minutes. You configure the same setting for boundary group *B* to **130** minutes. A client in boundary group *Z* fails to reach its last known-good software update point.

- For the next 120 minutes, the client tries to reach only its original server in boundary group Z. After 10 minutes, Configuration Manager adds the software update points from boundary group A to the pool of available servers. However, the client doesn't try to contact them or any other server until the initial 120-minute period elapses.

- After trying to contact the original software update point for 120 minutes, the client expands its search. It adds servers to the available pool of software update points that are in it's current and any neighbor boundary groups configured for 120 minutes or less. This pool includes the servers in boundary group A, which were previously added to the pool of available servers.

- After 10 more minutes, the client expands the search to include software update points from boundary group B. This period is 130 minutes of total time after the client first failed to reach its last known-good software update point.

## Manually switch to a new software update point

Along with fallback, use client notification to manually force a device to switch to a new software update point.

When you switch to a new server, the devices use fallback to find that new server. Clients switch to the new software update point during their next software updates scan cycle.<!-- SCCMDocs#1537 -->

Review your boundary group configurations. Before you start this change, make sure that your software update points are in the correct boundary groups.

For more information, see [Manually switch clients to a new software update point](../../../../sum/plan-design/plan-for-software-updates.md#BKMK_ManuallySwitchSUPs).

## Intranet clients can use a CMG software update point

<!--7102873-->

Starting in version 2006, intranet clients can access a software update point via a cloud management gateway (CMG). Assign the CMG to a boundary group, and enable the software update point to [**Allow Configuration Manager cloud management gateway traffic**](../../../clients/manage/cmg/setup-cloud-management-gateway.md#bkmk_role).

This behavior is useful in the following scenarios:

- When an internet machine connects to the VPN, it will continue to scan against the CMG software update point over the internet.

- If the only software update point for the boundary group is the CMG software update point, then all intranet and internet devices will scan against it.

## Next steps

- [Boundary groups and management points](boundary-groups-management-points.md)

- [Procedures for boundary groups](boundary-group-procedures.md)
