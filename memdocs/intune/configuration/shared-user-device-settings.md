---
# required metadata

title: Shared or multi-user device settings in Microsoft Intune
description: Add and use Windows 10/11 and Windows Holographic for Business devices that are shared, or used by multiple users in Microsoft Intune. See a list of all the settings and what they do on the devices, including Microsoft HoloLens. Control guest accounts, manage accounts and delete inactive accounts, allow or prevent saving to local storage, set power and sleep options, choose when updates are installed, and use devices in education environments in a device configuration profile.
keywords:
author: MandiOhlinger

ms.author: mandia
manager: dougeby
ms.date: 01/20/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:
ms.assetid:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; seodec18
ms.collection:
- tier2
- M365-identity-device-management
---

# Control access, accounts, and power features on shared PC or multi-user devices using Intune

Devices that have multiple users are called shared devices, and are a common part of mobile device management (MDM) solutions. Using Microsoft Intune, you can customize shared devices running the following platforms:

- Windows 10/11 Professional
- Windows 10/11 Enterprise
- Windows Holographic for Business, such as the HoloLens

For example, schools have devices that are typically used by many students. With this setting, the school Intune administrator can turn on the Shared PC feature to allow one user at a time. Students can't switch between different signed-in accounts on the device. When the student signs out, you also choose to remove all user-specific settings.

End users can sign in to these shared devices with a guest account. After users sign in, the credentials are cached. As they use the device, end-users only get access to features you allow. For example, you choose when the device goes in to sleep mode, if users can see and save files locally, enable or disable power management settings, and more. You also control if the guest account deletes when the user signs-off, or delete inactive accounts when a threshold is reached.

This article shows you how to create a configuration profile, and includes links to the available settings with their descriptions.

When the profile is created in Intune, you deploy or assign the profile to device groups in your organization. You can also assign this profile to device groups with mixed device types and operating system (OS) versions.

## Create the profile

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

   - **Platform**: Select **Windows 10 and later**.
   - **Profile**: Select **Templates** > **Shared multi-user device**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

   - **Name**: Enter a descriptive name for the new profile.
   - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. Select **Next**.
7. In **Configuration settings**, depending on the platform you chose, the settings you can configure are different. Choose your platform for detailed settings:

    - [Windows 10/11](shared-user-device-settings-windows.md)
    - [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md)

8. Select **Next**.

9. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, see [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

10. In **Assignments**, select the devices group that will receive your profile. For more information on assigning profiles, see [Assign user and device profiles](device-profile-assign.md).

    Select **Next**.

    > [!NOTE]
    > Be sure to assign the profile to device groups in your organization.

11. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

The next time each device checks in, the policy is applied.

## Next steps

- See all the settings for [Windows 10/11](shared-user-device-settings-windows.md) and [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md).
- After the [profile is assigned](device-profile-assign.md), [monitor its status](device-profile-monitor.md).
