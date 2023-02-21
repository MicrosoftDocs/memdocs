---
# required metadata

title: Kiosk settings for Windows Holographic for Business in Microsoft Intune
description: Configure your  Windows Holographic for Business devices as single-app and multi-app kiosks, customize the start menu, add apps, show the task bar, and configure a web browser in Microsoft Intune. 
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/19/2022
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
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
- tier3
- M365-identity-device-management
---

# Windows Holographic for Business device settings to run as a kiosk in Intune

On Windows Holographic for Business devices, you can configure these devices to run in single-app kiosk mode, or multi-app kiosk mode. Some features aren't supported on Windows Holographic for Business.

This article describes the different settings you can control on Windows Holographic for Business devices. As part of your mobile device management (MDM) solution, use these settings to configure your Windows Holographic for Business devices to run in kiosk mode.

As an Intune administrator, you can create and assign these settings to your devices.

To learn more about the Windows kiosk feature in Intune, see [configure kiosk settings](kiosk-settings.md).

## Before you begin

- [Create a Windows 10/11 kiosk device configuration profile](kiosk-settings.md#create-the-profile).

  When you create a Windows client kiosk device configuration profile, there are more settings than what's listed in this article. The settings in this article are supported on Windows Holographic for Business devices.

- This kiosk profile is directly related to the device restrictions profile you create using the [Microsoft Edge kiosk settings](device-restrictions-windows-holographic.md#microsoft-edge-browser). To summarize:

  1. Create this kiosk profile to run the device in kiosk mode.
  2. Create the [device restrictions profile](device-restrictions-windows-holographic.md#microsoft-edge-browser), and configure specific features and settings allowed in Microsoft Edge.

> [!IMPORTANT]
> Be sure to assign this kiosk profile to the same devices as your [Microsoft Edge profile](device-restrictions-windows-holographic.md#microsoft-edge-browser).

## Single app, full-screen kiosk

Runs only one app on the device. When the user signs in, a specific app starts. This mode also restricts the user from opening new apps, or changing the running app.

- **User logon type**: Select the account type that runs the app. Your options:

  - **Auto logon (Windows 10 version 1803 and newer)**: Not supported on Windows Holographic for Business.
  - **Local user account**: Enter the local (to the device) user account. Or, enter a Microsoft Account (MSA) account associated with the kiosk app. The account you enter signs in to the kiosk.

    For kiosks in public-facing environments, a user type with the least privilege should be used.

- **Application type**: Select **Add Store app**.

  - **App to run in kiosk mode**: Select an app from the list.

    Don't have any apps listed? Add some using the steps at [Client Apps](../apps/apps-add.md).

## Multi-app kiosk

Apps in this mode are available on the start menu. These apps are the only apps the user can open. If an app has a dependency on another app, both must be included in the allowed apps list.

- **Target Windows 10 in S mode devices**: Select **No**. S mode isn't supported on Windows Holographic for Business.

- **User logon type**: Add one or more user accounts that can use the apps you add. Your options:

  - **Auto logon (Windows 10 version 1803 and newer)**: Not supported on Windows Holographic for Business.
  - **Local user accounts**: **Add** the local (to the device) user account. The account you enter signs in to the kiosk.
  - **Azure AD user or group (Windows 10, version 1803 and later)**: Requires user credentials to sign in to the device. Select **Add** to choose Azure AD users or groups from the list. You can select multiple users and groups. Choose **Select** to save your changes.
  - **HoloLens visitor**: The visitor account is a guest account that doesn't require any user credentials or authentication, as described in [shared PC mode concepts](/windows/configuration/set-up-shared-or-guest-pc#shared-pc-mode-concepts).

- **Browser and Applications**: Add the apps to run on the kiosk device. Remember, you can add several apps.

  - **Browsers**
    - **Add Microsoft Edge**: Microsoft Edge is added to the app grid, and all applications can run on this kiosk. Select the Microsoft Edge kiosk mode type:

      - **Normal mode (full version of Microsoft Edge)**: Runs a full-version of Microsoft Edge with all browsing features. User data and state are saved between sessions.
      - **Public browsing (InPrivate)**: Runs a multi-tab version of Microsoft Edge InPrivate with a tailored experience for kiosks that run in full-screen mode.

      For more information on these options, see [Deploy Microsoft Edge kiosk mode](/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types).

      > [!NOTE]
      > This setting enables the Microsoft Edge browser on the device. To configure Microsoft Edge-specific settings, create a device restrictions profile (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10** for platform > **Device Restrictions** > **Microsoft Edge Browser**). [Microsoft Edge browser](device-restrictions-windows-holographic.md#microsoft-edge-browser) describes the available Holographic for Business settings.

    - **Add Kiosk browser**: Not supported on Windows Holographic for Business.

  - **Applications**
    - **Add store app**: Select an existing app you added or deployed to Intune as [Client Apps](../apps/apps-add.md), including LOB apps. If you don't have any apps listed, Intune supports many [app types](../apps/apps-add.md) that you [add to Intune](../apps/store-apps-windows.md).
    - **Add Win32 app**: Not supported on Windows Holographic for Business.
    - **Add by AUMID**: Use this option to add inbox Windows apps, such as Notepad or Calculator. Enter the following properties:

      - **Application name**: Required. Enter a name for the application.
      - **Application user model ID (AUMID)**: Required. Enter the Application user model ID (AUMID) of the Windows app. To get this ID, see [find the Application User Model ID of an installed app](/windows-hardware/customize/enterprise/find-the-application-user-model-id-of-an-installed-app).

    - **AutoLaunch**: Optional. After you add your apps and browser, select one app or browser to automatically open when the user signs in. Only a single app or browser can be autolaunched.
    - **Tile size**: Required. After you add your apps, select a Small, Medium, Wide, or Large app tile size.

- **Use alternative Start layout**: Select **Yes** to enter an XML file that describes how the apps appear on the start menu, including the order of the apps. Use this option if you require more customization in your start menu. [Customize and export start layout](/hololens/hololens-kiosk#start-layout-for-hololens) provides some guidance, and includes a specific XML file for Windows Holographic for Business devices.

- **Windows Taskbar**: Not supported on Windows Holographic for Business.
- **Allow Access to Downloads Folder**: Not supported on Windows Holographic for Business.
- **Specify Maintenance Window for App Restarts**: Not supported on Windows Holographic for Business.

## Next steps

[Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).

You can also create kiosk profiles for [Android](device-restrictions-android.md#kiosk), [Android Enterprise](device-restrictions-android-for-work.md#device-experience), and [Windows 10/11](kiosk-settings-windows.md) devices.
