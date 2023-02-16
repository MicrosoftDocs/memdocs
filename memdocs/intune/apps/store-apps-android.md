---
# required metadata

title: Add Android store apps to Microsoft Intune
titleSuffix: 
description: Learn how to add Android store apps from the Google Play store to Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/16/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.technology:
ms.assetid: 4433000a-23e9-4cad-a818-48c28eedc1f5

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: manchen
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.collection:
- tier2
- M365-identity-device-management
- Android
ms.custom: intune-azure
---

# Add Android store apps to Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Before you assign an app to a device or a group of users, you must first add the app to Microsoft Intune. 

## Add an app

You can add an Android store app to Intune from the portal by doing the following:

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All apps** > **Add**.
3. In the **Select app type** pane, under the available **Store app** types, select **Android store app**.
4. Click **Select**.<br>
   The **Add app** steps are displayed.
5. To configure the **App information** for the Android app, navigate to the [Google Play store](https://play.google.com/store) and search for the app you want to deploy. Display the app page and make a note of the app details. 
6. In the **App information** page, add the app details:
    - **Name**: Enter the name of the app as it is to be displayed in the company portal. Make sure that any app name that you use is unique. If an app name is duplicated, only one name is displayed to users in the company portal.
    - **Description**: Enter a description for the app. This description is displayed to users in the company portal.
    - **Publisher**: Enter the name of the publisher of the app.
    - **Appstore URL**: Enter the app store URL of the app that you want to create. Use the URL of the app page when the details of the app are displayed in the store.
    - **Minimum operating system**: In the list, select the earliest operating system version on which the app can be installed. If you assign the app to a device with an earlier operating system, it will not be installed.
    - **Category**: Optionally, select one or more of the built-in app categories, or a category that you created. Doing so makes it easier for users to find the app when they browse the company portal.
    - **Show this as a featured app in the Company Portal**: Select this option to display the app suite prominently on the main page of the company portal when users browse for apps. Applies to apps deployed with Available intent.
    - **Information URL**: Optionally, enter the URL of a website that contains information about this app. The URL is displayed to users in the company portal.
    - **Privacy URL**: Optionally, enter the URL of a website that contains privacy information for this app. The URL is displayed to users in the company portal.
    - **Developer**: Optionally, enter the name of the app developer.
    - **Owner**: Optionally, enter a name for the owner of this app, for example, *HR department*.
    - **Notes**: Optionally, enter any notes that you want to associate with this app.
    - **Logo**: Optionally, upload an icon that will be associated with the app. This icon is displayed with the app when users browse the company portal.
7. Click **Next** to display the **Scope tags** page.
8. Click **Select scope tags** to optionally add scope tags for the app. For more information, see [Use role-based access control (RBAC) and scope tags for distributed IT](../fundamentals/scope-tags.md).
9. Click **Next** to display the **Assignments** page.
10. Select the group assignments for the app. For more information, see [Add groups to organize users and devices](../fundamentals/groups-add.md).
11. Click **Next** to display the **Review + create** page. Review the values and settings you entered for the app.
12. When you are done, click **Create** to add the app to Intune.

The **Overview** blade of the app you've created is displayed.

## Next steps

- [Assign apps to groups](apps-deploy.md)

## Related topics

- [Add Managed Google Play apps to Android Enterprise devices with Intune](./apps-add-android-for-work.md)