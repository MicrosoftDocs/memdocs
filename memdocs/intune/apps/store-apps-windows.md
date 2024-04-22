---
# required metadata

title: Add Microsoft Store apps to Intune (legacy)
titleSuffix:
description: Learn about adding Microsoft Store (legacy) apps to Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/17/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.assetid: 07241b6d-86d8-4abb-83a2-3fc5feae5788

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: bryanke
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- FocusArea_Apps_Store
---

# Add Microsoft Store apps to Intune (legacy)

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Before you can assign, monitor, configure, or protect apps, you must add them to Intune. 

> [!IMPORTANT]
> The steps provided in this topic refer to adding Microsoft Store apps using the legacy method. For the latest method, see  [Add Microsoft Store apps to Microsoft Intune](../apps/store-apps-microsoft.md).

## Add an app to Intune
You can add a Microsoft Store app to Intune by doing the following:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All apps** > **Add**.
3. In the **Select app type** pane, under the available **Store app** types, select **Microsoft store app (Legacy)**.
4. Click **Select**. The **Add app** steps are displayed.
5. To configure the **App information** for Microsoft store apps, click **Select app**, and search for the app you want to assign to members of your organization. Display the app page and make a note of the app details. 
6. In the **App information** page, add the app details:
    - **Name**: Enter the name of the app as it is to be displayed in the company portal. Make sure that any app name that you use is unique. If an app name is duplicated, only one name is displayed to users in the company portal.
    - **Description**: Enter a description for the app. This description is displayed to users in the company portal.
    - **Publisher**: Enter the name of the publisher of the app. 
    - **Appstore URL**: Enter the 'Link for Intune' URL for the app provided by the store.
    - **Category**: Optionally, select one or more of the built-in app categories, or a category that you created. Doing so makes it easier for users to find the app when they browse the company portal.
    - **Show this as a featured app in the Company Portal**: Select this option to display the app suite prominently on the main page of the company portal when users browse for apps.
    - **Information URL**: Optionally, enter the URL of a website that contains information about this app. The URL is displayed to users in the company portal.
    - **Privacy URL**: Optionally, enter the URL of a website that contains privacy information for this app. The URL is displayed to users in the company portal.
    - **Developer**: Optionally, enter the name of the app developer.
    - **Owner**: Optionally, enter a name for the owner of this app, for example, *HR department*.
    - **Notes**: Optionally, enter any notes that you want to associate with this app.
    - **Logo**: Optionally, upload an icon that will be associated with the app. This icon is displayed with the app when users browse the company portal.
1. Click **Next** to display the **Scope tags** page.
1. Click **Select scope tags** to optionally add scope tags for the app. For more information, see [Use role-based access control (RBAC) and scope tags for distributed IT](../fundamentals/scope-tags.md).
1. Click **Next** to display the **Assignments** page.
1. Select the group assignments for the app. For more information, see [Add groups to organize users and devices](../fundamentals/groups-add.md). 
1. Click **Next** to display the **Review + create** page. Review the values and settings you entered for the app.
1. When you are done, click **Create** to add the app to Intune.

The **Overview** blade of the app you've created is displayed.

The app that you've created is displayed in the apps list, where you can assign it to the groups that you select.

> [!IMPORTANT]
> Microsoft Store apps can only be assigned to groups with the assignment type **Available for enrolled devices** (users install the app from the Company Portal app or website).

## Next steps

- [Assign apps to groups](apps-deploy.md)
