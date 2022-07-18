---
# required metadata

title: Create a Wi-Fi profile for devices in Microsoft Intune
description: See the steps to create a Wi-Fi device configuration profile in Microsoft Intune. Create profiles for Android device administrator, Android Enterprise, Android kiosk, iOS, iPadOS, macOS, Windows 10/11, and Windows Holographic for Business. Use these profiles to create a WiFi connection to use certificates, choose an EAP type, select an authentication method, enable a proxy, and more.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/21/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
  - M365-identity-device-management
  - highpri
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

- Android 5 and newer
- Android Enterprise and kiosk
- Android (AOSP)
- iOS 11.0 and newer
- iPadOS 13.0 and newer
- macOS X 10.12 and newer
- Windows 11
- Windows 10
- Windows Holographic for Business

> [!NOTE]
> For devices running Windows 8.1, you can import a Wi-Fi configuration that was previously exported from another device. For more information, see [Import Wi-Fi settings for Windows devices](wi-fi-settings-import-windows-8-1.md).

## Create the profile

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Platform**: Choose the platform of your devices. Your options:

      - **Android device administrator**
      - **Android (AOSP)**
      - **Android Enterprise**
      - **iOS/iPadOS**
      - **macOS**
      - **Windows 10 and later**
      - **Windows 8.1 and later**

    - **Profile**: Select **Wi-Fi**. Or, select **Templates** > **Wi-Fi**.

      > [!TIP]
      >
      > - For **Android Enterprise** devices running as a dedicated device (kiosk), choose **Fully Managed, Dedicated, and Corporate-Owned Work Profile** > **Wi-Fi**.
      > - For **Windows 8.1 and newer**, you can choose **Wi-Fi import**. This option lets you import Wi-Fi settings as an XML file that you previously exported from a different device.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later. For example, a good profile name is **WiFi profile for entire company**.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. Select **Next**.
7. In **Configuration settings**, depending on the platform you chose, the settings you can configure are different. Select your platform for detailed settings:

    - [Android device administrator](wi-fi-settings-android.md)
    - [Android (AOSP)](wi-fi-settings-android-aosp.md)
    - [Android Enterprise](wi-fi-settings-android-enterprise.md), including dedicated devices
    - [iOS/iPadOS](wi-fi-settings-ios.md)
    - [macOS](wi-fi-settings-macos.md)
    - [Windows 10/11](wi-fi-settings-windows.md)
    - [Windows 8.1 and newer](wi-fi-settings-import-windows-8-1.md), including Windows Holographic for Business

8. Select **Next**.
9. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, see [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

10. In **Assignments**, select the user or groups that will receive your profile. For more information on assigning profiles, see [Assign user and device profiles](device-profile-assign.md).

    Select **Next**.

11. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

> [!TIP]
> If you use certificate based authentication for your Wi-Fi profile, deploy the Wi-Fi profile, certificate profile, and trusted root profile to the same groups to ensure that each device can recognize the legitimacy of your certificate authority.  For more information, see [How to configure certificates with Microsoft Intune](../protect/certificates-configure.md).

## Next steps

The profile is created, but may not be doing anything. Be sure to [assign the profile](device-profile-assign.md), and [monitor its status.](device-profile-monitor.md).

[Troubleshoot Wi-Fi profiles in Intune](/troubleshoot/mem/intune/troubleshoot-wi-fi-profiles).
