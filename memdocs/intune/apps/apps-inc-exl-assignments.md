---
# required metadata

title: Include and exclude app assignments in Microsoft Intune
titleSuffix: 
description: Learn how you can use Microsoft Intune to include and exclude app assignments.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/17/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.assetid: c59f6df5-3317-4dff-8f19-fdeec33faedf

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: bryanke
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Include and exclude app assignments in Microsoft Intune

In Intune, you can determine who has access to an app by assigning groups of users to include and exclude. Before you assign groups to the app, you must set the assignment type for an app. The assignment type makes the app available, required, or uninstalls the app.

To set the availability of an app, you include and exclude app assignments to a group of users or devices by using a combination of include and exclude group assignments. This capability can be useful when you make the app available by including a large group, and then narrow the selected users by also excluding a smaller group. The smaller group might be a test group or an executive group.

As a best practice, create and assign apps specifically for your user groups, and separately for your device groups. For more information on groups, see [Add groups to organize users and devices](../fundamentals/groups-add.md).  

Important scenarios exist when including or excluding app assignments:

- Exclusion takes precedence over inclusion in the following same group type scenarios:
  - Including user groups and excluding user groups when assigning apps
  - Including device groups and excluding device group when assigning apps

    For example, if you assign a device group to the **All corporate users user** group, but exclude members in the **Senior Management Staff** user group, **All corporate users** except the **Senior Management staff** get the assignment, because both groups are user groups.
- Intune doesn't evaluate user-to-device group relationships. If you assign apps to mixed groups, the results may not be what you want or expect.

For example, if you assign a device group to the **All Users** user group, but exclude an **All personal devices** device group, **All users** get the app. The exclusion does not apply.

As a result, it's not recommended to assign apps to mixed groups.

> [!NOTE]
> When you set a group assignment for an app, the **Not Applicable** type is deprecated and replaced with exclude group functionality.
>
> Intune provides pre-created **All Users** and **All Devices** groups in the Microsoft Intune admin center. The groups have built-in optimizations for your convenience. It's highly recommended that you use these groups to target all users and all devices instead of any "all users" or "all devices" groups that you might create yourself.  
>
> Android enterprise supports including and excluding groups. You can leverage the built-in **All Users** and **All Devices** groups for Android enterprise app assignment.

## Include and exclude groups when assigning apps

To assign an app to groups by using the include and exclude assignment:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All apps**. The list of apps that has been added to Intune is shown.
3. Select the app that you want to assign. A dashboard displays information about the app.
4. Select **Properties** under the **Manage** section.
5. Select **Edit** next to **Assignments**.
6. Select **Add all users** under the **Available with or without enrollment** section to assign this app to all users.
7. Select **Add group** under the **Available with or without enrollment** section.
8. Select the group that you want to exclude from the app assignment.
9. Click **Select** to include the group.
10. Select **Included** under the **Group mode** next to the group you added. The **Edit assignment** pane will be displayed.

    > [NOTE]
    > By default, the groups you select are assigned in included mode.

11. Select **Exclude** as the **Mode** under the **Assignment settings** in the **Edit assignment** pane.
12. Select **OK** to exclude the selected group.
15. Select **Excluded Groups** to select the groups of users that you want to make this app unavailable to.
16. Select the groups to exclude. This makes this app unavailable to those groups.
17. Click **Review + save** to make your group assignments active for the app.

> [!NOTE]
> When you add a group, if any other group has already been included for a specific assignment type, the app is preselected and can't be modified for other include assignment types. The group that has been used can't be used as an included group.

When you make group assignments, groups that have already been assigned aren't available to be modified. If you want to select a group that currently isn't available, first remove the group from the app's assigned list.

To edit assignments, in the app **Assignments** pane, select the row that contains the specific assignment that you want to change. You can also remove an assignment by selecting the ellipse (**…**) at the end of a row, and then selecting **Remove**.

> [!NOTE]
> Removing a group assignment does not remove the related app except on Android Enterprise dedicated, fully managed, and corporate-owned work profile devices. The installed app will remain on the device.  

## Next steps

- For more information about including and excluding group assignments for apps, see the [Microsoft Intune blog](https://aka.ms/new_app_assignment_process).
- Learn how to [monitor app information and assignments](apps-monitor.md).
