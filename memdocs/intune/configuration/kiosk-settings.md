---
# required metadata

title: Kiosk settings for Windows and Holographic devices in Microsoft Intune - Azure | Microsoft Docs
description: Configure your Windows 10 (and later) and Windows Holographic for Business devices as single-app and multi-app kiosks, customize the start menu, add apps, show the task bar, and configure a web browser in Microsoft Intune. 
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 11/04/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
---

# Windows 10 and Windows Holographic for Business device settings to run as a dedicated kiosk using Intune

On Windows 10 devices, use Intune to run devices as a kiosk, sometimes known as a dedicated device. A device in kiosk mode can run one app, or run many apps. You can show and customize a start menu, add different apps, including Win32 apps, add a specific home page to a web browser, and more. 

This feature applies to devices running:

- Windows 10 and later
- Windows Holographic for Business

Intune supports one kiosk profile per device. If you need multiple kiosk profiles on a single device, you can use a [Custom OMA-URI](custom-settings-windows-10.md).

Intune uses "configuration profiles" to create and customize these settings for your organization's needs. After you add these features in a profile, push or deploy these settings to groups in your organization.

This article shows you how to create a device configuration profile. For a list of all the settings, and what they do, see [Windows 10 kiosk settings](kiosk-settings-windows.md) and [Windows Holographic for Business kiosk settings](kiosk-settings-holographic.md).

## Create the profile

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

   - **Name**: Enter a descriptive name for the new profile.
   - **Description**: Enter a description for the profile. This setting is optional, but recommended.
   - **Platform**: Select **Windows 10 and later**
   - **Profile type**: Select **Kiosk**

4. In **Settings**, select a **kiosk mode**. **Kiosk mode** identifies the type of kiosk mode supported by the policy. Options include:

    - **Not Configured** (default): The policy doesn't enable kiosk mode.
    - **Single app, full-screen kiosk**: The device runs as a single user account, and locks it to a single Store app. So when the user signs in, a specific app starts. This mode also restricts the user from opening new apps, or changing the running app.
    - **Multi app kiosk**: The device runs multiple Store apps, Win32 apps, or inbox Windows apps by using the Application User Model ID (AUMID). Only the apps you add are available on the device.

        The benefit of a multi-app kiosk, or fixed-purpose device, is to provide an easy-to-understand experience for users by only accessing apps they need. And, also removing from their view the apps they don’t need.

    For a list of all settings, and what they do, see:
      - [Windows 10 kiosk settings](kiosk-settings-windows.md)
      - [Windows Holographic for Business kiosk settings](kiosk-settings-holographic.md)

5. When you're done, select **OK** > **Create** to save your changes.

The profile is created, and shown in the profiles list. Next, [assign](device-profile-assign.md) the profile.

## Next steps

[Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).

You can create kiosk profiles for devices that run the following platforms:
- [Android](device-restrictions-android.md#kiosk)
- [Android Enterprise](device-restrictions-android-for-work.md#dedicated-device-settings)
- [Windows 10 and later](kiosk-settings-windows.md)
- [Windows Holographic for Business](kiosk-settings-holographic.md)
