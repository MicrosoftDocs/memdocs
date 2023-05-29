---
# required metadata

title: Add Microsoft Defender for Endpoint to macOS devices using Microsoft Intune
titleSuffix:
description: Learn about adding Microsoft Defender for Endpoint to macOS devices using Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/01/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: arnab
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.collection:
- tier2
- M365-identity-device-management
- macOS
---

# Add Microsoft Defender for Endpoint to macOS devices using Microsoft Intune

Before you can deploy, configure, monitor, or protect apps, you must add them to Intune. One of the available [app types](apps-add.md#app-types-in-microsoft-intune) is Microsoft Defender for Endpoint. By selecting this app type in Intune, you can assign and install Microsoft Defender for Endpoint to devices you manage that run macOS. This app type makes it easy for you to assign Microsoft Defender for Endpoint to macOS devices without requiring you to use the macOS app wrapping tool. To help keep the apps more secure and up to date, the app comes with Microsoft AutoUpdate (MAU).

## Prerequisites

- The macOS device must be running macOS 10.13 or later.
- The macOS device must have at least 650 MB of disk space.
- Deploy kernel extension in Intune. See more information, see [Add macOS kernel extensions in Intune](../configuration/kernel-extensions-overview-macos.md).

> [!IMPORTANT]
> The kernel extension can be automatically approved only if it is present on the device before the Microsoft DDefender for Endpoint app is installed. Else, users will see "System extension blocked" message on Macs and must approve the extension by going to **Security Preferences** or **System Preferences** > **Security & Privacy** and then selecting **Allow**. For more information, see [Troubleshoot kernel extension issues in Microsoft Defender for Endpoint for Mac](/windows/security/threat-protection/microsoft-defender-atp/mac-support-kext).

## Add Microsoft Defender for Endpoint to Intune

You can add Microsoft Defender for Endpoint to Intune using the following steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All apps** > **Add**.
3. In the **App type** list under the **Microsoft Defender for Endpoint**, select **macOS**.

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

## Select scope tags (optional)

You can use scope tags to determine who can see client app information in Intune. For full details about scope tags, see Use role-based access control and scope tags for distributed IT.

1. Select **Scope (Tags)** > **Add**.
2. Use the **Select** box to search for scope tags.
3. Select the check box next to the scope tags you want to assign to this app.
4. Click **Select** > **OK**.

## Add the app

When you've completed configuring, select **Add** from the **App app** pane.

The app you've created is displayed in the apps list, where you can assign it to the groups that you select.

> [!NOTE]
> Currently, Apple does not provide a way for Intune to uninstall Microsoft Defender for Endpoint on macOS devices.

## Next steps

- To learn about Intune-based deployment for Microsoft Defender for Endpoint on macOS, see [Intune-based deployment for Microsoft Defender for Endpoint on macOS](/microsoft-365/security/defender-endpoint/mac-install-with-intune)
- To learn about applying an antivirus policy for endpoint security in Intune, see [Antivirus policy for endpoint security in Intune](../protect/endpoint-security-antivirus-policy.md)
- To learn about including and excluding app assignments from groups of users, see [Include and exclude app assignments](apps-inc-exl-assignments.md).
- To learn how to assign apps to groups in Intune, see [Assign apps to groups](apps-deploy.md).
