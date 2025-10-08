---
title: Add groups to organize users and devices for Microsoft Intune
description: Create Microsoft Entra groups to organize users and devices for use with Microsoft Intune.
author: paolomatarazzo
ms.author: paoloma
ms.date: 06/23/2025
ms.topic: how-to
ms.reviewer: scottduf
ms.collection:
- M365-identity-device-management
- highpri
---

# Use groups to organize users and devices for Microsoft Intune

Microsoft Intune uses security groups from Microsoft Entra ID for various organizational needs. These needs include the grouping of users or devices by geographic location, department, hardware characteristics, and more. To support the use of Entra groups by Intune, the Intune admin center includes the Entra Groups user interface with all its functionality. Any groups that appear in Entra and new groups that an Intune admin might create are visible in Intune, Entra, and other products that share the Entra Groups user interface like Microsoft 365.

Intune admins use well-defined groups when deploying policies, deploying apps, and for assigning other administrative users' permissions so they can help administer different aspects of the Intune subscription.

This article focuses on using the Intune admin center to create groups for use with Intune, including details about the permissions required to manage and use those groups within the admin center.

You can learn more about [Microsoft Entra groups](/entra/fundamentals/concept-learn-about-groups#microsoft-entra-groups-overview) in the Entra documentation.

## Role-based access controls for working with groups

By default, all Microsoft Entra user accounts have permissions to create and configure new groups without being assigned an Entra role-based access control (RBAC) role. These permissions extend to use of the Groups node within the Intune admin center.

Only the user who created the group, users who are assigned as an *Owner*, and users who have sufficient Entra RBAC permissions to manage Entra groups can edit the properties of a group. Other users without rights to edit a group can view its membership, and if administering Intune, can assign Intune policies, apps, and role assignments to the group.


The following Microsoft Entra built-in RBAC role is the least privileged built-in role that includes sufficient permissions to edit and  manage Entra groups created by other users:

- [**Groups Administrator**](/entra/identity/role-based-access-control/permissions-reference#groups-administrator) – This role provides permissions sufficient to add and edit groups from within the admin centers for Microsoft Intune, Microsoft Entra, and Microsoft 365.

When you work with RBAC, Microsoft recommends following the principle of least-permissions by using only accounts that have the minimum required permissions for a task, and limiting use and assignment of privileged administrative roles like the Intune Administrator.

To learn more about Microsoft Entra groups and group access, see [Learn about groups and access rights](/entra/fundamentals/concept-learn-about-groups) in the Entra documentation.

## Requirements of groups you use with Intune

Intune admins should be aware of the following aspects of Microsoft Entra groups when creating new groups or assigning them for policy deployment or administrative roles.

**Security** - The groups you use with Intune must be groups that are enabled for security. This typically requires the groups [group type](/entra/fundamentals/concept-learn-about-groups#group-types) be set to *Security* when the group is created. A security group supports both users and devices as members.

By default, *Microsoft 365* groups in Microsoft Entra aren't security-enabled, support only users as members, and aren't supported by Intune. While you can [use Microsoft Graph PowerShell](/microsoft-365/enterprise/manage-security-groups-with-microsoft-365-powershell) to create security-enabled Microsoft 365 groups that Intune supports, like the default Microsoft 365 groups they can only include users and not devices.

**Membership** - Intune supports both *Assigned* and *Dynamic group* memberships. Choose the [membership type](/entra/fundamentals/concept-learn-about-groups#membership-types) based on how you plan to manage group membership - manually or automatically based on rules. For example, to assign a built-in Intune RBAC role like the Endpoint Security Manager to administrative users, use a group with manually assigned members to limit who receives that privileged role. Conversely, to deploy a default set of device configuration policies to all Windows 11 devices, you might use a group that dynamically adds members based on a devices operating system version. Use of a dynamic group can help you ensure devices that enroll with Intune automatically receive the intended default policy without the device having to be manually added to a group.

## The Intune All users and All devices groups

In addition to the Microsoft Entra groups that you can create and use with Intune, Intune includes two virtual groups that are only available within the context of Intune and from within the Intune admin center:

- *All users* - This group automatically includes every user who has a license for Intune.
- *All devices* - This group automatically includes each device that enrolls with Intune.

These virtual groups provide an easy way to target all applicable users or devices with Intune policies and assignments that should broadly apply.

For example, you might deploy an Intune compliance policy to the *all devices* group to establish a minimum level of compliance requirements that all devices in your organization must meet. Later, you can deploy more requirements to specific Entra groups to apply extra requirements you might have for specific groups of devices or users.

> [!TIP]
> Consider the use of **Filters** for groups within Intune. You can use Filters within Intune when assigning apps, policies, and profiles in Microsoft Intune to large groups like *All users* and *All devices*. Filters can help you dynamically control which devices or users receive the deployment. For information about using Filters, see:
> - [Use filters when assigning your apps, policies, and profiles in Microsoft Intune](/intune/intune-service/fundamentals/filters)
> - [Performance recommendations for Grouping, Targeting, and Filtering in large Microsoft Intune environments](/intune/intune-service/fundamentals/filters-performance-recommendations)

## Add groups to Intune

When you create a group within the Microsoft Intune admin center, you're actually creating a group in Microsoft Entra ID. The following procedure provides basic guidance for creating groups in the Intune admin center. For more detailed information, see the following Microsoft Entra articles:

- [Manage Microsoft Entra groups and group membership](/entra/fundamentals/how-to-manage-groups)
- [Create a basic group and add members using Microsoft Entra ID](/entra/fundamentals/how-to-manage-groups)
- [Dynamic membership rules for groups in Microsoft Entra ID](/entra/identity/users/groups-dynamic-membership)

To create groups in the Microsoft Intune admin center:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), and then select **Groups** > **New group**:

   :::image type="content" source="./media/groups-add/groups-add-new.png" alt-text="Screenshot that shows Groups pane of the Intune admin center." lightbox="./media/groups-add/groups-add-new.png":::

2. The *New Group* pane opens, which is the same interface as found in Microsoft Entra:

   :::image type="content" source="./media/groups-add/groups-add-properties.png" alt-text="Screenshot that shows the New group pane from Entra within the Intune admin center.":::

   Configure the following options for the New Group:
   1. Set *Group type* to **Security**.
   2. For *Group name*, specify a meaningful name that clearly identifies the group. This name is visible to users who work with groups in the admin center.
   3. For *Group description*, which is optional, specify other details about the group like its intended use.
   4. For *Membership type*, select from the following options:

      - **Assigned** – With this membership type you'll need to manually add users to the group, which can be done now or later after the group is created.

        To add users at this time, locate and select **No members selected** to open the *Add members* pane.

        On the pane, use the *Users* or *Devices* tab where you can select the checkbox next to each object that you want to add to this group.

        You can also select the *Groups* tab if you want to nest a group within this group. A group that includes a group as a member is known as a parent group. Be careful when nesting groups as the membership relationships might not be clear to admins who later use the parent group for an assignment. Any membership changes made to a nested group are automatically applied to the effective membership of the parent group.

        > [!IMPORTANT]
        > Avoid creating groups that include both users and devices, as this can lead to policy conflicts and unpredictable behavior during Intune deployments.

        > [!TIP]
        > To create groups of devices, you can use [device categories](/intune/intune-service/enrollment/device-group-mapping) to automatically join devices to a group at the time they enroll with Intune.

      - **Dynamic User** - With this membership type, select **Add dynamic query** and then configure the dynamic membership rules. For guidance, see [Manage rules for dynamic membership groups in Microsoft Entra ID](/entra/identity/users/groups-dynamic-membership).

        > [!IMPORTANT]
        > To use Dynamic User groups, you must have a [Microsoft Entra ID P1 license for each user](/entra/identity/users/groups-dynamic-membership#license-requirements) that is a member of the dynamic group.

      - **Dynamic Device** - With this membership type, select **Add dynamic query** and then configure the dynamic membership rules. For guidance, see [Manage rules for dynamic membership groups in Microsoft Entra ID](/entra/identity/users/groups-dynamic-membership).

        > [!TIP]
        > No specific Entra ID license is required for members of dynamic device groups.

   5. The *Owners* configuration is optional. By default, the user that creates a group is an owner. To add other owners, select **No owners selected** and then the **Users** tab, where you can then select one or more users to add as owners of this group.

3. Select **Create** to add the new group. Your group is shown in the list.


## Edit a group

As an Intune admin, you can edit groups, such as changing the group members, owner, and properties.

Use the following steps to edit an existing group:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Groups** > **All groups** > *select the name of a group to edit*.
3. Under the **Manage** menu group, select an area of the group to edit, like **Properties**, **Members**, or **Owners**. Intune displays the user interface related to that configuration option.

## Delete a group

As an Intune admin, you can delete groups that are no longer needed.

Use the following steps to delete an existing group:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Groups** > **All groups**.
3. Select the checkbox for each group you want to delete, and then select **Delete** from options at the top of the *All Groups* view. Alternately, you can select the name of a group to open a single group's *Overview* page, and then select *Delete** from the top of that view.

> [!TIP]
> After a group is deleted, it might take some time before it appears in the *Deleted groups* list.

## Related content

- [Assign users licenses to Intune](../fundamentals/licenses-assign.md)
- [Assign Microsoft Intune roles to groups of users for role-based access control](../fundamentals/assign-role.md)