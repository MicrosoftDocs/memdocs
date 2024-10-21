---
# required metadata

title: Add Microsoft Store apps to Microsoft Intune
titleSuffix:
description: Learn about adding Microsoft Store apps to Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/07/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.assetid: 07241b6d-86d8-4abb-83a2-3fc5feae5788

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
- highpri
---

# Add Microsoft Store apps to Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Admins can browse, deploy, and monitor Microsoft Store applications inside Intune. Upon deployment, Intune automatically keeps the apps up to date when a new version becomes available. The Microsoft Store supports Universal Windows Platform (UWP) apps, desktop apps packaged in `.msix`, and now Win32 apps packaged in `.exe` or `.msi` installers.  

> [!IMPORTANT]
> There are key improvements to the most recent Microsoft Store apps functionality over legacy functionality.
> Specifically, the following differences:
>
> - You can browse and search for store apps within Intune
> - You can install and uninstall with required app deployments
> - You can monitor the installation progress and results for store apps
> - Win32 store apps are supported (in preview)  
> - System context and user context are supported for UWP apps
>   - When a device is enrolled by being Microsoft Entra registered, system context must be used.

## Prerequisites

To use Microsoft Store apps, be sure the following criteria are met:

- Client devices must support at least two core processors to successfully install and run Microsoft Store apps.
- Client device need to be able to support the [Intune Management Extension (IME)](..\apps\intune-management-extension.md) to install Microsoft Store apps.
- Client device need access to both the Microsoft Store and the destination content to install Microsoft Store apps. For more information, see [Microsoft Store proxy configuration](../fundamentals/intune-endpoints.md#microsoft-store).

## Add and deploy a Microsoft Store app

An [Intune administrator](../fundamentals/users-add.md#types-of-administrators) can use the following steps to add and deploy a Microsoft Store app. 

> [!NOTE]
> To ensure the Company Portal app is successfully installed on your end user's device, you may need to set the **Install behavior** to **User** and the deployment Entra ID group as **Only devices**. 

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

> [!IMPORTANT]
> There is no age restriction when searching for apps in the Microsoft Store.

1. Select **Search the Microsoft Store app** to display the search panel which features a search bar and includes the following columns:

    - **Name** – The name of the app.
    - **Publisher** – The publisher of the app.
    - **Type** – The app package type: Win32 or Universal Windows Platform (UWP).

2. In the search bar, type the name of the app that you want to find. You can also search by other app details, such as publisher, type, or store app ID.
   Once you search, a list of apps are displayed.

    > [!NOTE]
    > Specific Microsoft Store apps may not be displayed and available in Intune. Common reasons an app doesn't appear when searching within Intune include the following:
    >
    > - The app is not available in US region.
    > - The app is a paid app, which is not supported.
    > - The app platform isn't support in the Microsoft Store.

3. Choose the app that you want to deploy and choose **Select**.

   The app information is presented with the selected app's metadata. Specific fields are prepopulated.

    The following table shows the fields that are supported:
  
    |     Name   of the field    |     Description    |     Required    |
    |---|---|---|
    |     Name    | The name of the app is prepopulated from the store's metadata and you have the choice to edit the field. Enter the name of the app as it appears in the Company Portal. Make sure all app names that you use are unique. If the same app name exists twice, only one of the apps appears in the company portal.   |     Required    |
    |     Description    | The description of the app is prepopulated from the store's metadata and you have the choice to edit the field. The description appears in the Company Portal.          |     Required       |
    |     Publisher    |  The publisher of the app is prepopulated from the store's metadata and you have the choice to edit the field.           |     Required    |
    |     Installer   Type    | The installer type of the application package is the UWP or Win32 installer types. For related information, see [Universal Windows Platform (UWP) apps](/windows/uwp/get-started/universal-application-platform-guide).                |     N/A   Prefilled    |
    |     Package   Identifier     | The app's unique ID in the Microsoft Store. This value is read-only and is displayed before Installer Type in the UI.   |     N/A   Prefilled    |
    |     Install   behavior    | The install behavior of the app. If the app to be installed has the option of either **System** or **User** install behaviors, you must ensure that the installation works on devices as expected. NOTE: If the option is greyed out, the specific store application only supports the selected install behavior.     |     Admin must select **System** or **User**     |
    |     Category       | Optionally, select one or more of the built-in app categories, or select a category that you created. Categories make it easier for users to find the app when they browse through the Company Portal.          |     Optional       |
    |     Show   this as a featured app in the Company Portal    |  Display the app prominently on the main page of the company portal when users browse for apps.    |     Admin must select Yes or No    |
    |     Information   URL     |     Optionally, enter the URL of a website that   contains information about this app. The URL appears in the company portal.          |     Optional    |
    |     Privacy   URL     |     Optionally, enter the URL of a website that   contains privacy information for this app. The URL appears in the company   portal.          |     N/A   Prefilled    |
    |     Developer    |     Optionally, enter the name of the app developer.          |     Optional    |
    |     Owner     |     Optionally, enter a name for the owner of this app. An example is **HR department**.          |     Optional    |
    |     Notes     |     Enter any notes that you want to associate   with this app.          |     Optional    |
    |     Logo    |     Upload an icon that is associated with the   app. This icon is displayed with the app when users browse through the company   portal.          |     Optional       |

4. Select **Next** after you have finished populating the fields.

### Step 3: Creating assignments

You can choose how you want to assign Microsoft Store apps to users and devices.

> [!NOTE]
> If you assign an app to a device that is located in a region where that app is not supported, the app will not install on the device. However, if the device is moved to a region that supports the app, the app will install on the device. 

The following table provides assignment type details:

|     Assignment type    |     Assignment options    |     Description    |
|---|---|---|
|     Required       | Add group, Add all users, Add all devices    | The app is installed on devices in the selected groups.          |
|     Available for enrolled devices    | Add group, Add all users    | Users install the app from the Company Portal app or the Company Portal website.          |
|     Uninstall    | Add group, Add all users, Add all devices    | The app is uninstalled from devices in the selected groups.          |

1. Select **Add group** and assign the groups that use this app.
2. On the **Select groups** pane, select groups to assign based on users or devices.
3. After you select your groups, choose whether to set **End user notifications**, **Restart grace period**, and **Installation deadline**.
4. If you don't want the app assignment to affect groups of users, select **Included** under the **Filter mode** column. In the **Edit assignment** pane, change the **Filter mode** value from **Included** to **Excluded**. Select **OK** to close the **Edit assignment** pane.
5. Select **Next** to display the **Review + create** page after you finish setting the assignments for the apps.

### Step 4: Review and create

1. Review the values and settings that you entered for the app. Verify that you configured the app information correctly.
2. Select **Create** to add the app to Intune.

## App update

Apps that are deployed from the Microsoft Store are automatically kept up to date to the latest version of the app. For this feature to work properly for UWP apps, the **Turn off Automatic Download and Install of updates** shouldn't be enabled.

## Microsoft Store Win32 apps

> [!IMPORTANT]
> Win32 apps that are in the Microsoft Store are currently in preview. Not all Win32 apps will be available or searchable. The Win32 apps that are in preview will be identifiable with **Win32** and a banner.
>
> Third party vendors or publishers that add Win32 apps to the Microsoft Store are responsible for hosting their own content in their respective infrastructure. If your devices are behind a firewall, please reach out to application owner to understand and confirm network requirements.

### Intune management of Microsoft Store Win32 apps

When a Microsoft Store Win32 app is published to a device as **Required**, but the app is not detected due to a mismatch of the installed version or context, Intune will reinstall the app in the targeted installation context.

For available Microsoft Store Win32 apps, the end user must select install in the Company Portal before Intune takes over management and automatic updates for the app. Intune doesn't try to reinstall the app.

The Microsoft Store supports Win32 app types including **.exe** and **.msi** installers. These apps have external content sourcing hosted by the app publisher. Based on their installer definition in the store, each Win32 app supports either **User** or **System** context installation.For related information, see [Traditional desktop apps in the Microsoft Store on Windows](https://developer.microsoft.com/microsoft-store/desktop-apps).

> [!NOTE]
> Microsoft Store Win32 apps are kept up to date by Intune, therefore in order for the app to be updated it must be assigned in Intune. App updates are not affected by the Store's update policies.

## Microsoft Store UWP apps

In addition to user context, you can deploy Universal Windows Platform (UWP) apps from the **Microsoft Store app (new)** in system context. If a provisioned `.appx` app is deployed in system context, the app autoinstalls for each user that logs in. If an individual end user uninstalls the user context app, the app still shows as installed because it's still provisioned. In addition, the app must not already be installed for any users on the device. Our general recommendation is to not mix install contexts when deploying apps.

> [!NOTE]
> Assigning a UWP app using the "Microsoft Store app (new)" type with the installation behavior set as "System" to a device which already has that app installed will result in this error: "The application was not detected after installation completed successfully (0x87D1041C)". However, the app will still install correctly on the device.
>
> When a device is enrolled as Microsoft Entra registered, the installation behavior should be set to "System". If an app with the installation behavior set to "User" is assigned as **Available**, the end user will receive the following error when selecting install in the Company Portal: "Requirements Not Met". Make sure the device is _joined_ to Azure, or use System context to rectify this situation. 
> 
> UWP apps are kept up to date by the Store. The UWP app will stay up to date with or without Intune assignment once it is installed, unless the Store policy is set to block auto-update.

## Common Store policy settings and their impact on Microsoft Store apps

Some Store policies may affect app deployments from the Microsoft Store. The following policy list provides details on how some Store policies can affect app deployments.

For more information on the Microsoft Store integration with Intune due to the Microsoft Store for Business and Education retirement, go to the [Adding your Microsoft Store for Business and Education apps to the Microsoft Store in Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/adding-your-microsoft-store-for-business-and-education-apps-to/ba-p/3788506) blog post.

- **Disable all apps from the Microsoft Store** policy

  - Recommended values: **Not configured** or **Enabled**. To prevent end users from blocking or turning off this feature, set the value to **Enabled**.

  | CSP | Intune | On-premises GPO |
  | --- | --- | --- |
  | [ApplicationManagement/DisableStoreOriginatedApps](/windows/client-management/mdm/policy-csp-applicationmanagement#disablestoreoriginatedapps) | [Settings Catalog](../configuration/settings-catalog.md) &#124; Microsoft App Store > Disable Store Originated Apps | Administrative Templates > Windows Components > Store |

- **Turn off Automatic Download and Install of updates** policy

  - Recommended values: **Not configured** or **Disabled**. To prevent end users from blocking or turning off this feature, set the value to **Disabled**.

  | CSP | Intune | On-premises GPO |
  | --- | --- | --- |
  | [ApplicationManagement/AllowAppStoreAutoUpdate](/windows/client-management/mdm/policy-csp-applicationmanagement#allowappstoreautoupdate) | [Settings Catalog](../configuration/settings-catalog.md) &#124; Microsoft App Store > Allow apps from the Microsoft app store to auto update | Administrative Templates > Windows Components > Store |

- **Enable App Installer Microsoft Store Source** policy

  - Recommended values: **Not configured** or **Enabled**. To prevent end users from blocking or turning off this feature, set the value to **Enabled**.

  | CSP | Intune | On-premises GPO |
  | --- | --- | --- |
  | [DesktopAppInstaller/EnableMicrosoftStoreSource](/windows/client-management/mdm/policy-csp-desktopappinstaller#enablemicrosoftstoresource) | Not built in; use a [custom configuration profile](../configuration/custom-settings-configure.md). | Administrative Templates > Windows Components > Desktop App Installer |

- **Enable App Installer** policy

  - Recommended values: **Not configured** or **Enabled**. To prevent end users from blocking or turning off this feature, set the value to **Enabled**.

  | CSP | Intune | On-premises GPO |
  | --- | --- | --- |
  | [DesktopAppInstaller/EnableAppInstaller](/windows/client-management/mdm/policy-csp-desktopappinstaller#enableappinstaller) | Not built in; use a [custom configuration profile](../configuration/custom-settings-configure.md). | Administrative Templates > Windows Components > Desktop App Installer |

- **Turn off the Store application** policy: Your options:

  - **Not configured**: This policy isn't changed or updated. By default, the OS might allow end users to install arbitrary store apps outside of Intune.

  - **Enabled**: When enabled, this setting:

    - Blocks end users from installing arbitrary apps from the Microsoft Store app.
    - Blocks end users from using the Microsoft Store to manually install app updates.

  - **Disabled**: When disabled, this setting:

    - Allows end users to install arbitrary apps from the Microsoft Store app.
    - Allows end users to use the Microsoft Store to manually install app updates.

  > [!NOTE]
  > The Windows Package Manager command-line tool `winget.exe` is not affected by this policy.

  | CSP | Intune | On-premises GPO |
  | --- | --- | --- |
  | [ADMX_WindowsStore/RemoveWindowsStore_1](/windows/client-management/mdm/policy-csp-admx-windowsstore#removewindowsstore_1) <br/>[ADMX_WindowsStore/RemoveWindowsStore_2](/windows/client-management/mdm/policy-csp-admx-windowsstore#removewindowsstore_2) | [Settings Catalog](../configuration/settings-catalog.md) </br>[Administrative templates](../configuration/administrative-templates-windows.md) | **Windows Components** > **Store** > **Turn off the Store Application** <br/> **Administrative Templates** > **Windows Components** > **Store**|

### What you need to know

- The **Turn off the Store application** setting:

  - Doesn't affect Intune's ability to install Microsoft Store apps. In all cases, the new Intune integration with the Microsoft Store is allowed.
  - Doesn't affect the Microsoft Store's ability to automatically update UWP apps. As long as the **Turn off Automatic Download and Install of updates** ([AllowAppStoreAutoUpdate CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#allowappstoreautoupdate)) policy isn't enabled, the Microsoft Store automatically updates UWP apps.
- If you want to allow automatic UWP app updates from the Microsoft Store, including built-in Windows apps, and block users from installing apps from the Microsoft Store or `winget.exe`, then:

  - Set **Turn off Automatic Download and Install of updates** to Disabled or Not configured, **AND**
  - Set **Turn off the Store application** to Enabled or Not configured.

- For Win32 Store apps, if **Turn off Automatic Download and Install of updates** is set, then the Win32 apps with an active Intune assignment are still automatically updated.

> [!TIP]
> Using the **Only display the private store within the Microsoft Store app** policy ([RequirePrivateStoreOnly CSP](/windows/client-management/mdm/policy-csp-ApplicationManagement#requireprivatestoreonly)) is still valid. This policy:
>
> - Blocks end user access to the Microsoft Store.
> - Allows the Windows Package Manager `winget` command line interface (CLI) access to the Microsoft Store.
>
> So, it's not the preferred choice to prevent end user access to the Microsoft Store. Instead, it's recommended to use the **Turn off the Store application** policy.

## Unsupported functionality for Microsoft Store apps

Microsoft Store apps don't support the following features:

- Any app that has an ARM64 installer isn't supported.

## Next step

- [Assign apps to groups](apps-deploy.md)
