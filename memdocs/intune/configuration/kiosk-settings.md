---
# required metadata

title: Kiosk settings for Windows and Holographic devices in Microsoft Intune
description: Configure your Windows 10/11 and Windows Holographic for Business devices as single-app and multi-app kiosks, customize the start menu, add apps, show the task bar, and configure a web browser in Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/17/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mikedano
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; seodec18
ms.collection:
- tier2
- M365-identity-device-management
---

# Windows and Windows Holographic for Business device settings to run as a dedicated kiosk using Intune

On Windows devices, use Intune to run devices as a kiosk, sometimes known as a dedicated device. A device in kiosk mode can run one app, or run many apps. You can show and customize a start menu, add different apps, including Win32 apps, add a specific home page to a web browser, and more.

This feature applies to:

- Windows 11
- Windows 10
- Windows Holographic for Business

To create kiosk profiles for other platforms, go to [Android device administrator](device-restrictions-android.md#kiosk), [Android Enterprise](device-restrictions-android-for-work.md#device-experience), and [iOS/iPadOS](device-restrictions-ios.md#kiosk).

Intune supports one kiosk profile per device. If you need multiple kiosk profiles on a single device, you can use a [Custom OMA-URI](custom-settings-windows-10.md).

Intune uses "configuration profiles" to create and customize these settings for your organization's needs. After you add these features in a profile, push or deploy these settings to groups in your organization.

This article shows you how to run one app or many apps as a Windows kiosk device using a device configuration profile. For a list of all the settings, and what they do, go to [Windows client kiosk settings](kiosk-settings-windows.md) and [Windows Holographic for Business kiosk settings](kiosk-settings-holographic.md).

## Create the profile

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

   - **Platform**: Select **Windows 10 and later**.
   - **Profile**: Select **Templates** > **Kiosk**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

   - **Name**: Enter a descriptive name for the new profile.
   - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. Select **Next**.
7. In **Configuration settings** > **Select a kiosk mode**, choose the type of kiosk mode supported by the policy. Options include:

    - **Not Configured** (default): Intune doesn't change or update this setting. The policy doesn't enable kiosk mode.
    - **Single app, full-screen kiosk**: The device runs as a single user account, and locks it to a single web browser or app. So when the user signs in, a specific app starts. This mode also restricts users from opening new apps, or changing the running app.

      For example, you can run the Microsoft Edge browser, and only show one site, such as `Contoso.com`. Or, you can run a Store app, and have the device locked on this app.

    - **Multi app kiosk**: The device runs multiple Store apps, Win32 apps, web browsers, or inbox Windows apps by using the Application User Model ID (AUMID). Only the apps you add are available on the device.

        The benefit of a multi-app kiosk, or fixed-purpose device, is to provide an easy-to-understand experience for users by only accessing apps they need. And, also removing from their view the apps they don't need.

        > [!NOTE]
        > Currently, multi-app kiosk is only supported on Windows 10. It's not supported on Windows 11.

    For a list of all settings, and what they do, go to:

      - [Windows client kiosk settings](kiosk-settings-windows.md)
      - [Windows Holographic for Business kiosk settings](kiosk-settings-holographic.md)

8. Select **Next**.

9. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, go to [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

10. In **Assignments**, select the users or user group that will receive your profile. For more information on assigning profiles, go to [Assign user and device profiles](device-profile-assign.md).

    Select **Next**.

11. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

The next time each device checks in, the policy is applied.

## Next steps

After the [profile is assigned](device-profile-assign.md), [monitor its status](device-profile-monitor.md).

You can also create kiosk profiles for devices that run the following platforms:

- [Android device administrator](device-restrictions-android.md#kiosk)
- [Android Enterprise](device-restrictions-android-for-work.md#device-experience)
- [Windows 10/11](kiosk-settings-windows.md)
- [Windows Holographic for Business](kiosk-settings-holographic.md)
