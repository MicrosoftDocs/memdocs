---
# required metadata

title: How to add macOS line-of-business apps to Microsoft Intune
titleSuffix:
description: Learn about how to add macOS line-of-business (LOB) apps to Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/23/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology:
ms.assetid: ef8008ac-8b85-4bfc-86ac-1f9fcbd3db76

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: aiwang
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# How to add macOS line-of-business (LOB) apps to Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Use the information in this article to help you add macOS line-of-business apps to Microsoft Intune. You must download an external tool to pre-process your *.pkg* files before you can upload your line-of-business file to Microsoft Intune. The pre-processing of your *.pkg* files must take place on a macOS device.

> [!NOTE]
> Starting with the release of macOS Catalina 10.15, prior to adding your apps to Intune, check to make sure your macOS LOB apps are notarized. If the developers of your LOB apps did not notarize their apps, the apps will fail to run on your users' macOS devices. For more information about how to check if an app is notarized, visit [Notarize your macOS apps to prepare for macOS Catalina](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Notarizing-your-macOS-apps-to-prepare-for-macOS/ba-p/808579).

> [!NOTE]
> While users of macOS devices can remove some of the built-in macOS apps like Stocks, and Maps, you cannot use Intune to redeploy those apps. If end users delete these apps, they must go to the app store, and manually re install them.

## Before your start

You must download an external tool, mark the downloaded tool as an executable, and pre-process your *.pkg* files with the tool before you can upload your line-of-business file to Microsoft Intune. The pre-processing of your *.pkg* files must take place on a macOS device. Use the Intune App Wrapping Tool for Mac to enable Mac apps to be managed by Microsoft Intune.

> [!IMPORTANT]
> The *.pkg* file must be signed using "Developer ID Installer" certificate, obtained from an Apple Developer account. Only *.pkg* files may be used to upload macOS LOB apps to Microsoft Intune. Conversion of other formats, such as *.dmg* to *.pkg* is not supported.
>

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
    
    - `IntuneAppUtil -c <source_file> -o <output_file> [-v]`<br>
    This command will wrap *.pkg* LOB app file to a *.intunemac* file.
    
    - `IntuneAppUtil -r <filename.intunemac> [-v]`<br>
    This command will extract the detected parameters and version for the created *.intunemac* file.

## Select the app type

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All apps** > **Add**.
3. In the **Select app type** pane, under the **Other** app types, select **Line-of-business app**.
4. Click **Select**. The **Add app** steps are displayed.

## Step 1 - App information

### Select the app package file

1. In the **Add app** pane, click **Select app package file**. 
2. In the **App package file** pane, select the browse button. Then, select an macOS installation file with the extension *.intunemac*.
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

The app you have created appears in the apps list where you can assign it to the groups you choose. For help, see [How to assign apps to groups](apps-deploy.md).

> [!NOTE]
> If the *.pkg* file contains multiple apps or app installers, then Microsoft Intune will only report that the *app* is successfully installed when all installed apps are detected on the device.

## Update a line-of-business app

[!INCLUDE [shared-proc-lob-updateapp](../includes/shared-proc-lob-updateapp.md)]

> [!NOTE]
> For the Intune service to successfully deploy a new *.pkg* file to the device you must increment the package `version` and `CFBundleVersion` string in the *packageinfo* file in your *.pkg* package.

## Next steps

- The app you have created is displayed in the apps list. You can now assign it to the groups you choose. For help, see [How to assign apps to groups](apps-deploy.md).

- Learn more about the ways in which you can monitor the properties and assignment of your app. For more information, see [How to monitor app information and assignments](apps-monitor.md).

- Learn more about the context of your app in Intune. For more information, see [Overview of device and app lifecycles](../fundamentals/device-lifecycle.md)
