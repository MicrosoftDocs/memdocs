---
# required metadata

title: Add a Windows line-of-business app to Microsoft Intune
titleSuffix:
description: Learn how to add a Windows line-of-business (LOB) app using Microsoft Intune.
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
ms.assetid: f81c5f82-5cfa-4b97-9f73-d6cf77c06896

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: manchen
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- M365-identity-device-management
- Windows
- highpri
---

# Add a Windows line-of-business app to Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

A line-of-business (LOB) app is one that you add from an app installation file. This kind of app is typically written in-house. The following steps provide guidance to help you add a Windows LOB app to Microsoft Intune.

> [!IMPORTANT]
> When deploying Win32 apps using an installation file with the .msi extension (packaged in an .intunewin file using the Content Prep Tool), consider using [Intune Management Extension](../apps/intune-management-extension.md). If you mix the installation of Win32 apps and line-of-business apps during Autopilot enrollment, the app installation may fail.  

## Select the app type

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All apps** > **Add**.
3. In the **Select app type** pane, under the **Other** app types, select **Line-of-business app**.
4. Click **Select**. The **Add app** steps are displayed.

## Step 1 - App information

### Select the app package file

1. In the **Add app** pane, click **Select app package file**. 
2. In the **App package file** pane, select the browse button. Then, select a Windows installation file with the extension **.msi**, **.appx**, or **.appxbundle**.
   The app details will be displayed.

    > [!NOTE]
    > The file extensions for Windows apps include **.msi**, **.appx**, **.appxbundle**, **.msix**, and **.msixbundle**. For more information about **.msix**, see [MSIX documentation](/windows/msix/) and [MSIX App Distribution](/windows/msix/desktop/managing-your-msix-deployment-enterprise).

3. When you're finished, select **OK** on the **App package file** pane to add the app.

### Set app information

1. In the **App information** page, add the details for your app. Depending on the app that you chose, some of the values in this pane might be automatically filled in.
    - **Name**: Enter the name of the app as it appears in the company portal. Make sure all app names that you use are unique. If the same app name exists twice, only one of the apps appears in the company portal.
    - **Description**: Enter the description of the app. The description appears in the company portal.
    - **Publisher**: Enter the name of the publisher of the app.
    - **App Install Context**: Select the install context to be associated with this app. For dual mode apps, select the desired context for this app. For all other apps, this is pre-selected based on the package and cannot be modified.
    - **Ignore app version**: Set to **Yes** if the app developer automatically updates the app. This option applies to mobile .msi apps and Windows apps with self-updating installers (such as Google Chrome).
    - **Command-line arguments**: Optionally, enter any command-line arguments that you want to apply to the .msi file when it runs.  An example is **/q**. Do not include the msiexec command or arguments, such as **/i** or **/x**, as they are automatically used. For more information, see [Command-Line Options](/windows/desktop/Msi/command-line-options). If the .MSI file needs additional command-line options consider using [Win32 app management](app-management.md).
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

The app that you created now appears in the list of apps. From the list, you can assign the apps to groups that you choose. For help, see [How to assign apps to groups](apps-deploy.md).

## Update a line-of-business app

[!INCLUDE [shared-proc-lob-updateapp](../includes/shared-proc-lob-updateapp.md)]

   > [!NOTE]
   > For the Intune service to successfully deploy a new APPX file to the device, you must increment the `Version` string in the AppxManifest.xml file in your APPX package.

## Configure a self-updating mobile MSI app to ignore the version check process

You can configure a known self-updating mobile MSI app to ignore the version check process.

Some MSI installer-based apps are automatically updated by the app developer or another update method. For these automatically updated MSI apps, you can configure the **Ignore app version** setting in the **App information** pane. When you switch this setting to **Yes**, Microsoft Intune will not enforce the app version that's installed on the Windows client.

This capability is useful to avoid getting into a race condition. For instance, a race condition can occur when the app is automatically updated by the app developer and is updated by Intune. Both might try to enforce a version of the app on a Windows client, which creates a conflict.

## Next steps

- The app that you created appears in the list of apps. You can now assign it to groups that you choose. For help, see [How to assign apps to groups](apps-deploy.md).

- Learn more about the ways in which you can monitor the properties and assignment of your app. See [How to monitor app information and assignments](apps-monitor.md).

- Learn more about the context of your app in Intune. See [Overview of the app lifecycle in Microsoft Intune](app-lifecycle.md).

- Learn more about Win32 apps. See [Win32 app management](apps-win32-app-management.md).
