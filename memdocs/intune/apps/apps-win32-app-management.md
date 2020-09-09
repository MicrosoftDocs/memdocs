---
title: Win32 app management in Microsoft Intune
titleSuffix:
description: Learn how to manage Win32 apps with Microsoft Intune. This topic provides an overview of the Intune Win32 app delivery and management capabilities. 
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/09/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology:
ms.assetid: efdc196b-38f3-4678-ae16-cdec4303f8d2

ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Win32 app management in Microsoft Intune

Microsoft Intune allows Win32 app management capabilities. While it is possible for cloud connected customers to use Configuration Manager for Win32 app management, Intune-only customers will have greater management capabilities for their Win32 line-of-business (LOB) apps. This topic provides an overview of the Intune Win32 app management features and related information.

> [!NOTE]
> This app management capability supports both 32-bit and 64-bit operating system architecture for Windows applications.

> [!IMPORTANT]
> When deploying Win32 apps, consider using the [Intune Management Extension](../apps/intune-management-extension.md) approach exclusively, particularly when you have a multi-file Win32 app installer. If you mix the installation of Win32 apps and line-of-business apps during AutoPilot enrollment, the app installation may fail. The Intune management extension is installed automatically when a PowerShell script or Win32 app is assigned to the user or device.

## Prerequisites

To use Win32 app management, be sure you meet the following criteria:

- Windows 10 version 1607 or later (Enterprise, Pro, and Education versions)
- Windows 10 client needs to be: 
  - Devices must be joined to Azure AD and auto-enrolled. The Intune management extension supports Azure AD joined, hybrid domain joined, group policy enrolled devices are supported. 
  > [!NOTE]
  > For the group policy enrolled scenario - The end user uses the local user account to AAD join their Windows 10 device. The user must log onto the device using their AAD user account and enroll into Intune. Intune will install the Intune Management extension on the device if a PowerShell script or a Win32 app is targeted to the user or device.
- Windows application size is capped at 8 GB per app.

## Prepare the Win32 app content for upload

Use the [Microsoft Win32 Content Prep Tool](https://go.microsoft.com/fwlink/?linkid=2065730) to pre-process Windows Classic (Win32) apps. The tool converts application installation files into the *.intunewin* format. For more information and steps, see [Prepare Win32 app content for upload](apps-win32-prepare.md). 

## Add, assign, and monitor a Win32 app

After you have [prepared a Win32 app to be upload to Intune](apps-win32-prepare.md) using the [Microsoft Win32 Content Prep Tool](https://go.microsoft.com/fwlink/?linkid=2065730), you can add the app to Intune. For more information and steps, see [Add, assign, and monitor a Win32 app in Microsoft Intune](apps-win32-add.md).

## Delivery Optimization

Windows 10 1709 and above clients will download Intune Win32 app content using a delivery optimization component on the Windows 10 client. Delivery optimization provides peer-to-peer functionality that it is turned on by default. You can configure the Delivery Optimization agent to download Win32 app content either in background or foreground mode based on assignment. Delivery optimization can be configured by group policy and via Intune Device configuration. For more information, see [Delivery Optimization for Windows 10](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization). 

> [!NOTE]
> You can also install a Microsoft Connected Cache server on your Configuration Manager distribution points to cache Intune Win32 app content. For more information, see [Microsoft Connected Cache in Configuration Manager - Support for Intune Win32 apps](https://docs.microsoft.com/configmgr/core/plan-design/hierarchy/microsoft-connected-cache#bkmk_intune).

## Install required and available apps on devices

The end user will see Windows Toast Notifications for the required and available app installations. The following image shows an example toast notification where the app installation is not complete until the device is restarted. 

![Screenshot of Windows toast notifications for an app installation](./media/apps-win32-app-management/apps-win32-app-08.png)    

The following image notifies the end user that app changes are being made to the device.

![Screenshot notifying the user that app changes are being made](./media/apps-win32-app-management/apps-win32-app-09.png)    

Additionally, the Company Portal app shows additional app installation status messages to end users. The following conditions apply to Win32 dependency features:
- App failed to install. Dependencies defined by the admin were not met.
- App installed successfully but requires a restart.
- App is in the process of installing, but requires a restart to continue.

## Set Win32 app availability and notifications
You can configure the start time and deadline time for a Win32 app. At the start time, Intune management extension will start the app content download and cache it for required intent. The app will be installed at the deadline time. For available apps, start time will dictate when the app is visible in the Company Portal and content will be downloaded when the end user requests the app from the Company Portal. Additionally, you can enable a restart grace period. 

> [!IMPORTANT]
> The **Restart grace period** setting in the **Assignment** section is only available when the **Device restart behavior** of the **Program** section is set to either of the following options:
> - **Determine behavior based on return codes**
> - **Intune will force a mandatory device restart**

Set the app availability based on a date and time for a required app using the following steps:

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All apps**.
3. Select an existing **Windows app (Win32)** from the list. 
4. From the app pane, select **Properties** > **Edit** next to the **Assignments** section > **Add group** below the **Required** assignment type. 
   Note that app availability can be set based on the assignment type. The **Assignment type** can be **Required**, **Available for enrolled devices**, or **Uninstall**.
5. Select a group in the **Select group** pane to specify which group of users will be assigned the app. 

    > [!NOTE]
    > **Assignment type** options included the following:<br>
    > - **Required**: You can choose to **make this app required for all users** and/or **make this app required on all devices**.<br>
    > - **Available for enrolled devices**: You can choose to **make Make this app available to all users with enrolled devices**.<br>
    > - **Uninstall**: You can choose to ***uninstall this app for all users** and/or **uninstall this app for all devices**.

6. To modify the **End user notification** options select **Show all toast notifications**.
7. In the **Edit assignment** pane, set the **Ender user notifications** to **Show all toast notifications**. Note that you can set **End user notifications** to **Show all toast notifications**, **Show toast notifications for computer restarts**, or **Hide all toast notifications**.
8. Set the **App availability** to **A specific date and time** and select your date and time. This date and time specifies when the app is downloaded to the end users device. 
9. Set the **App installation deadline** to **A specific date and time** and select your date and time. This date and time specifies when the app is installed on the end users device. When more than one assignment is made for the same user or device, the app installation deadline time is picked based on the earliest time possible.

10. Click **Enabled** next to the **Restart grace period**. The restart grace period starts as soon as the app install has been completed on the device.​ When disabled, the device can restart without warning. <br>You can customize the following options:
    - **Device restart grace period (minutes)**: The default value is 1440 minutes (24 hours). This value can be a maximum of 2 weeks.
    - **Select when to display the restart countdown dialog box before the restart occurs (minutes)**: The default value is 15 minutes.
    - **Allow user to snooze the restart notification**: You can choose **Yes** or **No**.
        - **Select the snooze duration (minutes)**: The default value is 240 minutes (4 hours). The snooze value cannot be more than reboot grace period.

11. Click **Review + save**.

## Toast notifications for Win32 apps 
If needed, you can suppress showing end user toast notifications per app assignment. From Intune, select **Apps** > **All apps** > select the app > **Assignments** > **Include Groups**. 

> [!NOTE]
> Intune management extension installed Win32 apps will not be uninstalled on unenrolled devices. Admins can leverage assignment exclusion to not offer Win32 apps to BYOD Devices.

## Next steps

- For more information about adding apps to Intune, see [Add apps to Microsoft Intune](apps-add.md).
