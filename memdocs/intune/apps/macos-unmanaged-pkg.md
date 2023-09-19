---
# required metadata

title: Add an unmanaged macOS PKG app to Microsoft Intune
titleSuffix:
description: Learn about how to add an unmanaged macOS PKG app to Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/13/2023
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
- tier1
- M365-identity-device-management
- macOS
- highpri
---

# Add an unmanaged macOS PKG app to Microsoft Intune (public preview)

> [!NOTE]
> This feature is in public preview. For more information, go to [Public preview in Microsoft Intune](../fundamentals/public-preview.md).

Use the information in this article to help you add an unmanaged macOS PKG app to Microsoft Intune. To deploy a managed PKG app, see [How to add macOS line-of-business (LOB) apps to Microsoft Intune.](../apps/lob-apps-macos.md) 

## Prerequisites

The following prerequisites must be met before an unmanaged macOS PKG app is installed on macOS devices.

- Devices are managed by Intune.
- The PKG file is smaller than 2GB in size.
- The [Microsoft Intune management agent for macOS](../apps/lob-apps-macos-agent.md) version 2308.006 or greater is installed.
- The PKG file successfully runs using the `installer` command in Terminal.

## Important considerations for deploying PKG apps

The unmanaged macOS PKG app-type can install the following types of PKG apps:

- Non-flat packages with a hierarchical structure
- Component packages
- Unsigned packages
- Packages without a payload
- Packages that install apps outside `/Applications/`
- Custom packages with scripts

> [!NOTE]
> These types of PKG apps may not successfully deploy using the managed LOB app-type.

The containing app files can be listed under the **Included apps** section in the **Detection rules** tab in order, starting with the parent app to be used in reports.

## Select the app type

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All apps** > **Add**.
3. In the **Select app type** pane, under the **Other** app types, select **macOS app (PKG)**.
4. Click **Select**. The **Add app** steps are displayed.

## Step 1 – App information

Select the app package file:

1. In the **Add app** pane, click **Select app package file**.
2. In the **App package file** pane, select the browse button. Then, select a macOS PKG file with the extension *.pkg*. The app details will be displayed.
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

## Step 2 – Program
You can optionally configure a pre-install script and a post-install script to customize the app install.

**Pre-install script**: Provide a script that runs before the app is installed. Only when the pre-install script returns zero (indicating success), the app proceeds to install. If the pre-install script returns a non-zero code (indicating failure), the app does not install and reports its installation status as "failed". The pre-install script runs again for failed installations at the next device check-in (sync).

**Post-install script**: Provide a script that runs after the app installs successfully. If provided, the post-install script runs after a successful app installation. Irrespective of the post-install script run status, an installed app reports its installation status as "success".

> [!NOTE]
> - Each pre-install or post-install script must be less than 5121 characters long.
> - The Microsoft Intune management agent for macOS version 2309.007 or greater is required to configure pre-install and post-install scripts for macOS PKG apps.
> - For more details on configuring pre-install and post-install scripts, refer to [Prerequisites of shell scripts](../apps/macos-shell-scripts.md#prerequisites).

## Step 3 – Requirements

You can choose the minimum operating system required to install this app.

**Minimum Operating System**: From the list, choose the minimum operating system version on which the app can be installed. If you assign the app to a device with an earlier operating system, it will not be installed.

## Step 4 – Detection rules

You can use detection rules to choose how an app installation is detected on a managed macOS device.

**Ignore app version**: Select **Yes** to install the app if the app is not already installed on the device. This will only look for the presence of the app bundle ID. For apps that have an auto-update mechanism, select **Yes**. Select **No** to install the app when it is not already installed on the device, or if the deploying app's version number does not match the version that's already installed on the device.

**Included apps**: Provide the apps that are contained in the uploaded file. Included app bundle IDs and build numbers are used for detecting and monitoring app installation status of the uploaded file. Included apps list should only contain the application(s) installed by the uploaded file. Any other type of file that is not an application should be excluded from the **Included apps** list. If **Included apps** list contains files that are not applications or if all the listed apps are not installed, app installation status does not report success.

> [!NOTE]
>
> - The first app on the Included apps list is used for identifying the app when multiple apps are present in the PKG file. 
> - the `CFBundleIdentifier` and `CFBundleShortVersionString` can be found under the ```<app_name>.app/Contents/Info.plist``` file of an installed app on a Mac. <br> Alternatively, Mac Terminal can be used to look up and confirm the included app details of an installed app at a known location.<br>For example, to look up the bundle ID and build number of Company Portal, run the following:<br> `defaults read /Applications/Company\ Portal.app/Contents/Info CFBundleIdentifier`<br>Then, run the following:<br> `defaults read /Applications/Company\ Portal.app/Contents/Info CFBundleShortVersionString`  

## Step 5 – Select scope tags (optional)

You can use scope tags to determine who can see client app information in Intune. For full details about scope tags, see [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md).
    1. Click **Select scope tags** to optionally add scope tags for the app.
    2. Click **Next** to display the **Assignments** page.

## Step 6 - Assignments

You can select the **Required** group assignment for the app. For more information, see [Add groups to organize users and devices](../fundamentals/groups-add.md) and [Assign apps to groups with Microsoft Intune](../apps/apps-deploy.md).

> [!NOTE]
> A macOS app deployed using Intune agent will not automatically be removed from the device when the device is retired. The app and data it contains will remain on the device. It is recommended that the app is removed prior to retiring the device.

1. For the specific app, select **Required** assignment type.
2. Click **Next** to display the **Review + create** page.

## Step 7 – Review + create

1. Review the values and settings you entered for the app.
2. When you are done, click **Create** to add the app to Intune.
   The **Overview** pane for the macOS PKG app is displayed.

The app you have created appears in the apps list where you can assign it to the groups you choose. For help, see [How to assign apps to groups](../apps/apps-deploy.md).

## Known issues

- **"Available for enrolled devices" and "uninstall" assignment type are not available**: Only **Required** assignment type is currently supported.

## Troubleshooting

macOS app installation may not be successful due to any of the following reasons provided in the table below. To resolve these errors, follow the remediation steps. If the app remains assigned, failed installations are retried at the next agent check-in.

| Error code | Error message | Remediation steps |
|------------|---------------|-------------------|
| 0x87D30137 | The device doesn't meet the minimum OS requirement set by the admin. | Update macOS to the minimum OS version required by the admin. |
| 2016214710 | The pre-install script provided by the admin failed. | This might be expected if the pre-install script is waiting for a condition to become true before the app install can proceed. The failed pre-install script will be tried again at the next device check-in. Check the pre-install script if the error persists. |
| 0x87D3012F, 0x87D30130, 0x87D30133, 0x87D30134, 0x87D30136,| The app couldn't be installed due to an internal error. Contact Intune support if the error persists. | Something went wrong while installing the app using Intune. Try installing the app manually or try creating a new macOS app profile containing the app. Contact Intune support if the error persists. |

Note that post-install script failure is not reported. A successful app installation followed by a failed post-install script will report the app installation status as "success".

## Next steps

- The app you have created is displayed in the apps list. You can now assign it to the groups you choose. For help, see [How to assign apps to groups](apps-deploy.md).
- Learn more about the ways in which you can monitor the properties and assignment of your app. For more information, see [How to monitor app information and assignments](apps-monitor.md).
- Learn more about the context of your app in Intune. For more information, see [Overview of device and app lifecycles](../fundamentals/device-lifecycle.md)
