---
# required metadata

title: Include and exclude app assignments in Microsoft Intune
titleSuffix: 
description: Learn how you can use Microsoft Intune to include and exclude app assignments.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/01/2023
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
2. Select **Apps** > **All apps**. The list of added apps is shown.
3. Select the app that you want to assign. A dashboard displays information about the app.
4. In the **Manage** section of the menu, select **Properties**.

    ![Include app assignments when assigning apps](https://github.com/MicrosoftDocs/memdocs/assets/114827544/231b18c4-31a2-468b-8747-b1800d2e6be5)

5. Select **Edit** next to **Assignments**.
6. Select **Add all users** below **Available with or without enrollment** to assign this app to all users.

    ![Intune app assignments - Add all users](https://github.com/MicrosoftDocs/memdocs/assets/114827544/9ed306f6-77f3-4e08-9cee-b6eee6ac114c)

9. Select **Add group** below **Available with or without enrollment**.
10. Select the **group** of **users** that you wish to exclude.

    ![Intune app assignements - Select group](https://github.com/MicrosoftDocs/memdocs/assets/114827544/93353297-a313-46c0-9633-635cd4f16c0d)

13. Select **Select** to complete your group selection.

    ![Intune app assignements - Included groups](https://github.com/MicrosoftDocs/memdocs/assets/114827544/02159d59-0bd3-4e0c-a42d-7d544c43b5fb)
    
    > [NOTE]
    > By default, the groups you select are assigned in included mode.

15. Select **Included** on the group line you have just assigned to define the group as excluded.

    ![Intune assignements - Exclud group](https://github.com/MicrosoftDocs/memdocs/assets/114827544/1ec738e3-b1d4-4fd9-bf6c-91e5a56642a4)

18. Select **OK** to set the group to be excluded.
20. Select **Review + save** to complete your assignements.
21. Review the summary of your modification and select **Save** to finish.

To edit assignments, in the app **Assignments** list, select the row that contains the specific assignment that you want to change. You can also remove an assignment by selecting the ellipse (**…**) at the end of a row, and then selecting **Remove**.

> [!NOTE]
> Removing a group assignment does not remove the related app except on Android Enterprise dedicated, fully managed, and corporate-owned work profile devices. The installed app will remain on the device.  
## Next steps

- For more information about including and excluding group assignments for apps, see the [Microsoft Intune blog](https://aka.ms/new_app_assignment_process).
- Learn how to [monitor app information and assignments](apps-monitor.md).
