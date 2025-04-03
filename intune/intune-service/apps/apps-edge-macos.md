---
# required metadata

title: Add Microsoft Edge to macOS devices using Microsoft Intune
titleSuffix:
description: Learn about adding Microsoft Edge to macOS devices using Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/17/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: arnab
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.collection:
- tier3
- M365-identity-device-management
- macOS
- FocusArea_Apps_Add
---

# Add Microsoft Edge to macOS devices using Microsoft Intune

Before you can deploy, configure, monitor, or protect apps, you must add them to Intune. One of the available [app types](apps-add.md#app-types-in-microsoft-intune) is Microsoft Edge *version 77 and later*. By selecting this app type in Intune, you can assign and install Microsoft Edge *version 77 and later* to devices you manage that run macOS. This app type makes it easy for you to assign Microsoft Edge to macOS devices without requiring you to use the macOS app wrapping tool. To help keep the apps more secure and up to date, the app comes with Microsoft AutoUpdate (MAU).

> [!IMPORTANT]
> This app type offers developer and beta channels for macOS. The deployment is in English (EN) only, however end users can change the display language in the browser under **Settings** > **Languages**. 

> [!NOTE]
> Microsoft Edge *version 77 and later* is available for Windows 10 as well.

## Prerequisites

- The macOS device must be running macOS 10.14 or later before installing Microsoft Edge.

## Add Microsoft Edge to Intune

You can add Microsoft Edge version 77 and later to Intune using the following steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All Apps** > **Create**.
3. In the **App type** list under the **Microsoft Edge, version 77 and later**, select **macOS**.

## Configure app information
In this step, you provide information about this app deployment. This information helps you identify the app in Intune, and it helps users find the app in the company portal.

1. Click **App information** to display the **App information** pane.
2. In the **App information** pane, you provide information about this app deployment. This information helps you identify the app in Intune, and it helps users find the app in the company portal.
    - **Name**: Enter the name of the app as it will be displayed in the company portal. Make sure that all names are unique. If the same app name exists twice, only one of the apps is displayed to users in the company portal.
    - **Description**: Enter a description for the app. For example, you could list the targeted users in the description.
    - **Publisher**: Microsoft appears as the publisher.
    - **Category**: Optionally, select one or more of the built-in app categories or a category that you created. This setting makes it easier for users to find the app when they browse the company portal.
    - **Display this as a featured app in the Company Portal**: Select this option to display the app prominently on the main page of the company portal when users browse for apps.
    - **Information URL**: Optionally, enter the URL of a website that contains information about this app. The URL is displayed to users in the company portal.
    - **Privacy URL**: Optionally, enter the URL of a website that contains privacy information for this app. The URL is displayed to users in the company portal.
    - **Developer**: Microsoft appears as the developer.
    - **Owner**: Microsoft appears as the owner.
    - **Notes**: Optionally, enter any notes that you want to associate with this app.
3. Select **OK**.

## Configure Microsoft Edge settings
In this step, configure installation options for the app.

1. In the **Add App** pane, select **App settings**.
2. In the **App settings** pane, select either **Stable**, **Beta** or **Dev** from the **Channel** list to determine which Edge Channel you will deploy the app from. For more information, see [Microsoft Edge release schedule](/DeployEdge/microsoft-edge-release-schedule).

    - **Stable** channel is the recommended channel for deploying broadly in Enterprise environments. It updates every four weeks, each release incorporating improvements from the Beta channel.
    - **Beta** channel is the most stable Microsoft Edge preview experience and the best choice for a full pilot within your organization. With major updates every four weeks, each release incorporates the learnings and improvements from the Dev channel.
    - **Dev** channel is ready for enterprise feedback on Windows, Windows Server and macOS. It updates every week and contains the latest improvements and fixes.

    > [!NOTE]
    > The Microsoft Edge browser logo is displayed with the app when users browse the company portal.

3.    Select **OK**.

## Select scope tags (optional)
You can use scope tags to determine who can see client app information in Intune. For full details about scope tags, see Use role-based access control and scope tags for distributed IT.
1.    Select **Scope (Tags)** > **Add**.
2.    Use the **Select** box to search for scope tags.
3.    Select the check box next to the scope tags you want to assign to this app.
4.    Click **Select** > **OK**.

## Add the app
When you've completed configuring, select **Add** from the **App app** pane. 

The app you've created is displayed in the apps list, where you can assign it to the groups that you select.

## Next steps
- To learn how to configure Microsoft Edge on macOS devices, see [Configure Microsoft Edge on macOS devices](/deployedge/configure-microsoft-edge-on-mac).
- To learn about including and excluding app assignments from groups of users, see [Include and exclude app assignments](apps-inc-exl-assignments.md).
- [Assign apps to groups](apps-deploy.md)