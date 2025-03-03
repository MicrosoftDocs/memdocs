---
# required metadata

title: How to add macOS line-of-business apps to Microsoft Intune
titleSuffix:
description: Learn about how to add macOS line-of-business (LOB) apps to Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/20/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.assetid: ef8008ac-8b85-4bfc-86ac-1f9fcbd3db76

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
- highpri
- FocusArea_Apps_LOB
---

# How to add macOS line-of-business (LOB) apps to Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Use the information in this article to help you add macOS line-of-business apps to Microsoft Intune. 

> [!NOTE]
> macOS LOB apps have a maximum size limit of 8 GB per app.
>
> macOS LOB apps need to have a logo. If they don't have a logo, they won't be displayed in the apps section.
>
> While users of macOS devices can remove some of the built-in macOS apps like Stocks, and Maps, you cannot use Intune to redeploy those apps. If end users delete these apps, they must go to the app store, and manually re install them.

## App requirements

The .pkg file must satisfy the following requirements to successfully be deployed using Microsoft Intune.

1. The .pkg file is a component package or a package containing multiple packages.
2. The .pkg file does not contain a bundle or disk image or .app file.
3. The .pkg file is signed using a "Developer ID Installer" certificate, obtained from an Apple Developer account.
4. The .pkg file contains a payload. Packages without a payload attempt to re-install as long as the app remains assigned to the group.

## Select the app type

> [!NOTE]
> In August 2022, we removed the ability to upload wrapped .intunemac files in the Microsoft Intune admin center. You can now upload *.pkg* files to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

> [!IMPORTANT]
> The *.pkg* file must be signed using "Developer ID Installer" certificate, obtained from an Apple Developer account. Only *.pkg* files may be used to upload macOS LOB apps to Microsoft Intune. To deploy *.dmg* or *.app* files, see [Add a macOS DMG app to Microsoft Intune](../apps/lob-apps-macos-dmg.md).

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All Apps** > **Create**.
3. In the **Select app type** pane, under the **Other** app types, select **Line-of-business app**.
4. Click **Select**. The **Add app** steps are displayed.

## Step 1 - App information

### Select the app package file

1. In the **Add app** pane, click **Select app package file**. 
2. In the **App package file** pane, select the browse button. Then, select an macOS installation file with the extension *.pkg*.
   The app details are displayed.
3. When you're finished, select **OK** on the **App package file** pane to add the app.

### Set app information

1. In the **App information** page, add the details for your app. Depending on the app that you chose, some of the values in this pane might be automatically filled in.
    - **Name**: Enter the name of the app as it appears in the company portal. Make sure all app names that you use are unique. If the same app name exists twice, only one of the apps appears in the company portal.
    - **Description**: Enter the description of the app. The description appears in the company portal.
    - **Publisher**: Enter the name of the publisher of the app.
    - **Minimum Operating System**: From the list, choose the minimum operating system version on which the app can be installed. If you assign the app to a device with an earlier operating system, it won't be installed.
    - **Ignore app version**: Select **Yes** to install the app if the app is not already installed on the device. Select **No** to only install the app when it isn't already installed on the device, or if the deploying app's version number does not match the version that's already installed on the device.
    - **Install as managed**: Select **Yes** to install the Mac LOB app as a managed app on supported devices (macOS 11 and higher). A macOS LOB app can only be installed as managed when the app distributable contains a single app without any nested packages and installs to the */Applications* directory. Managed line-of-business apps are able to be removed using the **uninstall** assignment type on supported devices (macOS 11 and higher). In addition, removing the MDM profile removes all managed apps from the device. The default value is **No**.
    - **Included apps**: Review and edit the apps that are contained in the uploaded file. Included app bundle IDs and build numbers are used for detecting and monitoring app installation status of the uploaded file. The app listed first is used as the primary app in app reporting. <br>Included apps list should only contain the application(s) installed by the uploaded file in **Applications** folder on Macs. Any other type of file that isn't an application or an application that is not installed to **Applications** folder should be removed from the **Included apps** list. If **Included apps** list contains files that are not applications or if all the listed apps are not installed, app installation status does not report success.<br>Mac Terminal can be used to look up and confirm the included app details of an installed app.<br>For example, to look up the bundle ID and build number of a Company Portal, run the following:<br> *defaults read /Applications/Company\ Portal.app/Contents/Info CFBundleIdentifier*<br>Then, run the following:<br> *defaults read /Applications/Company\ Portal.app/Contents/Info CFBundleShortVersionString*
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

    > [!NOTE]
    > The **uninstall** intent will only be displayed for LOB apps created with **Install as managed** set to **Yes**. For more information, review **App information section** earlier on this article.

2. Click **Next** to display the **Review + create** page.

## Step 4 - Review + create

1. Review the values and settings you entered for the app.
2. When you are done, click **Create** to add the app to Intune.

    The **Overview** blade for the line-of-business app is displayed.

The app you created appears in the apps list where you can assign it to the groups you choose. For help, see [How to assign apps to groups](apps-deploy.md).

> [!NOTE]
> If the *.pkg* file contains multiple apps or app installers, then Microsoft Intune will only report that the *app* is successfully installed when all installed apps are detected on the device.

## Update a line-of-business app

[!INCLUDE [shared-proc-lob-updateapp](../includes/shared-proc-lob-updateapp.md)]

To update a line-of-business app deployed as a *.pkg* file, you must increment the `CFBundleShortVersionString` of the *.pkg* file.

For the line-of-business (LOB) apps, if the app is targeted with required intent and admin updated the content update, app install will be attempted in the next check in and if it fails then the re-attempt will happen every 24 hours.

## Next steps

- The app you have created is displayed in the apps list. You can now assign it to the groups you choose. For help, see [How to assign apps to groups](apps-deploy.md).

- Learn more about the ways in which you can monitor the properties and assignment of your app. For more information, see [How to monitor app information and assignments](apps-monitor.md).

- Learn more about the context of your app in Intune. For more information, see [Overview of device and app lifecycles](../fundamentals/device-lifecycle.md)
