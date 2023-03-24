---
# required metadata

title: Add Microsoft Store apps to Microsoft Intune
titleSuffix:
description: Learn about adding Microsoft Store apps to Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/22/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.technology:
ms.assetid: 07241b6d-86d8-4abb-83a2-3fc5feae5788

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: manchen
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Add Microsoft Store apps to Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Admins can browse, deploy, and monitor Microsoft Store applications inside Intune. Upon deployment, Intune automatically keeps the apps up to date when a new version becomes available. The Microsoft Store supports UWP apps, desktop apps packaged in *.msix*, and now Win32 apps packaged in *.exe* or *.msi* installers.  

> [!IMPORTANT]
> There are key improvements to the most recent Microsoft Store apps functionality over legacy functionality.
> Specifically, the following differences:
> - You can browse and search for store apps within Intune
> - You can install and uninstall with required app deployments
> - You can monitor the installation progress and results for store apps
> - Win32 store apps are supported (in preview)  
> - System context and user context are supported for UWP apps

## Prerequisites

To use Microsoft Store apps, be sure the following criteria are met:
- Client devices must support at least two core processors to successfully install and run Microsoft Store apps.
- Client device need to be able to support the [Intune Management Extension (IME)](..\apps\intune-management-extension.md) to install Microsoft Store apps.
- Client device need access to the Microsoft Store and the destination content to install Microsoft Store apps.

If you use Microsoft Intune to manage your apps (or use Group Policy), you can enable the **Only display the private store within the Microsoft Store** Group Policy setting to block the end user from using the store app.

:::image type="content" source="./media/store-apps-microsoft/store-apps-microsoft-01.png" alt-text="Only display the private store setting" border="true" :::

> [!NOTE]
> If you blocked the Microsoft Store app at the network level, the above Group Policy will not work.

## Add and deploy a Microsoft Store app

Use the following steps to add and deploy a Microsoft Store app.

### Step 1: Add an app from the Microsoft Store

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **All apps** > **Add**.
2. In **Select app type** pane, select **Microsoft Store app (new)** under the **Store app** section.
3. Choose **Select** at the bottom of the page to begin creating an app from the Microsoft Store.
    The app creation experience has three steps:
    - App information
    - Assignments
    - Review + create

### Step 2: Search the Microsoft Store

The Microsoft Store provides a large variety of apps designed to work on your Microsoft devices. Within Intune, you can search and add the apps you want to assign to your workforce at your organization. 

1. Select **Search the Microsoft Store app** to display the search panel which features a search bar and includes the following columns:
    -	**Name** – The name of the app.
    -	**Publisher** – The publisher of the app.
    -	**Type** – The app package type: Win32 or Universal Windows Platform (UWP).

2. In the search bar, type the name of the app that you want to find. You can also search by other app details, such as publisher, type, or store app ID.
   Once you search, a list of apps are displayed.
    > [!NOTE]
    > Specific Microsoft Store apps may not be displayed and available in Intune. Common reasons an app doesn't appear when searching within Intune include the following:
    > - The app is not available in your region
    > - The app is not available if there is an age restriction
    > - The app is a paid app, which is not supported
    > - The app is an Android app
    > - The app is a Microsoft Store for Business app that is not available publicly in the consumer store

3. Choose the app that you want to deploy and click **Select**. 
   The app information is presented with the selected app’s metadata. Specific fields are pre-populated.

    The following table shows the fields that are supported:
  
    |     Name   of the field    |     Description    |     Required    |
    |---|---|---|
    |     Name    | The name of the app is pre-populated from the store’s metadata and you have the choice to edit the field. Enter the name of the app as it appears in the Company Portal. Make sure all app names that you use are unique. If the same app name exists twice, only one of the apps appears in the company portal.   |     Required    |
    |     Description    | The description of the app is pre-populated from the store’s metadata and you have the choice to edit the field. The description appears in the Company Portal.          |     Required       |
    |     Publisher    |  The publisher of the app is pre-populated from the store’s metadata and you have the choice to edit the field.           |     Required    |
    |     Installer   Type    | The installer type of the application package is distinguished by either the UWP or Win32 installer types. For related information, see [Universal Windows Platform (UWP) apps](/windows/uwp/get-started/universal-application-platform-guide).                |     N/A   Pre-filled    |
    |     Package   Identifier     | The app’s unique ID in the Microsoft Store. This value is read-only and is displayed before Installer Type in the UI.   |     N/A   Pre-filled    |
    |     Install   behavior    | The install behavior of the app. If the app to be installed has the option of either **System** or **User** install behaviors, you must ensure that the installation works on devices as expected. NOTE: If the option is greyed out, the specific store application only supports the selected install behavior.     |     Admin must select **System** or **User**     |
    |     Category       | Optionally, select one or more of the built-in app categories, or select a category that you created. Categories make it easier for users to find the app when they browse through the Company Portal.          |     Optional       |
    |     Show   this as a featured app in the Company Portal    |  Display the app prominently on the main page of the company portal when users browse for apps.    |     Admin must select Yes or No    |
    |     Information   URL     |     Optionally, enter the URL of a website that   contains information about this app. The URL appears in the company portal.          |     Optional    |
    |     Privacy   URL     |     Optionally, enter the URL of a website that   contains privacy information for this app. The URL appears in the company   portal.          |     N/A   Pre-filled    |
    |     Developer    |     Optionally, enter the name of the app developer.          |     Optional    |
    |     Owner     |     Optionally, enter a name for the owner of this app. An example is **HR department**.          |     Optional    |
    |     Notes     |     Enter any notes that you want to associate   with this app.          |     Optional    |
    |     Logo    |     Upload an icon that is associated with the   app. This icon is displayed with the app when users browse through the company   portal.          |     Optional       |
    
4. Select **Next** after you have finished populating the fields.

### Step 3: Creating assignments

You can choose how you want to assign Microsoft Store apps to users and devices. 

The following table provides assignment type details:

|     Assignment type    |     Assignment options    |     Description    |
|---|---|---|
|     Required       | Add group, Add all users, Add all devices    | The app is installed on devices in the selected groups.          |
|     Available for enrolled devices    | Add group, Add all users    | Users install the app from the Company Portal app or the Company Portal website.          |
|     Uninstall    | Add group, Add all users, Add all devices    | The app is uninstalled from devices in the selected groups.          |

1. Select **Add group** and assign the groups that will use this app.
2. On the **Select groups** pane, select groups to assign based on users or devices.
3. After you select your groups, choose whether to set **End user notifications**, **Restart grace period**, and **Installation deadline**. 
4. If you don't want the app assignment to affect groups of users, select **Included** under the **Filter mode** column. In the **Edit assignment** pane, change the **Filter mode** value from **Included** to **Excluded**. Select **OK** to close the **Edit assignment** pane.
5. Select **Next** to display the **Review + create** page after you finish setting the assignments for the apps.

### Step 4: Review and create

1. Review the values and settings that you entered for the app. Verify that you configured the app information correctly.
2. Select **Create** to add the app to Intune.

## App update

Apps that are deployed from the Microsoft Store are automatically kept up to date to the latest version of the app. For this feature to work properly for UWP apps, the **Turn off Automatic Download and Install of updates** should not be enabled.

## Microsoft Store Win32 apps

> [!IMPORTANT]
> Win32 apps that are in the Microsoft Store are currently in preview. Not all Win32 apps will be available or searchable. The Win32 apps that are in preview will be identifiable with **Win32** and a banner.
> 
> Third party vendors or publishers that add Win32 apps to the Microsoft Store are responsible for hosting their own content in their respective infrastructure. If your devices are behind a firewall, please reach out to application owner to understand and confirm network requirements.

### Intune management of Microsoft Store Win32 apps

When a Microsoft Store Win32 app is published to a device as **Required**, but it is already installed (either manually or via the [Microsoft Store for Business](../apps/windows-store-for-business.md)), Intune will take over the management of the application. 

For available Microsoft Store Win32 apps, as well as UWP apps, the end user must click install in the Company Portal before Intune takes over the management of the application. Intune will not attempt to re-install the app.

The Microsoft Store supports Win32 app types including **.exe** and **.msi** installers. These apps have external content sourcing hosted by the app publisher. Based on their installer definition in the store, each Win32 app supports either **User** or **System** context installation.For related information, see [Traditional desktop apps in the Microsoft Store on Windows](https://developer.microsoft.com/microsoft-store/desktop-apps).

## Microsoft Store UWP apps
In addition to user context, you can deploy Universal Windows Platform (UWP) apps from the **Microsoft Store app (new)** in system context. If a provisioned *.appx* app is deployed in system context, the app will auto-install for each user that logs in. If an individual end user uninstalls the user context app, the app will still show as installed because it is still provisioned. In addition, the app must not already be installed for any users on the device. Our general recommendation is to not mix install contexts when deploying apps.

## Store group policies restrictions

Some **Store Group Policies** may affect app deployments from the Microsoft Store. 

The following table provides details about how app deployment may be affected by **Store Group Policies**:

|     Store Group   Policies    |     Desired   setting    |
|---|---|
|     Store\Disable all apps from the Microsoft   Store     | **Not configured** or **Enabled**. Set to **Enabled** if wish to prevent end users from blocking the scenario.          |
|     Store\Turn off Automatic Download and   Install of updates    | **Not configured** or **Disabled**. Set to **Disabled** if you need to prevent end users from blocking the scenario.          |
|     Desktop App Installer\Enable App Installer   Microsoft Store Source    | **Not configured** or **Enabled**. Set to **Enabled** if wish to prevent end users from blocking the scenario.          |
|     Desktop App Installer\Enable App Installer    | **Not configured** or **Enabled**. Set to **Enabled** if wish to prevent end users from blocking the scenario.          |
|     Store\Turn off the Store application    | **Not configured** or **Disabled**. Set to **Disabled** if you need to prevent end users from blocking the scenario.          |

> [!NOTE]
> If you would like to block installation of arbitrary applications from the Store application by the end user without blocking the Intune and Windows Package Manager store integration, set **Store\Only display the private store within the Microsoft Store** to **Enabled**.

## Unsupported functionality for Microsoft Store apps

The following capabilities aren't supported by Microsoft Store apps:

1. Ability to install Microsoft Store apps during Enrollment Status Page. Apps deployed using Microsoft Store app will install after enrollment status page has completed. The ability to install Microsoft Store apps during Enrolment Status Page is coming in a future release.
2. Any app that has an ARM64 installer is not supported.

## Next steps

- [Assign apps to groups](apps-deploy.md)
