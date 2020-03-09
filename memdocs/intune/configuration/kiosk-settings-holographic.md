---
# required metadata

title: Kiosk settings for Windows Holographic for Business in Microsoft Intune - Azure | Microsoft Docs
description: Configure your  Windows Holographic for Business devices as single-app and multi-app kiosks, customize the start menu, add apps, show the task bar, and configure a web browser in Microsoft Intune. 
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/18/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
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

# Windows Holographic for Business device settings to run as a kiosk in Intune

On Windows Holographic for Business devices, you can configure these devices to run in single-app kiosk mode, or multi-app kiosk mode. Some features aren't supported on Windows Holographic for Business.

This article lists and describes the different settings you can control on Windows Holographic for Business devices. As part of your mobile device management (MDM) solution, use these settings to configure your Windows Holographic for Business devices to run in kiosk mode.

As an Intune administrator, you can create and assign these settings to your devices.

To learn more about the Windows kiosk feature in Intune, see [configure kiosk settings](kiosk-settings.md).

## Before you begin

[Create the profile](kiosk-settings.md#create-the-profile).

## Single full-screen app kiosks

When you choose single app kiosk mode, enter the following settings:

- **User logon type**: Select **Local user account** to enter the local (to the device) user account, or a Microsoft Account (MSA) account associated with the kiosk app. **Autologon** user account types aren't supported on Windows Holographic for Business.

- **Application type**: Select **Store app**.

- **App to run in kiosk mode**: Choose **Add a store app**, and select an app from the list.

    Don't have any apps listed? Add some using the steps at [Client Apps](../apps/apps-add.md).

    Select **OK** to save your changes.

## Multi-app kiosks

Apps in this mode are available on the start menu. These apps are the only apps the user can open. When you choose multi app kiosk mode, enter the following settings:

- **Target Windows 10 in S mode devices**: Choose **No**. S mode isn't supported on Windows Holographic for Business.

- **User logon type**: Add one or more user accounts that can use the apps you add. Your options: 

  - **Auto logon**: Not supported on Windows Holographic for Business.
  - **Local user accounts**: **Add** the local (to the device) user account. The account you enter is used to sign in to the kiosk.
  - **Azure AD user or group (Windows 10, version 1803 and later)**: Requires user credentials to sign in to the device. Select **Add** to choose Azure AD users or groups from the list. You can select multiple users and groups. Choose **Select** to save your changes.
  - **HoloLens visitor**: The visitor account is a guest account that doesn't require any user credentials or authentication, as described in [shared PC mode concepts](https://docs.microsoft.com/windows/configuration/set-up-shared-or-guest-pc#shared-pc-mode-concepts).

- **Applications**: Add the apps to run on the kiosk device. Remember, you can add several apps.

  - **Add Store apps**: Select an existing app you added or deployed to Intune as [Client Apps](../apps/apps-add.md), including LOB apps. If you don't have any apps listed, Intune supports many [app types](../apps/apps-add.md) that you [add to Intune](../apps/store-apps-windows.md).
  - **Add Win32 app**: Not supported on Windows Holographic for Business.
  - **Add by AUMID**: Use this option to add inbox Windows apps. Enter the following properties: 

    - **Application name**: Required. Enter a name for the application.
    - **Application user model ID (AUMID)**: Required. Enter the Application user model ID (AUMID) of the Windows app. To get this ID, see [find the Application User Model ID of an installed app](https://docs.microsoft.com/windows-hardware/customize/enterprise/find-the-application-user-model-id-of-an-installed-app).
    - **Tile size**: Required. Choose a Small, Medium, Wide, or Large app tile size.

- **Kiosk browser settings**: Not supported on Windows Holographic for Business.

- **Use alternative Start layout**: Choose **Yes** to enter an XML file that describes how the apps appear on the start menu, including the order of the apps. Use this option if you require more customization in your start menu. [Customize and export start layout](https://docs.microsoft.com/hololens/hololens-kiosk#start-layout-for-hololens) provides some guidance, and includes a specific XML file for Windows Holographic for Business devices.

- **Windows Taskbar**: Not supported on Windows Holographic for Business.

## Next steps

[Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).

You can also create kiosk profiles for [Android](device-restrictions-android.md#kiosk), [Android Enterprise](device-restrictions-android-for-work.md#dedicated-device-settings), and [Windows 10 and later](kiosk-settings-windows.md) devices.
