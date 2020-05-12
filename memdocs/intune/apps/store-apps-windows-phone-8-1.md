---
# required metadata

title: Add Windows Phone 8.1 store apps to Microsoft Intune
titleSuffix: 
description: This topic describes how to add Windows Phone 8.1 store apps to Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/22/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology:
ms.assetid: 4a95e575-2c63-4bfc-b9c4-f0a132eef618

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Add Windows Phone 8.1 store apps to Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Before you assign an app to a device or a group of users, you must first add the app to Microsoft Intune. 

## Add an app to Intune
You can add a Windows Phone 8.1 store app to Intune from the Azure portal by doing the following:

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All apps** > **Add**.
3. In the **Select app type** pane, under the available **Store app** types, select **Windows Phone 8.1 store app**.
4. Click **Select**.<br>
   The **Add app** steps are displayed.
5. To configure the **App information** for Windows Phone 8.1 store apps, navigate to the [Microsoft store](https://www.microsoft.com/store/apps/windows-phone) and search for the app you want to deploy. Display the app page and make a note of the app details. 
6. In the **App information** page, add the app details:
    - **Name**: Enter the name of the app as it is to be displayed in the company portal. Make sure that any app name that you use is unique. If an app name is duplicated, only one name is displayed to users in the company portal.
    - **Description**: Enter a description for the app. This description is displayed to users in the company portal.
    - **Publisher**: Enter the name of the publisher of the app.
    - **Appstore URL**: Type the App Store URL of the app that you want to create.
    - **Category**: Optionally, select one or more of the built-in app categories, or a category that you created. Doing so makes it easier for users to find the app when they browse the company portal.
    - **Show this as a featured app in the Company Portal**: Select this option to display the app suite prominently on the main page of the company portal when users browse for apps.
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


The app that you've created is displayed in the apps list, where you can assign it to the groups that you select.

## Next steps

- [Assign apps to groups](apps-deploy.md)
