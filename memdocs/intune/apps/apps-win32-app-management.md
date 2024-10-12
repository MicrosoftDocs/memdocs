---
title: Win32 app management in Microsoft Intune
description: Learn how to manage Win32 apps with Microsoft Intune. This article provides an overview of the Intune Win32 app delivery and management capabilities.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/09/2024
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.assetid: efdc196b-38f3-4678-ae16-cdec4303f8d2

ms.reviewer: bryanke
ms.suite: ems
search.appverid: MET150
ai-usage: ai-assisted
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- FocusArea_Apps_Win32
---

# Win32 app management in Microsoft Intune

Microsoft Intune enables Windows Win32 app management. Win32 app management in Intune allows you to install, configure, protect, and monitor your Windows applications on devices at your organization. Win32 apps are deployed using the Microsoft Intune management extension (IME), which is installed automatically when a PowerShell script or a Win32 app is assigned to the user or device using Intune.

In addition to supporting extensive management capabilities, Win32 app management in Microsoft Intune provides support for the following capabilities:
- Management of large traditional desktop apps 
- Support for several app types
- Control for complex app installations
- Support for detection rules, dependencies, and requirements
- Support for 32-bit and 64-bit Windows operating system architecture
- Support for Windows S mode devices

Although it's possible for cloud-connected customers to use Microsoft Configuration Manager for Windows app management, Intune-only customers have greater management capabilities for their Win32 apps. This article provides an overview of the Intune Win32 app management features and related information.

> [!NOTE]
> For information about Enterprise App Catalog apps, see [Add an Enterprise App Catalog app (Win32) to Microsoft Intune](../apps/apps-add-enterprise-app.md).

> [!IMPORTANT]
> When you're deploying Windows Win32 apps, consider using the Win32 app type in Intune exclusively, particularly when you have a multiple-file Win32 app installer. If you mix the installation of Win32 apps and line-of-business apps during Windows Autopilot enrollment, the app installation might fail as they both may attempt to use the Trusted Installer service at the same time which causes a failure due to this conflict. However, mixing of Win32 and line-of-business apps during Windows Autopilot device preparation is supported.

## Prerequisites

To use Win32 app management, be sure the following criteria are met:

- Use Windows 10 version 1607 or later (Enterprise, Pro, or Education editions).
- Devices must be enrolled in Intune and either:
  - [Microsoft Entra registered](/azure/active-directory/devices/concept-azure-ad-register)
  - [Microsoft Entra joined](/azure/active-directory/devices/concept-azure-ad-join)
  - [Microsoft Entra hybrid joined](/azure/active-directory/devices/concept-azure-ad-join-hybrid)
- Windows application size must not be greater than 30 GB per app.

  > [!NOTE]
  >
  > The [Microsoft Intune management extension (IME)](../apps/intune-management-extension.md) provides Intune's Win32 app type capabilities on managed clients. It is installed automatically when a PowerShell script or Win32 app is assigned to the user or device. Additionally, the Intune management extension agent checks every hour (or on service or device restart) for any new Win32 app assignments.

## Prepare the Win32 app content for upload

Before you can add a Win32 app to Microsoft Intune, you must prepare the app by using the Microsoft Win32 Content Prep Tool. You use the Microsoft Win32 Content Prep Tool to preprocess Windows classic (Win32) apps. The tool converts application installation files into the *.intunewin* format. For more information and steps, see [Prepare Win32 app content for upload](apps-win32-prepare.md).

## Add, assign, and monitor a Win32 app

After you have [prepared a Win32 app to be uploaded to Intune](apps-win32-prepare.md) by using the Microsoft Win32 Content Prep Tool, you can add the app to Intune. For more information and steps, see [Add, assign, and monitor a Win32 app in Microsoft Intune](apps-win32-add.md).

> [!NOTE]
> Windows application size is limited to 30 GB per app.

## Delivery optimization

Windows 10 1709 and later clients will download Intune Win32 app content by using the delivery optimization component of Windows. Delivery optimization provides peer-to-peer functionality that's turned on by default.

You can configure Delivery Optimization to download Win32 app content in either background or foreground mode based on assignment. Delivery optimization can be configured using Intune device configuration (or by group policy). For more information, see [Delivery Optimization for Windows 10](/windows/deployment/update/waas-delivery-optimization).

> [!NOTE]
> You can also install a Microsoft Connected Cache server on your Configuration Manager distribution points to cache delivery optimization aware content like Intune Win32 app content. For more information, see [Microsoft Connected Cache in Configuration Manager](/configmgr/core/plan-design/hierarchy/microsoft-connected-cache#bkmk_intune).

## Install required and available apps on devices

The user will see Windows notifications for the required and available app installations. The following image shows an example notification where the app installation is not complete until the device is restarted.

![Screenshot of Windows notifications for an app installation.](./media/apps-win32-app-management/apps-win32-app-08.png)

The following image notifies the user that app changes are being made to the device.

![Screenshot notifying the user that app changes are being made.](./media/apps-win32-app-management/apps-win32-app-09.png)

Additionally, the Company Portal app shows more app installation status messages to users. The following conditions apply to Win32 dependency features:

- App failed to be installed. Dependencies defined by the admin were not met.
- App was installed successfully but requires a restart.
- App is in the process of being installed but requires a restart to continue.

## Set Win32 app availability and notifications

You can configure the start time and deadline time for a Win32 app. At the start time, the Intune management extension will start the app content download and cache it for the required intent. The app will be installed at the deadline time.

For available apps, the start time will dictate when the app is visible in the company portal, and content will be downloaded when the user requests the app from the company portal. You can also enable a restart grace period.

On a device where a Win32 app with grace period settings has been deployed, low-rights users with non-administrative privileges can interact with the grace period UX. Admins on the device are also able to interact with the grace period UX on the device.

> [!IMPORTANT]
> The **Restart grace period** setting in the **Assignment** section is available only when **Device restart behavior** of the **Program** section is set to either of the following options:
>
> - **Determine behavior based on return codes** - Commonly set to Hard Reboot, however if return code is mapped to Soft Reboot, the user will only get a reboot notification and restart grace period settings will not be applied.
> - **Intune will force a mandatory device restart**
>
> Win32 apps installed by Intune on a managed device won't be automatically uninstalled from that device if it is unenrolled from Intune management. Admins should restrict app assignment and installation to corporate managed devices to reduce the risk of applications and data becoming unmanaged.

Set the app availability and other app assignment properties using the following steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All apps** or **Apps** > **Windows**.
3. Select an app from the list with **Windows app (Win32)** as its **Type**.
4. From the app pane, select **Properties** and then **Edit** next to the **Assignments** section. Then select **Add group**, **Add all users**, or **Add all devices** below one of the assignment types.

    **Assignment type** options include the following:

    - **Required**
    - **Available for enrolled devices**
    - **Uninstall**

    > [!NOTE]
    > Win32 apps installed using the **Available for enrolled devices** assignment will not be automatically reinstalled by Intune if they are uninstalled from a device in any way.

5. If **Add group** was used, select a group on the **Select groups** pane to specify which groups will be assigned the app.
6. To modify additional properties of the assignment, select the corresponding text under one of the assignment headings, including **Group mode**, **End user notifications**, **Availability**, **Installation deadline**, **Restart grace period**, or **Delivery optimization priority**.
7. In the **Edit assignment** pane, you can set the following properties:
    - **Mode** to **Include** or **Exclude**
    - **End user notifications** to one of the following options:
      - **Show all toast notifications**
      - **Show toast notifications for computer restarts**
      - **Hide all toast notifications**.
    - **Time zone** to **UTC** or **Device time zone**
    - **App availability** to **As soon as possible** or **A specific date and time** and specify your date and time. This date and time specify when the app is downloaded to the user's device.
    - **App installation deadline** to **As soon as possible** or **A specific date and time** and select your date and time. This date and time specify when the app is installed on the targeted device. When more than one assignment is made for the same user or device, the app installation deadline time is picked based on the earliest time possible.
      
      > [!NOTE]
      > If a win32 app is configured with a deadline to install, it will be downloaded but it won't install until the deadline. The Company Portal does not provide this level of detail. The Company Portal will show an **Installing** status for the app as soon as it is downloaded. Once the app is installed, the Company Portal will show the app installation status as **Installed**. The time between showing an **Installing** status verses an **Installed** status depends on the configuration for the deadline in Intune.

    - **Restart grace period** to **Enabled** or **Disabled**. The restart grace period starts as soon as the app installation has finished on the device. When the setting is disabled, the device can restart without warning.

      You can customize the following options:

      - **Device restart grace period (minutes)**: The default value is 1,440 minutes (24 hours). This value can be a maximum of 2 weeks.
      - **Select when to display the restart countdown dialog box before the restart occurs (minutes)**: The default value is 15 minutes.
      - **Allow user to snooze the restart notification**: You can choose **Yes** or **No**.
        - **Select the snooze duration (minutes)**: The default value is 240 minutes (4 hours). The snooze value can't be more than the reboot grace period.

      > [!IMPORTANT]
      > The **Restart grace period** assignment setting is available only when **Device restart behavior** in the **Program** section of the app is set to either of the following options:
      >
      > - **Determine behavior based on return codes**
      > - **Intune will force a mandatory device restart**

8. Select **Review + save**.

## Notifications for Win32 apps

If needed, you can suppress showing user notifications per app assignment. Follow the steps above and choose either **Show toast notifications for computer restarts** or **Hide all toast notifications** for the **End user notifications** option in the **Edit assignment** pane based on the level of notification suppression that you require.

## Next steps

- For more information about adding apps to Intune, see [Add apps to Microsoft Intune](apps-add.md).
