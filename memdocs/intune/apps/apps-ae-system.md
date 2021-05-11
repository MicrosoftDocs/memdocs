---
# required metadata

title: Manage Android Enterprise system apps in Microsoft Intune
titleSuffix: 
description: Learn how to manage Android Enterprise system apps in Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/11/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Manage Android Enterprise system apps in Microsoft Intune

Before you assign an Android Enterprise system app to a device, you must first enable the app in Microsoft Intune. System apps are supported on Android Enterprise devices. You can enable a system app for [Android Enterprise dedicated devices](../enrollment/android-kiosk-enroll.md), [fully managed devices](../enrollment/android-fully-managed-enroll.md), [Android Enterprise corporate-owned with work profile](../enrollment/android-corporate-owned-work-profile-enroll.md), or [Android Enterprise personally-owned work profiles](../apps/android-deployment-scenarios-app-protection-work-profiles.md). When you no longer need the system app, you can disable it.

## Enable a system app in Intune

You can enable an Android Enterprise system app in Intune using the following steps:

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All apps** > **Add**.
3. In the **Select app type** pane, under the available **Other** types, select **Android Enterprise system app**.
4. Click **Select**. The **Add app** steps are displayed.
In the **App information** page, add the app details:
    - **App Name**: Enter the name of the app.
    - **Publisher**: Enter the name of the publisher of the app.  
    - **Package Name**: Enter a package name. Intune will validate that the package name is valid.
5. Click **Next** to display the **Scope tags** page.
8. Click **Select scope tags** to optionally add scope tags for the app. For more information, see [Use role-based access control (RBAC) and scope tags for distributed IT](../fundamentals/scope-tags.md).
9. Click **Next** to display the **Assignments** page.
10. Select the group assignments for the app. For more information, see [Add groups to organize users and devices](../fundamentals/groups-add.md). 
11. Click **Next** to display the **Review + create** page. Review the values and settings you entered for the app.
12. When you are done, click **Create** to enable the app in Intune.

The **Overview** blade of the app you've created is displayed.

> [!NOTE]
> You will need to work with the OEM of your device to find the package name of the app you would like to enable/disable.

The app you've created is displayed in the apps list, where you can assign it to the groups that you select. 

Android Enterprise system apps will enable or disable apps that are already part of the platform. To enable an app, assign the system app as **Required**. To disable an app, assign the system app as **Uninstall**. System apps cannot be assigned as available for a user.

## Disable a system app in Intune

You can disable an Android Enterprise system app in Intune using the following steps:

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All apps**.
3. Select the system app from the app list.
4. Click **Delete** > **Yes** to disable the system app.

## Next steps

- [Assign apps to groups](apps-deploy.md)
