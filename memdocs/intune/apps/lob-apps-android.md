---
# required metadata

title: Add an Android line-of-business app to Microsoft Intune
description: Learn about how to add a Android line-of-business (LOB) app to Microsoft Intune.
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
ms.assetid: 061d793c-c724-4cd9-9240-adb0cbda5661

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: manchen
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.collection:
- tier1
- M365-identity-device-management
- Android
ms.custom: intune-azure
---

# Add an Android line-of-business app to Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

A line-of-business (LOB) app is an app that you add to Intune from an app installation file. This kind of app is typically written in-house. Intune installs the LOB app on the user's device.

> [!NOTE]
> For more information about LOB apps and the Google Play Developer Console, see [Managed Google Play private (LOB) app publishing using the Google Developer Console](apps-add-android-for-work.md?#managed-google-play-private-lob-app-publishing-using-the-google-developer-console). 

> [!NOTE]
> For Android Enterprise devices, see [Add Managed Google Play apps to Android Enterprise devices with Intune](apps-add-android-for-work.md).

## Select the app type

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All apps** > **Add**.
3. In the **Select app type** pane, under the **Other** app types, select **Line-of-business app**.
4. Click **Select**. The **Add app** steps are displayed.

## Step 1 - App information

### Select the app package file

1. In the **Add app** pane, click **Select app package file**.
2. In the **App package file** pane, select the browse button. Then, select an Android installation file with the extension **.apk**.
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

1. Select the **Required**, **Available for enrolled devices**, or **Uninstall** group assignments for the app. For more information, see [Add groups to organize users and devices](../fundamentals/groups-add.md) and [Assign apps to groups with Microsoft Intune](apps-deploy.md).
2. Click **Next** to display the **Review + create** page.

## Step 4 - Review + create

1. Review the values and settings you entered for the app.
2. When you are done, click **Create** to add the app to Intune.

    The **Overview** blade for the line-of-business app is displayed.

## Step 5: Update a line-of-business app

[!INCLUDE [shared-proc-lob-updateapp](../includes/shared-proc-lob-updateapp.md)]

If **Check apps from external sources** is enabled on the Android device, the user will be prompted before installing the update. Otherwise the update will be installed automatically.

> [!NOTE]
> For the Intune service to successfully deploy a new APK file to the device, you must increment the `android:versionCode` string in the AndroidManifest.xml file in your APK package.

## Next steps

- The app that you created appears in the list of apps. You can now assign it to groups that you choose. For help, see [How to assign apps to groups](apps-deploy.md).

- Learn more about the ways in which you can monitor the properties and assignment of your app. See [How to monitor app information and assignments](apps-monitor.md).

- Learn more about the context of your app in Intune. See [Overview of device and app lifecycles](../fundamentals/device-lifecycle.md).
