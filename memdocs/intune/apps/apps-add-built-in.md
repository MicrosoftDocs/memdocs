---
# required metadata

title: Add built-in apps to mobile devices using Microsoft Intune
titleSuffix: 
description: Learn how you can use Intune to make it easier to install built-in apps mobile devices.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 11/21/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.assetid: 0ec8de66-5a0f-4c8d-afbf-c2becc7d6eec

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: bryanke
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- FocusArea_Apps_Add
---

# Add built-in apps to Microsoft Intune

The *built-in* app type makes it easy for you to assign curated managed apps, such as Microsoft 365 apps and third-party apps, to iOS/iPadOS and Android devices. You can assign specific apps for this app type, such as Excel, OneDrive, Outlook, Skype, and others. After you add an app, the app type is displayed as either *Built-in iOS app* or *Built-in Android app*. By using the built-in app type, you can choose which of these apps to publish to device users.

> [!NOTE]
> Built-in apps are not supported on Android Enterprise devices. For more information about Android Enterprise supported apps, see [Add Managed Google Play apps to Android Enterprise devices with Intune](../apps/apps-add-android-for-work.md) and [Manage Android Enterprise system apps in Microsoft Intune](../apps/apps-ae-system.md). 

In earlier versions of the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), Intune provided several default managed Microsoft 365 apps, such as Outlook and OneDrive. The app types for these managed apps were tagged as *Managed iOS Store App* or *Managed Android App*. Instead of using these app types, we recommend that you use the built-in app type. By using the built-in app type, you have the additional flexibility to edit and delete Microsoft 365 apps.

>[!NOTE]
>Default Microsoft 365 apps that are tagged as *Managed iOS Store* and *Managed Android App* are removed from the app list when all assignments are deleted.

## Add a built-in app

To add a built-in app to your available apps in Microsoft Intune, do the following:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All Apps** > **Create**.
3. In the **Select app type** pane, under the available **Other** types, select **Built-In app**.
4. Click **Select**. The **Add app** steps are displayed.
5. In the **Select Built-in apps** page, click **Select app** to select the apps that you want to include.
6. Select the built-in apps that you want to include.
7. Once you have selected the apps, click **Select** on the **Select Built-in apps** pane.
8. Click **Next** to display the **Scope tags** page.
9. Click **Select scope tags** to optionally add scope tags for the app. For more information, see [Use role-based access control (RBAC) and scope tags for distributed IT](../fundamentals/scope-tags.md).
10. Click **Next** to display the **Assignments** page.
11. Select the group assignments for the app. For more information, see [Add groups to organize users and devices](../fundamentals/groups-add.md).
12. Click **Next** to display the **Review + create** page. Review the values and settings you entered for the app.
13. When you are done, click **Create** to add the app to Intune.

    The **Overview** blade of the app you've created is displayed.

## Configure app information

You can modify information about the built-in app. This information helps you to identify the app in Intune and helps users find the app in the company portal.

1. Select **Apps** > **All Apps** and select the built-in app that you want to modify.  
   A pane for the built-in app is displayed.
2. Select  **Properties**.
3. Select **Edit** next to **App information**.
4. In the **App information** pane, you can modify the following information:
    - **Name**: Enter the name of the built-in app as it is displayed in the company portal. Make sure all names that you use are unique. If the same app name exists twice, only one of the apps is displayed to users in the company portal.
    - **Description**: Enter a description for the app. 
    - **Publisher**: Enter the name of the publisher of the app.
    - **Category**: Optionally, select one or more of the built-in app categories. Setting this option makes it easier for users to find the app when they browse the company portal.
    - **Show this as a featured app in the company portal**: Display the app prominently on the main page of the company portal when users browse for apps.
    - **Information URL**: Optionally, enter the URL of a website that contains information about this app. The URL is displayed to users in the company portal.
    - **Privacy URL**: Optionally, enter the URL of a website that contains privacy information for this app. The URL is displayed to users in the company portal.
    - **Developer**: Optionally, enter the name of the app developer.
    - **Owner**: Optionally, enter a name for the owner of this app (for example, *HR department*).
    - **Notes**: Enter any notes that you want to associate with this app.
    - **Upload Icon**: Upload an icon that is displayed with the app when users browse the company portal.
5. Click **Review + save** to display the **Review + create** page. Review the values and settings you entered for the app.
6. When you are done, click **Save** to update the app in Intune.

    The **Overview** blade of the app you've created is displayed.

## Next steps

- You can now assign the apps to the groups that you choose. For more information, see [Assign apps to groups](apps-deploy.md).
