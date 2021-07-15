---
# required metadata
title: Manage device RDP redirections for Cloud PCs.
titleSuffix:
description: Learn how to Use the Windows 365 deployment checklist during your deployment.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 4/21/2021
ms.topic: reference
ms.service: cloudpc
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: chrimo
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection: 
---

# Manage RDP device redirections for Cloud PCs

Remote Desktop Protocol (RDP) can be used to create redirections that let users connect to peripherals (like cameras, USB drives, and printers) from remote devices like Cloud PCs. By default, these redirections are enabled for Cloud PCs. For security reasons, you might want to override the default and block these redirections.

There are two ways to manage RDP redirections:

- Use Microsoft Endpoint Manager
- Use Group Policy Objects (GPO)

## Use Microsoft Endpoint Manager to manage RDP device redirections

Screencaps to be added later.

1. Sign in to [Endpoint Manager portal](https://endpoint.microsoft.com) > **Devices** > **Configuration profiles** > **Create profile**.
2. In the **Create a profile** pane, select the following options:
    - **Platform**: Windows 10 and later
    - **Profile type**: Settings catalog (preview)
3. Select **Create**.
4. On the **Basics** tab of the **Create device configuration profile** page, type a **Name** and (optional) **Description** for the profile and then select **Next**.
5. On the **Configuration settings** tab, choose **Add settings**.
6. In the **Settings picker**, search for *Device and Resource Redirection*, and then select it in the results. This category is under Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Session Host\Device and Resource Redirection.
7. You'll see a list of settings. Choose **Select all these settings**.
8. If you want to manage printer redirection, search for *Printer Redirection* > select the category that ends with *Remote Desktop Session Host\Printer Redirection* > **Select all these settings**.
9. After you're done adding settings, select the **X** to exit the **Settings picker**.
10. If you want to remove any settings from the configuration profile, choose the minus icon next to the setting.
11. Select **Next**.
12. On the **Assignments** page, you can assign the profile to users or devices. Some settings from the Configuration settings have **(User)** or **(Device)** at the end of the setting. If you assign the configuration profile to a group of users, the device settings will not apply, and vice versa.
13. Select **Create** to create the configuration profile.

## Use GPO to manage RDP device redirections

To block any of the redirections, create and assign a Group Policy Object with the corresponding policies as shown in the table below. To learn more about the policies, download the [Group Policy Settings Reference Spreadsheet](https://www.microsoft.com/download/101451) :

| Redirection | Group policy |
| --- | --- |
| Audio input | Allow audio recording redirection |
| Audio output | Allow audio and video playback redirection |
| Cameras | Do not allow video capture redirection |
| Clipboard | Do not allow Clipboard redirection |
| Printers | Do not allow client printer redirection |
| COM ports | Do not allow COM port redirection |
| Drives | Do not allow drive redirection |
| Smartcards | Do not allow smart card device redirection |
| USB drives| Do not allow supported Plug and Play device redirection |

## Redirection support

The following table lists which peripherals are supported for redirection based on which platform is used to access the Cloud PC.

| Peripheral | Windows Remote Desktop client | Microsoft Store Remote Desktop client | Android | iOS/iPadOS | macOS | Web |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| Cameras | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) |
| Clipboard | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) (Text) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) (Text images) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) (Text) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) (Text) |
| Dynamic resolution | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) |
| Keyboard | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) |
| Local drive/storage | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) |
| Location | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) |
| Microphones |![Supported](./media/manage-rdp-device-restrictions/checkmark.png)  | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) |![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) |
| Mouse | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) |
| Multimedia | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) |
| Multi-monitor | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) (16 monitors) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) |
| Pen | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) (as Touch) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) (as Touch) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) |
| Printers | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) (CUPS only) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) (PDF print) |
| Scanners | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) |
| Screen capture protection | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) |
| Serial port | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) |
| Smart cards | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) (Windows sign in not supported) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) |
| Speakers | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) |
| Start menu integration | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) |
| Teams AV | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) |
| Touch | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) |
| USB | ![Supported](./media/manage-rdp-device-restrictions/checkmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) | ![Not supported](./media/manage-rdp-device-restrictions/xmark.png) |

<!-- ########################## -->
## Next steps

[Learn about apps in Windows 365](app-overview.md).
