---
# required metadata

title: Add an iOS/iPadOS line-of-business app to Microsoft Intune
titleSuffix:
description: Learn about how to add an iOS/iPadOS line-of-business (LOB) app to Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/20/2025
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.assetid: 099101e8-4b22-40ac-ba19-82ba5c71944c

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
- iOS/iPadOS
- FocusArea_Apps_LOB
---

# Add an iOS/iPadOS line-of-business app to Microsoft Intune

Use the information in this article to help you add an iOS/iPadOS line-of-business (LOB) app to Microsoft Intune. A line-of-business (LOB) app is an app that you add to Intune from an IPA app installation file. This kind of app is typically written in-house. You'll first need to join the iOS Developer Enterprise Program.

> [!NOTE]
> Users of iOS/iPadOS devices can remove some of the built-in iOS/iPadOS apps, like Stocks and Maps. You can't use Intune to redeploy these apps. If users delete these apps, they must go to the app store and manually reinstall them.
>
> iOS/iPadOS LOB apps have a maximum size limit of 2 GB per app.
>
> Bundle identifiers (for example, *com.contoso.app*) are meant to be unique identifiers of an app. For example, to install a beta version of an LOB app next to the production version for testing purposes, the beta version must have a different unique identifier (for example, *com.contoso.app-beta*). Otherwise, the beta version will overlap with the production and be treated as an upgrade. Renaming the .ipa file has no effect on this behavior.

You can deploy LOB apps to Shared iPad devices. For Shared iPad devices, line-of-business apps must be assigned as **required** to a device group containing Shared iPad devices from the Microsoft Intune admin center.

## Select the app type

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All Apps** > **Create**.
3. In the **Select app type** pane, under the **Other** app types, select **Line-of-business app**.
4. Click **Select**. The **Add app** steps are displayed.

## Step 1 - App information

### Select the app package file

1. In the **Add app** pane, click **Select app package file**.
2. In the **App package file** pane, select the browse button. Then, select an iOS/iPadOS installation file with the extension **.ipa**.
   The app details will be displayed.
3. When you're finished, select **OK** on the **App package file** pane to add the app.

### Set app information

1. In the **App information** page, add the details for your app. Depending on the app that you chose, some of the values in this pane might be automatically filled in.
    - **Name**: Enter the name of the app as it appears in the company portal. Make sure all app names that you use are unique. If the same app name exists twice, only one of the apps appears in the company portal.
    - **Description**: Enter the description of the app. The description appears in the company portal.
    - **Publisher**: Enter the name of the publisher of the app.
    - **Minimum Operating System**: From the list, choose the minimum operating system version on which the app can be installed. If you assign the app to a device with an earlier operating system, it will not be installed.
    - **Category**: Select one or more of the built-in app categories, or select a category that you created. Categories make it easier for users to find the app when they browse through the company portal.
    - **Show this as a featured app in the Company Portal**: Display the app prominently on the main page of the company portal when users browse for apps.
    - **Information URL**: Optionally, enter the URL of a website that contains information about this app. The URL appears in the company portal.
    - **Privacy URL**: Optionally, enter the URL of a website that contains privacy information for this app. The URL appears in the company portal.
    - **Developer**: Optionally, enter the name of the app developer.
    - **Owner**: Optionally, enter a name for the owner of this app. An example is **HR department**.
    - **Notes**: Enter any notes that you want to associate with this app.
    - **Logo**: Upload an icon that is associated with the app. This icon is displayed with the app when users browse through the company portal.
2. Click **Next** to display the **Scope tags** page.

## Step 2 - Select scope tags (optional)

You can use scope tags to determine who can see client app information in Intune. For full details about scope tags, see [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md).

1. Click **Select scope tags** to optionally add scope tags for the app.
2. Click **Next** to display the **Assignments** page.

## Step 3 - Assignments

1. Select the **Required**, **Available for enrolled devices**, **Available with or without enrollment**, or **Uninstall** group assignments for the app. For more information, see [Add groups to organize users and devices](../fundamentals/groups-add.md) and [Assign apps to groups with Microsoft Intune](apps-deploy.md).

1. Click **Next** to display the **Review + create** page.

> [!NOTE]
> Users may receive the "Open in iTunes?" prompt when installing LOB apps from the iOS Company Portal. Instruct users to click 'Open' to install the LOB app. 
## Step 4 - Review + create

1. Review the values and settings you entered for the app.
2. When you're done, click **Create** to add the app to Intune.

    The **Overview** blade for the line-of-business app is displayed.

The app that you created now appears in the list of apps. From the list, you can assign the apps to groups that you choose. For help, see [How to assign apps to groups](apps-deploy.md).

> [!NOTE]
> Provisioning profiles for iOS/iPadOS LOB apps have a 30 day notice before they'll expire.

## Step 5: Update a line-of-business app

[!INCLUDE [shared-proc-lob-updateapp](../includes/shared-proc-lob-updateapp.md)]

The update to the line-of-business app will be installed automatically.

> [!NOTE]
> For the Intune service to successfully deploy a new IPA file to the device, you must update the CFBundleVersion and CFBundleShortVersionString in the Info.plist file in your IPA package. You're allowed to upgrade an app by increasing the value, or downgrade an app by decreasing the value, however you can't upload a new version of CFBundleVersion and CFBundleShortVersionString of the new app is identical to the existing one.

For an iOS LOB app targeted with available intent, autoupdate of the application will happen as long as the following conditions are met:

- The end user must request the specific Intune app from the Company Portal and the app must be successfully installed, or the app is already installed on the device.
- The targeting for the user hasn't changed (app assignment with available intent isn't removed and user isn't removed from the group membership in the life cycle of the app assignment).
- If the previous version of the app is installed through required intent, then the available app update won't happen. The app will be updated automatically as long as the user/device is part of required intent group.
- If the app has both available and required deployments targeted, the resolved intent becomes 'RequiredAndAvailable'. **Note:** You can't create **Available** and **Required** deployments to the same Microsoft Entra group, but you can use different Microsoft Entra group with same members in it. If the app was installed automatically on devices after the **Required** deployment is created (not manually installed from Company Portal) and the required deployment is later removed, the **Available** app update won't happen automatically on those devices and the users have to request the app from Company Portal.

## Next steps

- The app that you created appears in the list of apps. You can now assign it to groups that you choose. For help, see [How to assign apps to groups](apps-deploy.md).

- Learn more about the ways in which you can monitor the properties and assignment of your app. See [How to monitor app information and assignments](apps-monitor.md).

- Learn more about the context of your app in Intune. See [Overview of device and app lifecycles](../fundamentals/device-lifecycle.md).

