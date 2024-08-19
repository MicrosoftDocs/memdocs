---
# required metadata
title: User settings in Windows 365
titleSuffix:
description: Learn about user settings in Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 07/26/2023
ms.topic: how-to
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
- essentials-manage
---

# User settings

The **User settings** page lets IT administrators manage the following settings for the user:

- **Enable local admin**: If enabled, each user in the assigned groups is elevated to a local administrator of each of their own Cloud PCs. These permissions apply at the user level.
- **Enable users to reset their Cloud PCs**: If enabled, a **Reset** option is shown in the Windows 365 app and portal for users in the assigned groups. Resetting wipes and reprovisions the Cloud PC, deleting all user data and apps.
- **Allow user to initiate restore service**: If enabled, each user in the assigned groups can restore their own Cloud PCs to any available backup version.

When managing settings, keep the following points in mind:

- The settings can be applied before or after a Cloud PC is assigned.
- Changes to the settings take effect when the user logs on. If the user is currently logged on, they must sign out and then sign in again to see the change.

## Add a new setting

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Windows 365** (under **Provisioning**) > **...** > **User Settings** > **Add**.
![Screenshot of add user setting](./media/assign-users-as-local-admin/user-settings.png)
2. Under **Settings**, enter a **Name** for the setting.
3. Select the boxes for the settings that you want to enable for the users.
    - If you selected **Allow user to initiate restore service**, also select an option for **Frequency of restore-point service**.
5. Select **Next**.  
6. Under **Assignments**, choose **Add Groups**.
7. Under **Select groups to include**, choose a group of users to get the settings > **Select**.  
8. Select **Next**.
9. On the **Review + save** page, select **Create**.  

## Edit a user setting

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Windows 365** (under **Provisioning**) > **...**  > **User Settings**.
2. The **User Settings** page shows the current settings.  
3. Select the user setting that you want to edit.
5. To change the name of the policy or to turn settings on or off, select **Edit** next to **Settings**.
6. Under **Settings**, make any changes you want, and then select **Next**.  
7. On the **Review + Save** page, select **Update**.  
8. To edit assignments, select **Edit** next to **Assignments** > **Add Groups** to add another group. To remove existing groups, select the ellipses (**…**) > **Remove**.  
9. Select **Next**.  
10. On the **Review + Save** page, select **Update**.  

## Delete a user setting

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Windows 365** (under **Provisioning**) > **...**  > **User Settings**.
2. On the **User settings** page, you can view the created settings.  
3. Select the ellipses (**…**) in the row of the setting you want to delete > **Delete**.
4. Select **Yes** on the confirmation pop up to delete the setting permanently.

## Conflict Resolution for Local Admin

Because user setting policies are assigned to user groups, there’s a possibility of overlap for groups/users. If a user is assigned to more than one user setting policy, user settings from the most-recently created policy will be used and ignore all others. The last time a policy was updated doesn't affect this priority. To make sure user settings are consistent and clear, avoid any policy targeting overlaps.

<!-- ########################## -->
## Next steps

[Learn about security in Windows 365](security-guidelines.md).
