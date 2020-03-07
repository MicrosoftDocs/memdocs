---
# required metadata

title: Add or configure education settings in Microsoft Intune - Azure | Microsoft Docs
description: Use the Take a Test app in a device configuration profile on Windows 10 and later devices in Microsoft Intune. Create a configuration profile using the Education settings, and enter a test app URL, choose how users sign-in, monitor the screen during the test, and allow or prevent text suggestions during the test.
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 11/04/2019
ms.topic: conceptual
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

- Windows 10 and later

When the user signs in, the Take a Test app automatically opens with the test you entered. No other apps can run on the device while the test is in progress. [Take tests in Windows 10](https://docs.microsoft.com/education/windows/take-tests-in-windows-10) provides more details on the Take a Test app.

This article lists the steps to create a device configuration profile  in Microsoft Intune. It also includes information to read and learn about the available education settings for your Windows 10 devices.

## Create a device profile

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Name**: Enter a descriptive name for the new profile.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.
    - **Platform**: Choose **Windows 10 and later**.
    - **Profile**: Choose **Education profile**.

4. Enter the settings you want to configure:

    - [Windows 10 and later](education-settings-windows.md)

5. Select **OK** > **Create** to save your changes.

After you enter your settings, and create the profile, your profile is shown in the profiles list. Next, [assign this profile to some groups](device-profile-assign.md).

## Next steps

See a list of the [Windows 10 education settings](education-settings-windows.md) and their descriptions.

[Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).
