---
# required metadata

title: 
description: 
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/13/2023
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: scottduf
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom:
ms.collection:
- tier1
- M365-identity-device-management
---

# Intune grouping, targeting, and filtering: recommendations for best performance

BLOG: https://techcommunity.microsoft.com/t5/intune-customer-success/intune-grouping-targeting-and-filtering-recommendations-for-best/ba-p/2983058

This post provides concise recommendations and considerations for Intune grouping, targeting, and filtering. My goal is to help you make key architecture and design decisions in your own Intune deployments and inform you about the limitations and trade-offs of different grouping and targeting approaches. Consider these performance recommendations as just one factor along with others that are specific to your own environment (for example, manageability and simplicity).

In this article:

- A brief overview of Intune grouping and targeting concepts
- Key recommendations for best performance

## Overview of Intune grouping and targeting concepts

Before getting into the recommendations, it’s worthwhile to briefly review the grouping, targeting, and filtering units available in Intune today. 

### Azure Active Directory groups

Intune almost exclusively uses Azure Active Directory (Azure AD) groups for grouping and targeting. When you select **Groups** in the Microsoft Intune admin center, you're looking at the Azure AD groups page.

Azure AD groups are important to Intune admins. They are:

- The objects used for assigning apps, policies, and other workloads to users and devices.
- Used for other purposes where you define which devices certain admins are allowed to view in the Intune admin center, such as Scope groups in role-based administration (RBAC).

IMAGE

### Virtual groups

The **All users** and **All devices** assignments are known as Intune “virtual” groups. These virtual groups are convenient. They exist by default in all Intune tenants and don’t come with any management overhead (you don’t need to create or adjust any Azure AD rules to keep them populated with members). They're also highly scalable and optimized, mainly because they don't need to be synced from Azure AD in the same way that groups do.

### Filters

You can use [filters](filters.md) to narrow the assignment scope of apps and policies (and other workloads) to specific devices, after the app or policy is assigned to one of the other mentioned group types. With filters, you can target user or device groups. Then, filter devices in or out of that assignment based on device properties. Filtering is high performance, low latency applicability evaluation at device check-in without any need to pre-compute.

IMAGE

## Performance recommendations

This section includes some general recommendations that can improve performance when working with assignments in Microsoft Intune.

These recommendations are general, and focus on improving performance & reducing latency in workload assignment. They have the most impact when working in large Intune environments (10k devices+). Recommendations should be considered alongside other design aspects such as manageability, ease of use, role-based administration, and simplicity.

### Use virtual groups

| DO | DON'T |
| --- | --- |
| ✔️ Use the **All users** and **All devices** virtual groups where possible.<br/><br/>✔️ Use filters to achieve granular device applicability. | ❌ Don’t create your own “All users” or “All devices” groups for use in Intune targeting or RBAC. |

If you assign Intune workloads to large Azure AD groups that have many users or devices, then it can cause large synchronization backlogs in your Intune tenant. This backlog impacts policy and app deployments, which will take longer to reach managed devices.

The **All users** and **All devices** groups are an Intune-only grouping construct. This means there is no ongoing sync between Azure AD and Intune. Similarly, filters are an Intune construct that allow devices to be evaluated for applicability dynamically during an Intune check-in. Using several large groups, like “All windows devices” and “all iOS devices”, rather than the virtual groups with filters can create sync bottlenecks, blocking the sync of smaller groups until the large groups are fully synced.

Every time you use a new group (one that has never been used before in an Intune assignment), in addition to the membership sync, there's a first-time setup process that happens. The first full sync always takes longer than subsequent incremental syncs.

### Reuse groups

| DO | DON'T |
| --- | --- |
| ✔️ Re-use the same group objects for assigning  multiple policies. | ❌ Don’t create duplicate copies of the same group to target different policies. <br/><br/> ❌ Don’t create dedicated “App groups” or “Policy groups”. |

Behind the scenes, Intune converts Azure AD group members to assignment targeting messages for each user and device. This process is highly optimized when the group objects are the same. For example, Intune grouping and targeting works best when the “Engineering” user group is targeted with 10 policies, rather than the Engineering users being used as members of 10 different groups, each assigned to a different policy.

We’ve seen a few designs countering this guidance. For example, where IT admins create a group called “Install_Edge” and then another group called “Deploy_Edge_Config_Policy” and put the same devices in each group.

A similar and not recommended pattern is creating “App groups”, where each app has several Azure AD groups created for it and then adding members directly to those groups. For example, to manage the Edge application, the administrator creates three groups:

- Edge_Required
- Edge_Available
- Edge_Uninstall

The administrator then adds individual user or device objects into those groups, typically by custom tooling or the Graph API.

We don’t recommend this approach. It dramatically increases the number of Azure AD groups that Intune must subscribe to and monitor for membership updates, which is less efficient. Inefficient group sync design can impact the speed at which new assignments can be created and delivered to devices.

### Make incremental group changes

| DO | DON'T |
| --- | --- |
| ✔️ Make incremental changes to build out nested groups.| ❌ Don’t make big group nesting changes all at once. |

A large group membership change in Azure AD can generate bursts of targeting changes in Intune and slow down targeting of other assignments in your environment.

For example, you have the following group structure:

- Parent group (0 devices) – Not assigned
- Child group 1 (30k devices) – Not assigned
- Child group 2 (60k devices) – Not assigned
- Child group 3 (90k devices) – Not assigned

Rather than targeting the parent group (and its child groups) in a policy deployment (impacting 180k devices all at once), we recommend that you start with an empty parent group that has no nested children. Then gradually, over the course of days, add child groups 1-3. At a rate of 30k devices a day, this targeting will be applied to all devices over 6 days. This recommendation doesn’t mean you need to further break-up child groups 2 and 3 to enforce a 30k maximum per day. The example is just to highlight a conservative rate of processing new groups through the grouping and targeting system.

This recommendation also applies when groups are “un-nested”.

### Use filters to include and exclude

| DO | DON'T |
| --- | --- |
| ✔️ Use filters to achieve the right user+device combination for targeting. | ❌ Don’t mix user groups and device groups when using Include and Exclude groups. |

This recommendation is also a support statement. We don't recommend or support creating assignments to user groups and excluding a device group from that assignment, or vice-versa. This recommendation exists due to the timing/latency characteristic of dynamic groups and the fact that **Excluded groups** membership is not instant, which can result in cases where devices incorrectly receive app or policy assignments. To understand more, go to [Assign policies and profiles - support matrix](../configuration/device-profile-assign#support-matrix.md).

Instead of mixed exclusions, we recommend assigning to a user group. Then, use filters to dynamically include or exclude the appropriate devices.

## Summary

When creating and managing assignments in Intune, incorporate some of these recommendations. Take advantage of virtual groups and filters to help refine the scope of your Azure AD groups, and keep these best practices in mind:

- Use Intune virtual groups that don’t require Azure AD syncing.
- Re-use groups to optimize your targeting.
- Make incremental group changes for more efficient processing.
- Use filters, instead of groups, to dynamically include and exclude.
