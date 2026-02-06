---
title: Restrict devices features using policy in Microsoft Intune
description: Add a device configuration profile to restrict features on Android device administrator, Android Enterprise, AOSP, macOS, iOS, iPadOS, and Windows 10/11 client devices in Microsoft Intune.
author: MandiOhlinger
ms.author: mandia
ms.date: 10/14/2025
ms.topic: how-to
ms.reviewer: mikedano
ms.collection:
- M365-identity-device-management
- highpri
---

# Configure device restriction settings in Microsoft Intune

[!INCLUDE [android_device_administrator_support](../includes/android-device-administrator-support.md)]

Intune includes device restriction policies that help administrators control Android, iOS/iPadOS, macOS, and Windows devices. These restrictions let you control a wide range of settings and features to protect your organization's resources. For example, admins can:

- Allow or block the device camera.
- Control access to Google Play, app stores, viewing documents, and gaming.
- Block built-in apps, or create a list of apps that allowed or prohibited.
- Allow or prevent backing up files to cloud and storage accounts.
- Set a minimum password length, and block simple passwords.

These features are available in Intune, and are configurable by the administrator. Intune uses **configuration profiles** to create and customize these settings for your organization's needs. After you add these features in a profile, you then assign the profile to devices in your organization.

This feature applies to:

- Android device administrator
- Android Open Source Project (AOSP)
- Android Enterprise personally owned devices with a work profile
- iOS/iPadOS
- macOS
- Windows

This article shows you how to create a device restrictions profile. You can also see all the available settings for the different platforms.

## Create the profile

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy**.
3. Enter the following properties:

    - **Platform**: Select the platform of your devices. Your options:

        - **Android device administrator**
        - **Android (AOSP)**
        - **Android Enterprise**
        - **iOS/iPadOS**
        - **macOS**
        - **Windows 10 and later**

    - **Profile type**: Select **Device restrictions**. Or, select **Templates** > **Device restrictions**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, a good policy name is **iOS/iPadOS: Block camera on devices**.
    - **Description**: Enter a description for the policy. This setting is optional, but recommended.

6. Select **Next**.

7. In **Configuration settings**, depending on the platform you chose, the settings you can configure are different. Select your platform for detailed settings:

    - [Android](device-restrictions-android-for-work.md)
    - [iOS/iPadOS](device-restrictions-apple.md)
    - [macOS](device-restrictions-apple.md)
    - [Windows](device-restrictions-windows-10.md)

8. Select **Next**.
9. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, like `US-NC IT Team` or `JohnGlenn_ITDepartment`. For information about scope tags, go to [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

10. In **Assignments**, select the users or groups that will receive your profile. For information on assigning profiles, go to [Assign user and device profiles](device-profile-assign.md).

    Select **Next**.

11. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

## Related articles

- [Assign the profile](device-profile-assign.md).
- [Monitor the profile status](device-profile-monitor.md).
