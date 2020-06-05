---
# required metadata

title: Add Android Enterprise system apps to Microsoft Intune
titleSuffix: 
description: Learn how to add Enterprise system apps to Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/23/2020
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

# Add Android Enterprise system apps to Microsoft Intune

Before you assign an app to a device or a group of users, you must first add the app to Microsoft Intune. System apps are supported on Android Enterprise devices. You can enable a system app for [Android Enterprise dedicated devices](../enrollment/android-kiosk-enroll.md) or [fully managed devices](../enrollment/android-fully-managed-enroll.md).

## Add the app

You can add an Android Enterprise system app to Intune from the Azure portal by doing the following:

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
12. When you are done, click **Create** to add the app to Intune.

The **Overview** blade of the app you've created is displayed.

> [!NOTE]
> You will need to work with the OEM of your device to find the package name of the app you would like to enable/disable.

The app you've created is displayed in the apps list, where you can assign it to the groups that you select. 

Android Enterprise system apps will enable or disable apps that are already part of the platform. To enable an app, assign the system app as **Required**. To disable an app, assign the system app as **Uninstall**. System apps cannot be assigned as available for a user.


## Next steps

- [Assign apps to groups](apps-deploy.md)
