---
# required metadata

title: Restrict devices features using policy in Microsoft Intune
description: Add a device configuration profile to restrict features on Android device administrator, Android Enterprise, AOSP, macOS, iOS, iPadOS, and Windows 10/11 client devices in Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/19/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mikedano
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---
 
# Configure device restriction settings in Microsoft Intune

[!INCLUDE [windows-phone-81-windows-10-mobile-support](../includes/windows-phone-81-windows-10-mobile-support.md)]

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
- Windows 11
- Windows 10
- Windows 8.1

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
        - **Windows 8.1 and later**

    - **Profile type**: Select **Device restrictions**. Or, select **Templates** > **Device restrictions**.

        To create a device restrictions profile for Windows 10 Team devices, like Surface Hub, then select **Device restrictions (Windows 10 Team)**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, a good policy name is **iOS/iPadOS: Block camera on devices**.
    - **Description**: Enter a description for the policy. This setting is optional, but recommended.

6. Select **Next**.

7. In **Configuration settings**, depending on the platform you chose, the settings you can configure are different. Select your platform for detailed settings:

    - [Android device administrator](device-restrictions-android.md)
    - [Android (AOSP)](device-restrictions-android-aosp.md)
    - [Android Enterprise corporate-owned devices](device-restrictions-android-for-work.md) and [BYOD personally owned devices](device-restrictions-android-enterprise-personal.md)
    - [iOS/iPadOS](device-restrictions-ios.md)
    - [macOS](device-restrictions-macos.md)
    - [Windows 8.1](device-restrictions-windows-8-1.md)
    - [Windows 10/11](device-restrictions-windows-10.md)
    - [Windows 10 Team](device-restrictions-windows-10-teams.md)
    - [Windows Holographic for Business](device-restrictions-windows-holographic.md)

8. Select **Next**.
9. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, like `US-NC IT Team` or `JohnGlenn_ITDepartment`. For information about scope tags, go to [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

10. In **Assignments**, select the users or groups that will receive your profile. For information on assigning profiles, go to [Assign user and device profiles](device-profile-assign.md).

    Select **Next**.

11. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

## Related articles

- [Assign the profile](device-profile-assign.md).
- [Monitor the profile status](device-profile-monitor.md).
