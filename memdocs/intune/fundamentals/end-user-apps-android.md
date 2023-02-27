---
# required metadata

title: How your Android users get their apps 
description: Methods for making Android apps available to end users
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: f33d1684-b1b5-44f7-9aac-c6d5186a5d7c

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic
ms.collection:
- tier2
- M365-identity-device-management
---


# How your Android users get their apps  

This article helps you understand how and where your Android device administrator end users get the apps that you distribute through Microsoft Intune. The information can vary by device type (native Android devices or Samsung Knox Standard devices).

## Native (non-Samsung Knox Standard) Android devices   

| App type | Line-of-business (LOB) apps | Play Store apps  |
| ------------- |-------------| -----|
| Available apps      | Users tap **install** in the Company Portal. A notification appears, which users then tap to start the installation. After the installation is successful, the notification disappears. | Users tap the app in the Company Portal, and are taken to an app page in the Play Store. This is where they start the installation.|
| Required apps      | Users are shown a notification, which they can't dismiss, indicating that they need to install an app. Users tap the notification to start the installation. After the installation is successful, the notification disappears.    | Users are shown a notification, which they can't dismiss, indicating that they need to install an app. Users tap the notification and are taken to an app page in the Play Store. This is where they start the installation. After the installation is successful, the notification disappears. |

Your end users need to allow installation from unknown sources to install [LOB apps](../apps/lob-apps-android.md). This setting is normally found in two different places, depending on the version of Android:

* Android 7.1.2 and lower: **Settings** > **Security** > **Unknown sources**
* Android 8.0 and above: **Settings** > **Apps & notifications** > **Special app access** > **Install unknown apps** > **Company Portal** > **Allow from this source**

If this occurs, the Company Portal app will inform and directly guide the end user to the appropriate setting. 

## Samsung Knox Standard Android devices

| App type | Line-of-business (LOB) apps | Play Store apps  |
| ------------- |-------------| -----|
| Available apps      | Users tap **install** in the Company Portal. The app installs without further user intervention. | Users tap the app in the Company Portal and are taken to an app page in the Play Store. This is where they start the installation.|
| Required apps      | The app is installed without any user intervention.    | Users are shown a notification, which they can't dismiss, indicating that they need to install an app. Users tap the notification and are taken to an app page in the Play Store. This is where they start the installation. After the installation is successful, the notification disappears. |

Apps can be managed or unmanaged, as described below. The process of making apps managed is the same for all types of Android devices.

* Managed apps: These apps are managed through policies. They've been "wrapped" by Intune or built with the Intune App SDK. These apps can be managed by Intune, and application policies can be applied to them.

* Unmanaged apps: These apps aren't managed through policies. They have not been wrapped by Intune or don't incorporate the Intune App SDK. Application policies can't be applied to these apps.

## Zebra devices with Zebra Mobility Extensions

Intune uses the Zebra Mobility Extensions (MX) toolkit to silently install apps on Zebra devices managed by device administrator. This feature allows you to deploy and update apps on Zebra devices without user intervention. If the MX version on your device is 4.2 or older, then apps aren't installed silently. For more information, see [Full MX Feature Matrix](http://techdocs.zebra.com/mx/compatibility/) on Zebra's web site.

LOB apps deployed to Zebra devices must be installed from a public location on the device. The .apk app package may be accessible to other apps and services that also have access to public storage on the device. Typically, this access is a small window between the app download completing, and at the beginning of installation. This window may allow for a timing attack. For example, an .apk package could be changed during this window. Intune minimizes the amount of time that the .apk spends in public storage, and doesn't allow unsigned apps to install. To help minimize the security risk, be sure that the .apk files you upload don't contain sensitive information.

## See also

[Add apps with Microsoft Intune](../apps/apps-add.md)

[How your iOS/iPadOS users get their apps](end-user-apps-ios.md)

[How your Windows users get their apps](end-user-apps-windows.md)
