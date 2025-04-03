---
# required metadata
title: Shared or multi-user Windows device settings in Microsoft Intune
description: Add and use Windows 10/11 and Windows Holographic for Business devices that are shared, or used by multiple users in Microsoft Intune. See a list of all the settings and what they do on the devices, including Microsoft HoloLens. Control guest accounts, manage accounts and delete inactive accounts, allow or prevent saving to local storage, set power and sleep options, choose when updates are installed, and use devices in education environments in a device configuration profile.
keywords: intune shared device, shared device intune, sharedpc
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/22/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high

# optional metadata
#ROBOTS:
#audience:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Control access, accounts, and power features on shared PC or multi-user Windows devices using Intune

Devices that have multiple users are called shared devices, and are a common part of mobile device management (MDM) solutions. Using Microsoft Intune, you can create and configure shared devices.

For example, schools have devices that are typically used by many students. School Intune admins can turn on the Shared PC feature to allow one user at a time. Students can't switch between different signed-in accounts on the device. When the student signs out, you also choose to remove all user-specific settings.

With this feature:

- End users can sign in to these shared devices with a guest account. After users sign in, the credentials are cached.
- You control if the guest account deletes when the user signs off, or delete inactive accounts when a threshold is reached.
- As end users use the device, they only get access to features you allow. For example, you:

  - Choose when the device goes in to sleep mode
  - Decide if users can see and save files locally
  - Can enable or disable power management settings

End users can sign in to these shared devices with a guest account. After users sign in, the credentials are cached. As they use the device, end-users only get access to features you allow.

For example, you choose when the device goes in to sleep mode, if users can see and save files locally, enable or disable power management settings, and more. You also control if the guest account deletes when the user signs-off, or delete inactive accounts when a threshold is reached.

This article shows you how to create a shared multi-user device configuration profile, and includes links to the available settings.

When you create the profile in Intune, you deploy or assign the profile to device groups in your organization. You can also assign this profile to device groups with mixed device types and operating system (OS) versions.

This feature applies to:

- Windows 10/11 Professional
- Windows 10/11 Enterprise
- Windows Holographic for Business, such as the HoloLens

> [!TIP]
> For iOS/iPadOS shared devices, go to [shared device solutions for iOS/iPadOS](../enrollment/device-enrollment-shared-ios.md).

## Prerequisites

- To create the policy, at a minimum, sign in with an account that has the **Policy and Profile Manager** Intune role. For more information, go to [Role-based access control (RBAC) with Microsoft Intune](../fundamentals/role-based-access-control.md).

## Create the profile

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy**.
3. Enter the following properties:

   - **Platform**: Select **Windows 10 and later**.
   - **Profile type**: Select **Templates** > **Shared multi-user device**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

   - **Name**: Enter a descriptive name for the new profile.
   - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. Select **Next**.
7. In **Configuration settings**, depending on the platform you chose, the settings you can configure are different. Choose your platform for detailed settings:

    - [Windows 10/11](shared-user-device-settings-windows.md)
    - [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md)

8. Select **Next**.

9. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, go to [Use role based access control (RBAC) and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

10. In **Assignments**, select the devices group that receives your profile. For more information on assigning profiles, go to [Assign user and device profiles](device-profile-assign.md).

    Select **Next**.

    > [!NOTE]
    > Be sure to assign the profile to device groups in your organization.

11. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

The next time each device checks in, the policy is applied.

## Related articles

- See all the settings for [Windows 10/11](shared-user-device-settings-windows.md) and [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md).
- [Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).
