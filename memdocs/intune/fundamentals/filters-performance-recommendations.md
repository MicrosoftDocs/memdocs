---
# required metadata

title: Performance recommendations when using filters
description: When using filters in Microsoft Intune, use Intune virtual groups that don't require Microsoft Entra ID syncing. To improve performance, reuse groups, make incremental group changes, and use filters to include and exclude.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/22/2024
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: gokarthi
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom:
ms.collection:
- tier1
- M365-identity-device-management
---

# Performance recommendations for grouping, targeting, and filtering in large Microsoft Intune environments

When you create a policy, you can use [filters](filters.md) to assign a policy based on rules you create. You can apply filters to Intune-enrolled devices and Intune-managed apps. For an overview of filters, go to [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](filters.md).

When you create filters, there are some performance recommendations you should consider.

This article lists and describes recommendations for Intune grouping, targeting, and filtering for your policies and apps. The goal is to help you make architecture and design decisions for Intune deployments in large environments.

These performance recommendations and their implementation can be different and depend on your own environment & other factors, including manageability and simplicity.

In this article:

- Get an overview of Intune grouping and targeting concepts
- Get some performance recommendations

For guidance on dynamic groups, go to [Create simpler, more efficient rules for dynamic groups in Microsoft Entra ID](/azure/active-directory/enterprise-users/groups-dynamic-rule-more-efficient).

## Overview of Intune grouping and targeting concepts

Let's review the grouping, targeting, and filtering features available in Intune.

### Microsoft Entra groups

Intune almost exclusively uses Microsoft Entra groups for grouping and targeting. When you select **Groups** in the Microsoft Intune admin center, you're looking at Microsoft Entra groups.

:::image type="content" source="./media/filters-performance-recommendations/admin-center-all-groups.png" alt-text="Screenshot that shows the Intune admin center, groups, and all groups in Microsoft Intune." lightbox="./media/filters-performance-recommendations/admin-center-all-groups.png":::

Microsoft Entra groups are an important part of Intune because these groups are:

- The objects used for assigning apps, policies, and other workloads to users and devices
- Used to define the devices that admins can view and manage in the Intune admin center, like scope groups in role-based access control (RBAC)

### Virtual groups

The **All users** and **All devices** assignments are Intune "virtual" groups. These virtual groups are available by default in all Intune tenants and don't come with any management overhead. For example, you don't need to create or adjust any Microsoft Entra ID rules to keep their members populated.

The **All users** and **All devices** groups are also highly scalable and optimized, mainly because they don't need to be synced from Microsoft Entra ID in the same way that other groups do.

### Filters

After the app or policy is assigned to a Microsoft Entra ID or virtual group, you can use [filters](filters.md) to narrow the assignment scope of these apps and policies to specific user or device groups.

Your filter filters devices in (or out) of that assignment based on device properties.

:::image type="content" source="./media/filters-performance-recommendations/filters-azuread-virtual-groups.png" alt-text="Screenshot that shows the Intune admin center, the Microsoft Entra groups, virtual groups, and some filter properties in Microsoft Intune."lightbox="./media/filters-performance-recommendations/filters-azuread-virtual-groups.png":::

Filtering is high performance, low latency applicability evaluation at device check-in without any need to precompute group membership.

## Performance recommendations

This section includes some recommendations that can improve performance when assigning your policies in Microsoft Intune.

These recommendations focus on improving performance and reducing latency in workload assignment. They have the most impact when working in large Intune environments, like environments with >100,000 devices. These recommendations should be considered with other design aspects, like manageability, ease of use, role-based administration, and simplicity.

### Use the built-in virtual groups

| DO | DON'T |
| --- | --- |
| ✅ Use the **All users** and **All devices** virtual groups instead of creating your own version of all users/all devices using Microsoft Entra dynamic groups. | ❌ Don't create your own "All users" or "All devices" dynamic groups for policy and app targeting in Intune.

Larger groups take longer to sync membership updates between Microsoft Entra ID and Intune. The **All users** and **All devices** are usually the largest groups you have. If you assign Intune workloads to large Microsoft Entra groups that have many users or devices, then synchronization backlogs can happen in your Intune environment. This backlog impacts policy and app deployments, which take longer to reach managed devices.

> [!IMPORTANT]
> The update from Entra to Intune is relatively quick, typically within 5 minutes or so, but it is not instantaneous. This is most crucial for enrollment assignments, admins should try to enroll devices only after several minutes, and not immediately after adding the enrolling users to a group, for optimal performance throughout Intune. 

The built-in **All users** and **All devices** groups are Intune-only grouping objects that don't exist in Microsoft Entra ID. There isn't a continuous sync between Microsoft Entra ID and Intune. So, group membership is instant. 

> [!NOTE]
> For information on Intune check-in policy refresh intervals, go to [Intune Policy refresh intervals](../configuration/device-profile-troubleshoot.md#policy-refresh-intervals).

You can also apply this optimization to other large and frequently changing groups you might have, like "All windows devices" or "all iOS devices". Instead of creating and targeting these groups, use the existing "All users" or "All devices" virtual groups, since Intune policies and applications are automatically scoped by platform.

When using very large groups in Intune (over 100,000 members), expect some initial delay in targeting. There's a first time setup process that happens between Microsoft Entra ID and Intune. The first full sync always takes longer than subsequent incremental syncs.

### Reuse groups

| DO | DON'T |
| --- | --- |
| ✅ Reuse the same group objects for assigning multiple policies. | ❌ Don't create duplicate copies of the same group to target different policies. <br/><br/> ❌ Don't create dedicated "App groups" or "Policy groups". |

Behind the scenes, Intune converts Microsoft Entra group members to assignment targeting messages for each user and device. This process is highly optimized when the group objects are the same.

For example, Intune grouping and targeting works best when the "Engineering" user group is targeted with 10 policies. It doesn't work best when the Engineering users are members of 10 different groups, with each group assigned to a different policy.

We've seen a few designs not using this guidance. For example, IT admins create an "Install_Edge" group, create a "Deploy_Edge_Config_Policy" group, and then put the same devices in each group, which isn't recommended for performance.

A similar and not recommended pattern is creating "App groups". An app group is when each app has several Microsoft Entra groups created for it. For example, to manage the Microsoft Edge application, an admin creates the following groups:

- Edge_Required
- Edge_Available
- Edge_Uninstall

The admin adds individual user or devices into these groups. These app groups dramatically increase the number of Microsoft Entra groups that Intune must subscribe to and monitor for membership updates, which is less efficient. Inefficient group sync design impacts how fast new assignments are created and delivered to devices.

### Make incremental group changes

| DO | DON'T |
| --- | --- |
| ✅ Be careful with large group nesting changes in Microsoft Entra ID.| ❌ Don't make large group nesting changes all at once. |

A large group membership change in Microsoft Entra ID can generate bursts of targeting changes in Intune. These bursts can delay targeting of other assignments in your environment.

If a set of admins manage your groups and another set manages Microsoft Entra ID, then you should communicate the impact Microsoft Entra ID changes can have on Intune targeting.

For example, if a Microsoft Entra admin nests new large groups within an existing group that Intune uses for targeting, then Intune begins syncing all groups and group memberships. The time it takes to process all memberships depends on the number and size of group changes made in Microsoft Entra ID.

This recommendation also applies when groups are "unnested". For more information on nested groups, go to [Manage Microsoft Entra groups and group membership](/azure/active-directory/fundamentals/how-to-manage-groups).

### Use filters to include and exclude

| DO | DON'T |
| --- | --- |
| ✅ Use filters to achieve the correct user+device combination for targeting. | ❌ Don't mix user groups and device groups when using Include and Exclude groups. |

This recommendation is also a support statement. We don't recommend or support creating assignments to user groups and excluding a device group from that assignment, or vice-versa.

This recommendation exists due to the timing/latency characteristic of dynamic groups. **Excluded groups** membership isn't instant, which can result in cases where devices incorrectly receive app or policy assignments. To understand more, go to [Assign policies and profiles - support matrix](../configuration/device-profile-assign.md#support-matrix).

Instead of mixed exclusions, we recommend assigning to a user group. Then, use filters to dynamically include or exclude the appropriate devices.

## Summary

When creating and managing assignments in Intune, incorporate some of these recommendations. Use groups or virtual groups, and apply filters to help refine the targeting scope. Keep the best practices in mind:

- Don't create your own version of "All users" or "All devices" groups. Use the Intune virtual groups, as they don't require Microsoft Entra ID syncing when a new user or device is added to the environment.
- To optimize your targeting, reuse groups as much as possible.
- Take care when making large nesting changes to Intune groups. Intune needs to process all these changes and calculate effective changes for all the members of all the groups impacted by that change. 
- Intune doesn't support mixed group exclusions. So, use filters to dynamically include and exclude devices in addition to group or virtual group assignments.

## Related articles

- [Use filters when assigning your apps, policies, and profiles](filters.md)
- [Supported device properties when creating filters](filters-device-properties.md)
- [Supported workloads when creating filters](filters-supported-workloads.md)
- [Filter reports and troubleshooting](filters-reports-troubleshoot.md)
