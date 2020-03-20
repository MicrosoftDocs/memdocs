---
# required metadata

title: Create a Wi-Fi profile for devices in Microsoft Intune - Azure | Microsoft Docs
description: See the steps to create a Wi-Fi device configuration profile in Microsoft Intune. Create profiles for Android device administrator, Android Enterprise, Android kiosk, iOS, iPadOS, macOS, Windows 10 and newer, and Windows Holographic for Business. Use these profiles to create a WiFi connection to use certificates, choose an EAP type, select an authentication method, enable a proxy, and more.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: maholdaa
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Add and use Wi-Fi settings on your devices in Microsoft Intune

Wi-Fi is a wireless network that's used by many mobile devices to get network access. Microsoft Intune includes built-in Wi-Fi settings that can be deployed to users and devices in your organization. This group of settings is called a "profile", and can be assigned to different users and groups. Once assigned, your users get access your organization's Wi-Fi network without configuring it themselves.

For example, you install a new Wi-Fi network named Contoso Wi-Fi. You then want to set up all iOS/iPadOS devices to connect to this network. Here's the process:

1. Create a Wi-Fi profile that includes the settings that connect to the Contoso Wi-Fi wireless network.
2. Assign the profile to a group that includes all users of iOS/iPadOS devices.
3. On their devices, users find the new Contoso Wi-Fi network in the list of wireless networks. They can then connect to the network, using the authentication method of your choosing.

This article lists the steps to create a Wi-Fi profile. It also includes links that describe the different settings for each platform.

## Supported device platforms

Wi-Fi profiles support the following device platforms:

- Android 4 and newer
- Android Enterprise and kiosk
- iOS 8.0 and newer
- iPadOS 13.0 and newer
- macOS X 10.11 and newer
- Windows 10 and newer, Windows 10 Mobile, and Windows Holographic for Business

> [!NOTE]
> For devices running Windows 8.1, you can import a Wi-Fi configuration that was previously exported from another device.

## Create the profile

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Platform**: Choose the platform of your devices. Your options:

      - **Android device administrator**
      - **Android Enterprise**
      - **iOS/iPadOS**
      - **macOS**
      - **Windows 10 and later**
      - **Windows 8.1 and later**

    - **Profile**: Select **Wi-Fi**.

      > [!TIP]
      >
      > - For **Android Enterprise** devices running as a dedicated device (kiosk), choose **Device owner only** > **Wi-Fi**.
      > - For **Windows 8.1 and later**, you can choose **Wi-Fi import**. This option lets you import Wi-Fi settings as an XML file that you previously exported from a different device.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later. For example, a good profile name is **WiFi profile for entire company**.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. Select **Next**.
7. In **Configuration settings**, depending on the platform you chose, the settings you can configure are different. Select your platform for detailed settings:

    - [Android device administrator](wi-fi-settings-android.md)
    - [Android Enterprise](wi-fi-settings-android-enterprise.md), including dedicated devices
    - [iOS/iPadOS](wi-fi-settings-ios.md)
    - [macOS](wi-fi-settings-macos.md)
    - [Windows 10 and later](wi-fi-settings-windows.md)
    - [Windows 8.1 and later](wi-fi-settings-import-windows-8-1.md), including Windows Holographic for Business

8. Select **Next**.
9. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, see [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

10. In **Assignments**, select the user or groups that will receive your profile. For more information on assigning profiles, see [Assign user and device profiles](device-profile-assign.md).

    Select **Next**.

11. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

## Next steps

The profile is created, but it's not doing anything. Next, [assign this profile](device-profile-assign.md) and [monitor its status.](device-profile-monitor.md).

[Troubles Wi-Fi profiles in Intune](troubleshoot-wi-fi-profiles.md).
