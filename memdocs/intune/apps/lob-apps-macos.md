---
# required metadata

title: How to add macOS line-of-business apps to Microsoft Intune
titleSuffix:
description: Learn about how to add macOS line-of-business (LOB) apps to Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/13/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.technology:
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
- M365-identity-device-management
- macOS
- highpri
---

# How to add macOS line-of-business (LOB) apps to Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Use the information in this article to help you add macOS line-of-business apps to Microsoft Intune. You must download an external tool to pre-process your *.pkg* files before you can upload your line-of-business file to Microsoft Intune. The pre-processing of your *.pkg* files must take place on a macOS device.

> [!NOTE]
> Starting with the release of macOS Catalina 10.15, prior to adding your apps to Intune, check to make sure your macOS LOB apps are notarized. If the developers of your LOB apps did not notarize their apps, the apps will fail to run on your users' macOS devices. For more information about how to check if an app is notarized, visit [Notarize your macOS apps to prepare for macOS Catalina](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Notarizing-your-macOS-apps-to-prepare-for-macOS/ba-p/808579).
> 
> macOS LOB apps have a maximum size limit of 2 GB per app.
> 
> While users of macOS devices can remove some of the built-in macOS apps like Stocks, and Maps, you cannot use Intune to redeploy those apps. If end users delete these apps, they must go to the app store, and manually re install them.

## Before your start

> [!NOTE]
> Using the Intune App Wrapping Tool for Mac is not required when uploading *.pkg* files.

You must download an external tool, mark the downloaded tool as an executable, and pre-process your *.pkg* files with the tool before you can upload your line-of-business file to Microsoft Intune. The pre-processing of your *.pkg* files must take place on a macOS device. Use the Intune App Wrapping Tool for Mac to enable Mac apps to be managed by Microsoft Intune.

> [!IMPORTANT]
> The *.pkg* file must be signed using "Developer ID Installer" certificate, obtained from an Apple Developer account. Only *.pkg* files may be used to upload macOS LOB apps to Microsoft Intune. However, conversion of other formats, such as *.dmg* to *.pkg* is supported. For more information about converting non-pkg application types, see [How to deploy DMG or APP-format apps to Intune-managed Macs](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-deploy-dmg-or-app-format-apps-to-intune-managed-macs/ba-p/1503416).

1. Download the [Intune App Wrapping Tool for Mac](https://github.com/msintuneappsdk/intune-app-wrapping-tool-mac).

    > [!NOTE]
    > The **Intune App Wrapping Tool for Mac** must be run on a macOS machine. 

2. Mark the downloaded tool as an executable:
   - Start the terminal app.
   - Change the directory to the location where `IntuneAppUtil` is located.
   - Run the following command to make the tool executable:<br> 
       `chmod +x IntuneAppUtil`

3. Use the `IntuneAppUtil` command within the **Intune App Wrapping Tool for Mac** to wrap *.pkg* LOB app file from a *.intunemac* file.<br>

    Sample commands to use for the Microsoft Intune App Wrapping Tool for macOS:
    > [!IMPORTANT]
    > Ensure that the argument `<source_file>` does not contain spaces before running the `IntuneAppUtil` commands.

    - `IntuneAppUtil -h`<br>
    This command will show usage information for the tool.
    
    - `IntuneAppUtil -c <source_file> -o <output_directory_path> [-v]`<br>
    This command will wrap the *.pkg* LOB app file provided in `<source_file>` to a *.intunemac* file of the same name and place it in the folder pointed to by `<output_directory_path>`.
    
    - `IntuneAppUtil -r <filename.intunemac> [-v]`<br>
    This command will extract the detected parameters and version for the created *.intunemac* file.

## Select the app type

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All apps** > **Add**.
3. In the **Select app type** pane, under the **Other** app types, select **Line-of-business app**.
4. Click **Select**. The **Add app** steps are displayed.

## Step 1 - App information

> [!NOTE]
> The **minimum operating system** for uploading a *.pkg* file is macOS 10.14. Upload a *.intunemac* file to select an older minimum operating system.

### Select the app package file

1. In the **Add app** pane, click **Select app package file**. 
2. In the **App package file** pane, select the browse button. Then, select an macOS installation file with the extension *.intunemac* or *.pkg*.
   The app details will be displayed.
3. When you're finished, select **OK** on the **App package file** pane to add the app.

### Set app information

1. In the **App information** page, add the details for your app. Depending on the app that you chose, some of the values in this pane might be automatically filled in.
    - **Name**: Enter the name of the app as it appears in the company portal. Make sure all app names that you use are unique. If the same app name exists twice, only one of the apps appears in the company portal.
    - **Description**: Enter the description of the app. The description appears in the company portal.
    - **Publisher**: Enter the name of the publisher of the app.
    - **Minimum Operating System**: From the list, choose the minimum operating system version on which the app can be installed. If you assign the app to a device with an earlier operating system, it will not be installed.
    - **Ignore app version**: Select **Yes** to install the app if the app is not already installed on the device. Select **No** to only install the app when it is not already installed on the device, or if the deploying app's version number does not match the version that's already installed on the device.
    - **Install as managed**: Select **Yes** to install the Mac LOB app as a managed app on  supported devices (macOS 11 and higher). A macOS LOB app can only be installed as managed when the app distributable contains a single app without any nested packages and installs to the */Applications* directory. Managed line-of-business apps will be able to be removed using the **uninstall** assignment type on supported devices (macOS 11 and higher). In addition, removing the MDM profile removes all managed apps from the device. The default value is **No**.
    - **Included apps**: Review and edit the apps that are contained in the uploaded file. Included app bundle IDs and build numbers are used for detecting and monitoring app installation status of the uploaded file. The app listed first is used as the primary app in app reporting. <br>Included apps list should only contain the application(s) installed by the uploaded file in **Applications** folder on Macs. Any other type of file that is not an application or an application that is not installed to **Applications** folder should be removed from the **Included apps** list. If **Included apps** list contains files that are not applications or if all the listed apps are not installed, app installation status does not report success.<br>Mac Terminal can be used to look up and confirm the included app details of an installed app.<br>For example, to look up the bundle ID and build number of Company Portal, run the following:<br> *defaults read /Applications/Company\ Portal.app/Contents/Info CFBundleIdentifier*<br>Then, run the following:<br> *defaults read /Applications/Company\ Portal.app/Contents/Info CFBundleShortVersionString*
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
> Uninstall intend will only be displayed for LOB apps created with **Install as managed** set to **Yes**. For more information review **App information section** earlier on this article.

2. Click **Next** to display the **Review + create** page. 

## Step 4 - Review + create

1. Review the values and settings you entered for the app.
2. When you are done, click **Create** to add the app to Intune.

    The **Overview** blade for the line-of-business app is displayed.

The app you have created appears in the apps list where you can assign it to the groups you choose. For help, see [How to assign apps to groups](apps-deploy.md).

> [!NOTE]
> If the *.pkg* file contains multiple apps or app installers, then Microsoft Intune will only report that the *app* is successfully installed when all installed apps are detected on the device.

## Update a line-of-business app

[!INCLUDE [shared-proc-lob-updateapp](../includes/shared-proc-lob-updateapp.md)]

To update a line-of-business app deployed as a *.intunemac* file, you must increment the package `version` and `CFBundleVersion` string in the *packageinfo* file in your *.pkg* file.

To update a line-of-business app deployed as a *.pkg* file, you must increment the `CFBundleShortVersionString` of the *.pkg* file.

Intune will update the app when this schedule elapses, provided that any previous version of the app is still present on the device.

## Next steps

- The app you have created is displayed in the apps list. You can now assign it to the groups you choose. For help, see [How to assign apps to groups](apps-deploy.md).

- Learn more about the ways in which you can monitor the properties and assignment of your app. For more information, see [How to monitor app information and assignments](apps-monitor.md).

- Learn more about the context of your app in Intune. For more information, see [Overview of device and app lifecycles](../fundamentals/device-lifecycle.md)
