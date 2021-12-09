---
# required metadata

title: Add or configure education settings in Microsoft Intune
description: Use the Take a Test app in a device configuration profile on Windows 10 and later devices in Microsoft Intune. Create a configuration profile using the Education settings, and enter a test app URL, choose how users sign-in, monitor the screen during the test, and allow or prevent text suggestions during the test.
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 01/29/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:
ms.assetid: 6f4de4bd-3dde-4a8d-8e22-46c5d06c3eea

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Use the Take a Test app on Windows 10 devices in Microsoft Intune

Education profiles in Intune are designed for students to take a test or exam on devices. This feature includes the **Take a Test** app and settings to add a test URL, choose how end-users sign in to the test, and more. This feature supports the following platform:

- Windows 10 and newer

When the user signs in, the Take a Test app automatically opens with the test you entered. No other apps can run on the device while the test is in progress. [Take tests in Windows 10](/education/windows/take-tests-in-windows-10) provides more details on the Take a Test app.

This article lists the steps to create a device configuration profile  in Microsoft Intune. It also includes information to read and learn about the available education settings for your Windows 10 devices.

## Create a device profile

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Platform**: Select **Windows 10 and later**.
    - **Profile**: Select **Templates** > **Secure assessment (Education)**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the new profile.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. Select **Next**.
7. In **Configuration settings**, enter the settings you want to configure:

    - [Windows 10 and newer](education-settings-windows.md)

8. Select **Next**.

9. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, see [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

10. In **Assignments**, select the users or user group that will receive your profile. For more information on assigning profiles, see [Assign user and device profiles](device-profile-assign.md).

    Select **Next**.

11. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

The next time each device checks in, the policy is applied.

## Next steps

See a list of the [Windows 10 education settings](education-settings-windows.md) and their descriptions.

After the [profile is assigned](device-profile-assign.md), [monitor its status](device-profile-monitor.md).