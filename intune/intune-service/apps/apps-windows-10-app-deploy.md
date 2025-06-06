---
# required metadata

title: Windows app deployment by using Microsoft Intune
titleSuffix:
description: Learn about Windows 10/11 app deployment scenarios available with Microsoft Intune.
keywords:
author: nicholasswhite
ms.author: nwhite
manager: laurawi
ms.date: 04/16/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.assetid: abebfb5e-054b-435a-903d-d1c31767bcf2

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- Windows
- highpri
- FocusArea_Apps_Deploy
---

# Windows app deployment by using Microsoft Intune

Microsoft Intune supports a variety of app types and deployment scenarios on Windows 10 devices. After you've added an app to Intune, you can assign the app to users and devices. This article provides more details on the supported Windows scenarios, and also covers key details to note when you're deploying apps to Windows. For information about deploying an app, also known as assigning an app, see [Assign an app](../apps/apps-deploy.md#assign-an-app) to a group.

A Line-of-business (LOB) app is the app type supported on Windows 10 devices. The file extensions for Windows apps include .msi, .appx, and .appxbundle.

> [!NOTE]
> To deploy modern apps, you need at least:
>
> - For Windows 10 1803, [May 23, 2018—KB4100403 (OS Build 17134.81)](https://support.microsoft.com/help/4100403/windows-10-update-kb4100403).
> - For Windows 10 1709, [June 21, 2018—KB4284822 (OS Build 16299.522)](https://support.microsoft.com/help/4284822).
>
> Only Windows 10 1803 and later support installing apps when there is no primary user associated.
>
> LOB app deployment isn't supported on devices running Windows 10 Home editions.

## Supported Windows app types

Specific app types are supported based on the version of Windows 10 that your users are running. The following table provides the app type and Windows 10 supportability.

| App type | Home | Pro | Business | Enterprise | Education | S-Mode | HoloLens<sup>1 | Surface Hub |
|----------------|------|-----|----------|------------|-----------|--------|-----------|------------|
|  .MSI | No | Yes | Yes | Yes | Yes | No | No | No |
| .IntuneWin | No | Yes | Yes | Yes | Yes | 19H2+ | No | No |
| Office C2R | No | Yes | Yes | Yes | Yes | RS4+ | No | No |
| LOB: APPX/MSIX | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes |
| [Microsoft Store app (new)](store-apps-microsoft.md) | No | Yes | Yes | Yes | Yes | Yes | No | No |
| Web Apps | Yes | Yes | Yes | Yes | Yes | Yes | Yes<sup>2 | Yes<sup>2 |
| Store Link | Yes | Yes | Yes | Yes | Yes | Yes | Yes | Yes |
| Microsoft Edge | No | Yes | Yes | Yes | Yes | 19H2+<sup>3 | No | No |

<sup>1</sup> To unlock app management, upgrade your HoloLens device to [Holographic for Business](../fundamentals/windows-holographic-for-business.md).<br />
<sup>2</sup> Launch from the Company Portal only.<br />
<sup>3</sup> For Edge app to install successfully, devices must also be assigned an S-Mode policy.

> [!NOTE]
> All Windows app types require enrollment.

## Windows LOB apps

You can upload Windows LOB apps to the Microsoft Intune admin center. These can include modern apps, such as Universal Windows Platform (UWP) apps and Windows App Packages (AppX), as well as Win 32 apps, such as simple Microsoft Installer package files (MSI). The admin must manually upload and deploy updates of LOB apps. These updates are automatically installed on user devices that have installed the app. No user intervention is required, and the user has no control over the updates.

## Install apps on Windows devices

Depending on the app type, you can install the app on a Windows device in one of two ways:

- **User Context**: When an app is deployed in user context, the managed app is installed for that user on the device when the user signs in to the device. Note that the app installation doesn't succeed until the user signs in to the device.
  - Modern LOB apps and Microsoft Store apps can be deployed in user context. The apps support both the Required and Available intents.
  - Win32 apps built as User Mode or Dual Mode can be deployed in user context, and support both the Required and Available intents.
- **Device Context**: When an app is deployed in device context, the managed app is installed directly to the device by Intune.
  - Modern LOB can be deployed in device context. These apps only support the Required intent.
  - Win32 apps built as Machine Mode or Dual Mode and Microsoft Store apps can be deployed in device context, and support both the Required and Available intents.

> [!NOTE]
> For Win32 apps built as Dual Mode apps, the admin must choose if the app will install as a User Mode or Machine Mode app for all assignments associated with that instance. The deployment context can't be changed per assignment.

Apps can only be installed in the device context when supported by the device and the Intune app type. Device context installs are supported on Windows desktops and Teams devices, such as the Surface Hub. They aren't supported on devices running Windows Holographic for Business, such as the Microsoft HoloLens.

You can install the following app types in the device context and assign these apps to either a device or user group:

- Win32 apps
- LOB apps (MSI, APPX and MSIX)
- Microsoft 365 Apps for enterprise
- Microsoft Store apps

Windows LOB apps (specifically APPX and MSIX) that you've selected to install in device context must be assigned to a device group. The installation fails if one of these apps is deployed in the user context. The following status and error appears in the admin center:

- Status: Failed.
- Error: A user can't be targeted with a device context install.

> [!IMPORTANT]
> When used in combination with a Windows Autopilot pre-provisioning scenario, there is no requirement for LOB apps deployed in device context to target a device group. For more information, see [Windows Autopilot pre-provisioning deployment](/autopilot/pre-provision).

> [!NOTE]
> After you save an app assignment with a specific deployment, you can't change the context for that assignment, except for modern apps. For modern apps, you can change the context from user context to device context.

If there's a conflict in policies on a single user or device, the following priorities apply:

- A device context policy is a higher priority than a user context policy.
- An install policy is a higher priority than an uninstall policy.

For more information, see [Include and exclude app assignments in Microsoft Intune](apps-inc-exl-assignments.md). For more information about app types in Intune, see [Add apps to Microsoft Intune](apps-add.md).

## Next steps

- [Assign apps to groups with Microsoft Intune](apps-deploy.md)
- [How to monitor apps](apps-monitor.md)
