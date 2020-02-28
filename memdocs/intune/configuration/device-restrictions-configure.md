---
# required metadata

title: Restrict devices features using policy in Microsoft Intune - Azure | Microsoft Docs
description: Add a device profile to restrict features on Android, macOS, iOS, iPadOS, Windows Phone, and Windows 10 devices in Microsoft Intune
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---
 
# Configure device restriction settings in Microsoft Intune



Intune includes device restriction policies that help administrators control Android, iOS/iPadOS, macOS, and Windows devices. These restrictions let you control a wide range of settings and features to protect your organization's resources. For example, administrators can:

- Allow or block the device camera
- Control access to Google Play, app stores, viewing documents, and gaming
- Block built-in apps, or create a list of apps that allowed or prohibited
- Allow or prevent backing up files to cloud and storage accounts
- Set a minimum password length, and block simple passwords

These features are available in Intune, and are configurable by the administrator. Intune uses "configuration profiles" to create and customize these settings for your organization's needs. After you add these features in a profile, you can then push or deploy the profile to devices in your organization.

This article shows you how to create a device restrictions profile. You can also see all the available settings for the different platforms.

## Create the profile

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, a good policy name is **iOS/iPadOS: Block camera on devices**.
    - **Description**: Enter a description for the policy. This setting is optional, but recommended.
    - **Platform**: Choose the platform of your devices. Your options:  

        - **Android**
        - **Android enterprise**
        - **iOS/iPadOS**
        - **macOS**
        - **Windows Phone 8.1**
        - **Windows 8.1 and later**
        - **Windows 10 and later**

    - **Profile type**: Select **Device restrictions**.

        To create a device restrictions profile for Windows 10 Team devices, such as Surface Hub, then choose **Device restrictions (Windows 10 Team)**.

4. Depending on the platform you chose, the settings you can configure are different. Choose your platform for detailed settings:

    - [Android settings](../device-restrictions-android.md)
    - [Android enterprise settings](../device-restrictions-android-for-work.md)
    - [iOS/iPadOS settings](device-restrictions-ios.md)
    - [macOS settings](device-restrictions-macos.md)
    - [Windows Phone 8.1 settings](device-restrictions-windows-phone-8-1.md)
    - [Windows 8.1](device-restrictions-windows-8-1.md)
    - [Windows 10 settings](device-restrictions-windows-10.md)
    - [Windows 10 Team settings](device-restrictions-windows-10-teams.md)
    - [Windows Holographic for Business settings](device-restrictions-windows-holographic.md)

5. When you're done, select **OK** > **Create** to save your changes.

The profile is created and shown on the profiles list.

## Next steps

After the profile is created, it's ready to be assigned. Next, [assign the profile](../device-profile-assign.md) and [monitor its status](../device-profile-monitor.md).

<!--  Removing image as part of design review; retaining source until we known the disposition.

## Example of device restriction settings

In this high-level example, you'll create a device restriction policy that blocks the use of the built-in camera app on Android devices.

![How to disable the camera on Android devices](./media/device-restrictions-configure/disable-android-camera.png)

-->
