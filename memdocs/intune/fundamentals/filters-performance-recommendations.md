---
# required metadata

title: Performance recommendations for Grouping, Targeting and Fitering in Microsoft Intune
description: When using filters in Microsoft Intune, use Intune virtual groups that don’t require Azure AD syncing, reuse groups to optimize your targeting, make incremental group changes for efficient processing, and use filters to dynamically include and exclude. These recommendations improve performance.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/16/2023
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

# Performance recommendations for Grouping, Targeting and Fitering in large Microsoft Intune environments

This article lists and describes recommendations for Intune grouping, targeting, and filtering for your policies and applications. The goal is to help you make architecture and design decisions for your Intune deployments in large environments.

These performance recommendations and their implementation can be different and depend on your own environment & other factors, including manageability and simplicity.

In this article:

- Get an overview of Intune grouping and targeting concepts
- Get some performance recommendations

For more information and an overview of filters, go to [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](filters.md).

## Overview of Intune grouping and targeting concepts

Before getting into the recommendations, let's review the grouping, targeting, and filtering features available in Intune.

### Azure Active Directory groups

Intune almost exclusively uses Azure Active Directory (Azure AD) groups for grouping and targeting. When you select **Groups** in the Microsoft Intune admin center, you're looking at Azure AD groups.

:::image type="content" source="./media/filters-performance-recommendations/admin-center-all-groups.png" alt-text="Screenshot that shows the Intune admin center, groups, and all groups in Microsoft Intune." lightbox="./media/filters-performance-recommendations/admin-center-all-groups.png":::


Azure AD groups are an important part of Intune because these groups are:

- The objects used for assigning apps, policies, and other workloads to users and devices.
- Used to define the devices that admins can view and manage in the Intune admin center, like Scope groups in role-based access control (RBAC).

### Virtual groups

The **All users** and **All devices** assignments are Intune “virtual” groups. These virtual groups are available by default in all Intune tenants and don’t come with any management overhead. For example, you don’t need to create or adjust any Azure AD rules to keep their members populated.

The **All users** and **All devices** groups are also highly scalable and optimized, mainly because they don't need to be synced from Azure AD in the same way that other groups do.

### Filters

After the app or policy is assigned to a non-virtual group, you can use [filters](filters.md) to narrow the assignment scope of these apps and policies to specific user or device groups.

Your filter filters devices in (or out) of that assignment based on device properties. 

:::image type="content" source="./media/filters-performance-recommendations/filters-azuread-virtual-groups.png" alt-text="Screenshot that shows the Intune admin center, the Azure AD groups, virtual groups, and some filter properties in Microsoft Intune."lightbox="./media/filters-performance-recommendations/filters-azuread-virtual-groups.png":::

Filtering is high performance, low latency applicability evaluation at device check-in without any need to precompute.

## Performance recommendations

This section includes some recommendations that can improve performance when assigning your policies in Microsoft Intune.

These recommendations focus on improving performance and reducing latency in workload assignment. They have the most impact when working in large Intune environments, like environments with >100,000 devices. These recommendations should be considered with other design aspects, like manageability, ease of use, role-based administration, and simplicity.

### Use virtual groups

| DO | DON'T |
| --- | --- |
| ✔️ Use the **All users** and **All devices** virtual groups where possible.<br/><br/>✔️ Use filters for granular device policy assignment. | ❌ Don’t create your own “All users” or “All devices” groups for in policy targeting or RBAC. |

If you assign Intune workloads to large Azure AD groups that have many users or devices, then synchronization backlogs can happen in your Intune environment. This backlog impacts policy and app deployments, which take longer to reach managed devices.

The built-in **All users** and **All devices** groups are Intune-only grouping objects that do not exist in Azure AD. There isn't a continuous sync between Azure AD and Intune. Similarly, filters are Intune-only design rules that evaluate devices for policy assignment dynamically during a check-in with the Intune service.

> [!NOTE]
> For information on Intune check-in policy refresh intervals, go to [Intune Policy refresh intervals](../configuration/device-profile-troubleshoot.md#policy-refresh-intervals).

When you use several large groups, like “All windows devices” and “all iOS devices”, instead of the virtual groups with filters, then it can:

- Create sync bottlenecks
- Block the sync of smaller groups until the large groups are fully synced

Every time you use a new group (a group that's never been used in an Intune assignment) with a new membership sync, there's a first time setup process that happens. The first full sync always takes longer than subsequent incremental syncs.

### Reuse groups

| DO | DON'T |
| --- | --- |
| ✔️ Reuse the same group objects for assigning multiple policies. | ❌ Don’t create duplicate copies of the same group to target different policies. <br/><br/> ❌ Don’t create dedicated “App groups” or “Policy groups”. |

Behind the scenes, Intune converts Azure AD group members to assignment targeting messages for each user and device. This process is highly optimized when the group objects are the same.

For example, Intune grouping and targeting works best when the “Engineering” user group is targeted with 10 policies. It doesn't work best when the Engineering users are members of 10 different groups, each assigned to a different policy.

We’ve seen a few designs countering this guidance. For example, IT admins create an “Install_Edge” group, create a “Deploy_Edge_Config_Policy” group, and then put the same devices in each group.

A similar and not recommended pattern is creating “App groups”. An app group is when each app has several Azure AD groups created for it. For example, to manage the Edge application, an admin creates the following groups:

- Edge_Required
- Edge_Available
- Edge_Uninstall

The admin adds individual user or devices into these groups. These app groups dramatically increase the number of Azure AD groups that Intune must subscribe to and monitor for membership updates, which is less efficient. Inefficient group sync design impacts how fast new assignments are created and delivered to devices.

### Make incremental group changes

| DO | DON'T |
| --- | --- |
| ✔️ Make incremental changes to build out nested groups.| ❌ Don’t make large group nesting changes all at once. |

A large group membership change in Azure AD can generate bursts of targeting changes in Intune. These bursts can delay targeting of other assignments in your environment.

For example, you have the following group structure:

- Parent group (0 devices) – Not assigned
- Child group 1 (30,000 devices) – Not assigned
- Child group 2 (60,000 devices) – Not assigned
- Child group 3 (90,000 devices) – Not assigned

Don't target the parent group and its child groups in a policy deployment that impacts 180,000 devices all at once. Instead, we recommend you start with an empty parent group that has no nested children. Then gradually, over the course of days, add child groups 1-3. At 30,000 devices a day, this targeting applies to all devices over six days.

This recommendation doesn’t mean you need to break-up child groups 2 and 3 to enforce a 30,000 maximum per day. The example just highlights a gradual rate of processing new groups through the grouping and targeting system.

This recommendation also applies when groups are “unnested”. For more information on nested groups, go to [Manage Azure AD groups and group membership](/azure/active-directory/fundamentals/how-to-manage-groups).

### Use filters to include and exclude

| DO | DON'T |
| --- | --- |
| ✔️ Use filters to achieve the correct user+device combination for targeting. | ❌ Don’t mix user groups and device groups when using Include and Exclude groups. |

This recommendation is also a support statement. We don't recommend or support creating assignments to user groups and excluding a device group from that assignment, or vice-versa.

This recommendation exists due to the timing/latency characteristic of dynamic groups. And, **Excluded groups** membership isn't instant, which can result in cases where devices incorrectly receive app or policy assignments. To understand more, go to the [Assign policies and profiles - support matrix](../configuration/device-profile-assign.md#support-matrix).

Instead of mixed exclusions, we recommend assigning to a user group. Then, use filters to dynamically include or exclude the appropriate devices.

## Summary

When creating and managing assignments in Intune, incorporate some of these recommendations. Use groups or virtual groups and apply filters to help refine the targeting scope, and keep the best practices in mind:

- Use Intune virtual groups, instead of building your own in AAD becauese they don’t require Azure AD syncing.
- Reuse groups to optimize your targeting.
- Make incremental group changes for more efficient processing, particularly when targeting a very large group for the first time.
- Use filters to dynamically include and exclude devices, on top of group or virtual group assignments.

## Next steps

- [Use filters when assigning your apps, policies, and profiles](filters.md)
- [Supported device properties when creating filters](filters-device-properties.md)
- [Supported workloads when creating filters](filters-supported-workloads.md)
- [Filter reports and troubleshooting](filters-reports-troubleshoot.md)
