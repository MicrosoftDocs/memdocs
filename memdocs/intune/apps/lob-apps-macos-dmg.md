---
# required metadata

title: Add a macOS DMG app to Microsoft Intune 
titleSuffix:
description: Add a macOS DMG app to Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/17/2022
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
ms.custom: intune-azure
ms.collection:
- M365-identity-device-management
- macOS
- highpri
---

# Add a macOS DMG app to Microsoft Intune 

> [!NOTE]
> The feature is in public preview. 

Use the information in this article to help you add a macOS DMG app to Microsoft Intune. A DMG app is a disk image file that contains one or more applications within it. Many common applications for macOS are available in DMG format. For more information about how to create a disk image file, see [Apple’s website](https://support.apple.com/guide/disk-utility/create-a-disk-image-dskutl11888/mac). 

> [!NOTE]
> The DMG file must contain one or more files with .app extensions. DMG files containing other types of installer files will not be installed. 

## Prerequisites

The following prerequisites must be met before a macOS DMG app is installed on macOS devices.
- Devices are managed by Intune.
- DMG app is smaller than 2GB in size.
- The [Microsoft Intune management agent for macOS](../apps/lob-apps-macos-agent.md) is installed. 

## Important considerations for deploying DMG apps

A single DMG should only contain a single application file or multiple application files that are dependent on one another. The containing application files can be listed under the **Included apps** section in the **Detection rules** tab in order starting with the parent app to be used in reports. 

It is not recommended that multiple apps that are not dependent on each other are installed using the same DMG file. If multiple independent apps are deployed using the same DMG app, failure to install one app will cause other apps to be re-installed. In this case, monitoring reports consider the DMG installation a failure as well.

## Select the app type
1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All apps** > **Add**.
3. In the **Select app type** pane, under the **Other** app types, select **macOS app (DMG)**.
4. Click **Select**. The **Add app** steps are displayed.

## Step 1 – App information

Select the app package file:
1. In the **Add app** pane, click **Select app package file**.
2. In the **App package file** pane, select the browse button. Then, select a macOS DMG file with the extension *.dmg*. The app details will be displayed.
3. When you're finished, select **OK** on the **App package file** pane to add the app.

### Set app information

1. In the **App information** page, add the details for your app. Depending on the app that you chose, some of the values in this pane might be automatically filled in.

    - **Name**: Enter the name of the app as it appears in the policy name and company portal. Make sure all app names that you use are unique. If the same app name exists twice, only one of the apps appears in the company portal.
    - **Description**: Enter the description of the app. The description appears in the company portal.
    - **Publisher**: Enter the name of the publisher of the app.
    - **Category**: Select one or more of the built-in app categories, or select a category that you created. Categories make it easier for users to find the app when they browse through the company portal.
    - **Information URL**: Optionally, enter the URL of a website that contains information about this app. The URL appears in the company portal.
    - **Privacy URL**: Optionally, enter the URL of a website that contains privacy information for this app. The URL appears in the company portal.
    - **Developer**: Optionally, enter the name of the app developer.
    - **Owner**: Optionally, enter a name for the owner of this app. An example is HR department.
    - **Notes**: Enter any notes that you want to associate with this app.
    - **Logo**: Upload an icon that is associated with the app. This icon is displayed with the app when users browse through the company portal.
2. Click **Next** to set the requirements.

## Step 2 – Requirements

You can choose the minimum operating system required to install this app.

**Minimum Operating System**: From the list, choose the minimum operating system version on which the app can be installed. If you assign the app to a device with an earlier operating system, it will not be installed.

## Step 3 – Detection rules

You can use detection rules to choose how an app installation is detected on a managed macOS device.

**Ignore app version**: Select **Yes** to install the app if the app is not already installed on the device. This will only look for the presence of the app bundle ID. For apps that have an auto-update mechanism, select **Yes**. Select **No** to install the app when it is not already installed on the device, or if the deploying app's version number does not match the version that's already installed on the device.

**Included apps**: Provide the apps that are contained in the uploaded file. Included app bundle IDs and build numbers are used for detecting and monitoring app installation status of the uploaded file. Included apps list should only contain the application(s) installed by the uploaded file in **Applications** folder on Macs. Any other type of file that is not an application or an application that is not installed to **Applications** folder should be excluded from the **Included apps** list. If **Included apps** list contains files that are not applications or if all the listed apps are not installed, app installation status does not report success.

> [!NOTE]
> - The first app on the Included apps list is used for identifying the app when multiple apps are present in the DMG file. 
> - Mac Terminal can be used to lookup and confirm the included app details of an installed app.
>   For example, to look up the bundle ID and build number of Company Portal, run the following:
> 
>   ```defaults read /Applications/Company\ Portal.app/Contents/Info CFBundleIdentifier```
> 
>   Then, run the following:
> 
>   ```defaults read /Applications/Company\ Portal.app/Contents/Info CFBundleVersion```
>
> - Alternatively, the `CFBundleIdentifier` and `CFBundleVersion` can be found under the ```<app_name>.app/Contents/Info.plist``` file of a mounted DMG file on a Mac.

## Step 4 – Select scope tags (optional)

You can use scope tags to determine who can see client app information in Intune. For full details about scope tags, see [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md).
    1. Click Select scope tags to optionally add scope tags for the app.
    2. Click Next to display the Assignments page.

## Step 5 - Assignments

1. Select the **Required group assignments** for the app. For more information, see [Add groups to organize users and devices](../fundamentals/groups-add.md) and [Assign apps to groups with Microsoft Intune](../apps/apps-deploy.md).
2. Click **Next** to display the **Review + create** page.

## Step 6 – Review + create

1. Review the values and settings you entered for the app.
2. When you are done, click **Create** to add the app to Intune. 
   The **Overview** pane for the macOS DMG app is displayed.

The app you have created appears in the apps list where you can assign it to the groups you choose. For help, see [How to assign apps to groups](../apps/apps-deploy.md).

> [!NOTE]
> If the *.dmg* file contains multiple apps, then Microsoft Intune will only report that the app is successfully installed when all installed apps are detected on the device.

## Next steps

- The app you have created is displayed in the apps list. You can now assign it to the groups you choose. For help, see [How to assign apps to groups](apps-deploy.md).
- Learn more about the ways in which you can monitor the properties and assignment of your app. For more information, see [How to monitor app information and assignments](apps-monitor.md).
- Learn more about the context of your app in Intune. For more information, see [Overview of device and app lifecycles](../fundamentals/device-lifecycle.md)

## Known issues

- **"Uninstall" and "Available for enrolled devices" assignment types are not available**: only "Required" assignment type is currently supported. 
- **"Collect logs" action is unavailable during preview**: log collection feature on macOS apps (DMG) is unavailable during preview. 
- **Errors might not show details during preview**: some errors you encounter may only show "Failed" status with an error code and not provide additional details.
- **App upgrade fails to install**: Updating an app that has the same bundle ID as an existing app in Applications folder fails to install. 
- **DMG apps report once after deployment**: Assigned DMG apps report back on initial deployment only. These apps will not report back again during preview.
- **Some DMG apps may display a warning to end-users on launch**: Apps downloaded from the internet and deployed using Intune may show a warning to end-users when launched. End-users can click "Open" on the dialog to continue opening the app.

  ![DMG apps may display a warning to end-users on launch](./media/lob-apps-macos-dmg/lob-apps-macos-dmg-01.png)

- **Some app icons may not display immediately after installation**: some app icons may take some time after installation to start displaying on the installed device.
- **Monitoring reports only show error code**: failed app installations only show an error code in "device status" monitoring reports. To show error details, refresh the browser window or refer to the table in the Troubleshooting section.


## Troubleshooting

macOS app installation may not be successful due to any of the following reasons provided in the table below. To resolve these errors, follow the remediation steps. If the app remains assigned, failed installations are retried at the next agent check-in.

| Error code | Error message | Remediation steps |
|------------|---------------|-------------------|
| 0x87D30137 | The device doesn't meet the minimum OS requirement set by the admin. | Update macOS to the minimum OS version required by the admin. |
| 0x87D3013E | The DMG file doesn't contain any supported app. It must contain at least one .app file. | Ensure that the uploaded file contains one or more .app files. |
| 0x87D30139 | The DMG file couldn't be mounted for installation. Check the DMG file if the error persists. | Try manually mounting the DMG file to verify that the volume loads successfully. |
| 0x87D3013B | The app couldn't be installed to the Applications directory. Sync the device to retry installing the app. | Ensure that the device can install apps locally to the Applications directory. |
| 0x87D3012F, 0x87D30130, 0x87D30133, 0x87D30134, 0x87D30136,| The app couldn't be installed due to an internal error. Contact Intune support if the error persists. | Something went wrong while installing the app using Intune. Try installing the app manually or try creating a new macOS app profile containing the app. Contact Intune support if the error persists. |
| 0x87D30131, 0x87D30132 | The app couldn't be downloaded. Sync the device to retry installing the app. | Something went wrong while downloading the app. This may happen if the network is poor or the app size is large. |
| 0x87D30135 | The app couldn't be installed due to a device error. Sync the device to retry installing the app. | This could be due to insufficient disk space or the app could not be written to the folder. Ensure that the device can install apps to the Applications folder. |
| 0x87D3013A | The physical resources of this disk have been exhausted. | This could be due to hard disk running out of space or binaries  of the installation files are corrupt. Fix the Hard disk space and restart the Microsoft Intune Management Extension service and try again. |
