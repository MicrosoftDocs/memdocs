---
# required metadata

title: Install Microsoft 365 apps to macOS devices using Microsoft Intune
titleSuffix: 
description: Learn how you can use Microsoft Intune to install Microsoft 365 apps on macOS devices.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/17/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.assetid: 2372332a-7e3a-4a9c-91a9-86654e0fabe2

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: arnab
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- macOS
---

# Assign Microsoft 365 to macOS devices with Microsoft Intune

This app type makes it easy for you to assign Microsoft 365 apps to macOS devices. By using this app type, you can install Word, Excel, PowerPoint, Outlook, OneNote, Teams, and OneDrive. To help keep the apps more secure and up to date, the apps come with Microsoft AutoUpdate (MAU). The apps that you want are displayed as one app in the list of apps in the Intune admin center.

> [!IMPORTANT]
> With Office for Mac update (16.67), macOS Big Sur 11 or later will be required to receive updates to Office for Mac. If you continue with an older version of macOS, your Microsoft 365 apps will still work, but you'll no longer receive any updates, including security updates. Upgrading your operating system to macOS Big Sur 11 or later will allow Office updates to be delivered for your apps. The October 2022 Office for Mac update (16.66) will be the last build to support macOS Catalina 10.15. For related information, see [Upgrade macOS to continue receiving Microsoft 365 and Office for Mac updates](https://go.microsoft.com/fwlink/?linkid=2015804).

> [!NOTE]
> Other versions of Office for Mac can be added to the Microsoft Intune admin center. For more information, see [Most current packages for Office for Mac](/officeupdates/update-history-office-for-mac#most-current-packages-for-office-for-mac).
>
> Microsoft Office 365 ProPlus has been renamed to **Microsoft 365 Apps for enterprise**. In our documentation, we'll commonly refer to it as **Microsoft 365 Apps**.

## Before you start

Before you begin adding Microsoft 365 apps to macOS devices, understand the following details:

- Devices to which you deploy these apps must be running macOS 10.14 or later.
- If any Microsoft 365 apps are open when Intune installs the app suite, users might lose data from unsaved files.

## Select Microsoft 365 Apps

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All Apps** > **Create**.
3. Select **macOS** in the **Microsoft 365 Apps** section of the **Select app type** pane.
4. Click **Select**. The **Add Microsoft 365 Apps** steps are displayed.

## Step 1 - App suite information

In this step, you provide information about the app suite. This information helps you to identify the app suite in Intune, and it helps users to find the app suite in the company portal.

1. In the **App suite information** page, you can confirm or modify the default values:
    - **Suite Name**: Enter the name of the app suite as it is displayed in the company portal. Make sure that all suite names that you use are unique. If the same app suite name exists twice, only one of the apps is displayed to users in the company portal.
    - **Suite Description**: Enter a description for the app suite. For example, you could list the apps you've selected to include.
    - **Publisher**: Microsoft appears as the publisher.
    - **Category**: Optionally, select one or more of the built-in app categories or a category that you created. This setting makes it easier for users to find the app suite when they browse the company portal.
    - **Show this as a featured app in the Company Portal**: Select this option to display the app suite prominently on the main page of the company portal when users browse for apps.
    - **Information URL**: Optionally, enter the URL of a website that contains information about this app. The URL is displayed to users in the company portal.
    - **Privacy URL**: Optionally, enter the URL of a website that contains privacy information for this app. The URL is displayed to users in the company portal.
    - **Developer**: Microsoft appears as the developer.
    - **Owner**: Microsoft appears as the owner.
    - **Notes**: Enter any notes that you want to associate with this app.
    - **Logo**: The Microsoft 365 Apps logo is displayed with the app when users browse the company portal.
2. Click **Next** to display the **Scope tags** page.

## Step 2 - Select scope tags (optional)

You can use scope tags to determine who can see client app information in Intune. For full details about scope tags, see [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md).

1. Click **Select scope tags** to optionally add scope tags for the app suite.
2. Click **Next** to display the **Assignments** page.

## Step 3 - Assignments

1. Select the **Required** or **Available for enrolled devices** group assignments for the app suite. For more information, see [Add groups to organize users and devices](../fundamentals/groups-add.md) and [Assign apps to groups with Microsoft Intune](apps-deploy.md).

    >[!Note]
    > You cannot uninstall the 'Microsoft 365 apps for macOS' app suite through Intune.

2. Click **Next** to display the **Review + create** page.

## Step 4 - Review + create

1. Review the values and settings you entered for the app suite.
2. When you are done, click **Create** to add the app to Intune.

    The **Overview** blade is displayed. The suite appears in the list of apps as a single entry.

## Next steps

- To learn about adding Microsoft 365 apps to Windows 10 devices, see [Assign Microsoft 365 Apps to Windows 10 devices with Microsoft Intune](apps-add-office365.md).
- To learn about including and excluding app assignments from groups of users, see [Include and exclude app assignments](apps-inc-exl-assignments.md).
