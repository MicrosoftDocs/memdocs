---
# required metadata

title: How your iOS/iPadOS users get their apps 
description: Methods for making iOS/iPadOS apps available to end users
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/01/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: 7e3135c1-df26-48c9-aa4c-cdab6168897a

# optional metadata

#ROBOTS:
#audience:

ms.reviewer:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic
ms.collection:
- tier2
- M365-identity-device-management
---


# How your iOS/iPadOS users get their apps

Use this information to understand how and where your end users get the apps that you distribute through Microsoft Intune.

**Required apps**: Apps that are required by the admin and that are installed on the device with minimal user involvement, depending on the platform.

**Available apps**: Apps that are provided in the Company Portal app list and that a user may optionally choose to install.

**Managed apps**: Apps that can be managed through policies and that have been "wrapped" by Intune or have been built with the Intune App Software Development Kit (SDK). These apps can be managed by Intune, and app protection policies can be applied to them.

**Unmanaged apps**: Apps that users can download from the iOS/iPadOS App Store that aren't integrated with the Intune app SDK. Intune doesn't have any control over the distribution, management, or selective wipe of these apps.  

Enrolled users get their apps by tapping on the following tiles on the Apps screen of the Company Portal app:

- **All Apps** points to a list of all apps in the ALL tab of the [Company Portal website](https://portal.manage.microsoft.com).

- **Featured Apps** take users to the FEATURED tab of the Company Portal website.

- **Categories** points to the CATEGORIES tab of the Company Portal website.

:::image type="content" source="./media/end-user-apps-ios/ios-cp-app-main-apps-screen.png" alt-text="iOS Company Portal apps screen.":::

For information on how to add apps, see [How to add an app to Microsoft Intune](../apps/apps-add.md).

## App management takeover
If an app is already installed on an end user's device, the iOS/iPadOS device shows an alert to allow management of the app by your organization. The end user must allow the organization to take management of the app before app configurations can be applied to a managed device. If the user cancels the alert, the alert will appear periodically for as long as the device is managed and the app is assigned.  

:::image type="content" source="./media/end-user-apps-ios/intune-app-management-confirmation-2002.png" alt-text="Image of the App Management Change alert, showing Cancel and Manage options.":::

## See also  

[How your Android users get their apps](end-user-apps-android.md)

[How your Windows users get their apps](end-user-apps-windows.md)
