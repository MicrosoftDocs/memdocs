---
title: Add apps to Microsoft Intune
titleSuffix:
description: Learn how to add apps to Microsoft Intune so you can assign apps to users and devices. Intune supports a wide range of app types.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/18/2022
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology:
ms.assetid: a1ded457-0ecf-4f9c-a2d2-857d57f8d30a

ms.reviewer: manchen
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection:
  - M365-identity-device-management
  - highpri
---

# Add apps to Microsoft Intune 

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Before you can configure, assign, protect, or monitor apps, you must add them to Microsoft Intune.

The users of apps and devices at your company (your company's workforce) might have several app requirements. Before adding apps to Intune and making them available to your workforce, you may find it helpful to assess and understand a few app fundamentals. There are various types of apps that are available for Intune. You must determine app requirements that are needed by the users at your company, such as the platforms and capabilities that your workforce needs. You must determine whether to use Intune to manage the devices (including apps) or have Intune manage the apps without managing the devices. Also, you must determine the apps and capabilities that your workforce needs, and who needs them. The information in this article helps you get started.

## App types in Microsoft Intune

Intune supports a wide range of app types. The available options differ for each app type. Intune lets you add and assign the following app types:

| App types | Installation | Updates |
|---|---|---|
| Apps from the store (store apps) | Intune installs the app on the device.  | App updates are automatic. |
| Apps written in-house or as a custom app (line-of-business) | Intune installs the app on the device (you supply the installation file). | You must update the app. |
| Apps that are built-in (built-in apps) | Intune installs the app on the device.  | App updates are automatic. |
| Apps on the web (web link) | Intune creates a shortcut to the web app on the device home screen. | App updates are automatic. |
| Apps from other Microsoft services  | Intune creates a shortcut to the app in the Company Portal. For more information, see [App source setting options](../apps/company-portal-app.md#app-source-setting-options). | App updates are automatic. |

### Specific app type details
 
The following table lists the specific app types and how you can add them in the Intune **Add app** pane:

| **App-specific type** | **General type** | **App-specific procedures** |
| --- | --- | --- |
| Android store apps  | Store app  | Select **Android** as the **app type**, and enter the Google Play store URL for the app. |
| Android Enterprise apps  | Store app  | Select **Android** as the **app type**, and enter the Managed Google Play store URL for the app. <sup>1</sup> |
| iOS/iPadOS store apps  | Store app  | Select **iOS** as the **app type**, search for the app, and select the app in Intune. |
| Microsoft store apps  | Store app  | Select **Windows** as the **app type**, and enter the Microsoft store URL for the app. |
| Managed Google Play apps | Store app  | Select **Managed Google Play** as the **app type**, search for the app, and select the app in Intune. |
| Microsoft 365 apps for Windows 10  | Store app (Microsoft 365) | Select **Windows 10** under **Microsoft 365 Apps** as the **app type**, and then select the Microsoft 365 app that you want to install.  |
| Microsoft 365 apps for macOS | Store app (Microsoft 365) | Select **macOS** under **Microsoft 365 Apps** as the **app type**, and then select the Microsoft 365 app suite. |
| Microsoft Edge, version 77 and later for Windows 10 | Store app | Select **Windows 10** under **Microsoft Edge, version 77 and later** as the **app type**. |
| Microsoft Edge, version 77 and later for macOS | Store app | Select **macOS** under **Microsoft Edge, version 77 and later** as the **app type**. |
| Android line-of-business (LOB) apps | LOB app | Select **Line-of-business** app as the **app type**, select the **App package file**, and then enter an Android installation file with the extension **.apk**.  |
| iOS/iPadOS LOB apps | LOB app | Select **Line-of-business** app as the **app type**, select the **App package file**, and then enter an iOS/iPadOS installation file with the extension **.ipa**.  |
| Windows LOB apps | LOB app | Select **Line-of-business** app as the app type, select the **App package file**, and then enter a Windows installation file with the extension **.msi**, **.appx**, **.appxbundle**, **.msix**, and **.msixbundle**. |
| Built-in iOS/iPadOS app  | Built-in app | Select **Built-In app** as the **app type**, and then select the built-in app in the list of provided apps.  |
| Built-in Android app  | Built-in app | Select **Built-In app** as the **app type**, and then select the built-in app in the list of provided apps.  |
| Cross platform web apps  | Web app  | Select **Web link** as the **app type**, and then enter a valid URL pointing to the web app.  |
| Android Enterprise system apps  | Store app  | Select **Android Enterprise system app** as the **app type**, and then enter the app name, publisher, and package file.  |
| Windows app (Win32)  | LOB app  | Select **Windows app (Win32)** as the **app type**, select the **App package file**, and then select an installation file with the extension **.intunewin**.  |
| macOS LOB apps | LOB app  | Select **Line-of-business** as the **app type**, select the **App package file**, and then select an installation file with the extension **.intunemac**.  |
| macOS apps (DMG) | LOB app (non-store app)  | Select **macOS app (DMG)** as the app type, select the **App package** file, and then select an installation file with the extension *.dmg*.  |

<sup>1</sup> For more information about Android Enterprise and Android work profiles, see [Understanding licensed apps](apps-add.md#understanding-licensed-apps) below.

You can add an app in Microsoft Intune by selecting **Apps** > **All apps** > **Add**. The **Select app type** pane is displayed and allows you to select the **App type**. 

>[!TIP]
> An LOB app is one that you add from an app installation file. For example, to install an iOS/iPadOS LOB app, you add the application by selecting **Line-of-business app** as the **App type** in the **Select app type** pane. You then select the app package file (extension .ipa). These types of apps are typically written in-house or as a custom app.

## Assess app requirements
As an IT Admin, you determine not only which apps your group must use, but you also determine the capabilities needed for each group and subgroup. For each app, you determine the platforms needed, the groups of users that need the app, the configuration policies to apply for those groups, and the protection policies to apply. For example, for enrollment types including Android personally-owned work profile, you may want to deploy a web browsing app to make sure users will have a way to open links. 

Additionally, you must determine whether to focus on Mobile Device Management (MDM) or only on Mobile Application Management (MAM). 

Using Intune to manage the device with MDM is useful when:
- Users need a Wi-Fi or a VPN corporate connectivity profile to be productive.
- Users need a set of apps to be pushed to their device.
- Your organization needs to comply with regulatory or other policies that call out specific MDM controls, such as security or encryption.

Using Intune to manage apps with MAM without managing the device is useful when:
- You want to allow users to use their own device (BYOD).
- You want to provide a one-time pop-up message to let users know that MAM protections are in place, rather than continual device-level notification.
- You want to comply with policies that require less management capability on personal devices. For instance, you want to manage the corporate data for the apps, rather than manage the corporate data for the entire device.

For more information, [Compare MDM and MAM](../fundamentals/byod-technology-decisions.md).

### Determine who will use the app

As you're determining which apps your workforce needs, consider the various groups of users and the various apps they use. Knowing these groups is also helpful after you've added an app. After you add an app, you assign a group of users that can use the app. 

First, you must determine which group should have access to the app, based on the sensitivity of the data the app contains. You might need to include or exclude certain types of roles within your organization. For example, only certain LOB apps might be required for your sales group, whereas people focused on engineering, finance, HR, or legal might not need to use the LOB apps. In addition, your sales group might need additional data protection and access to internal corporate services on their mobile devices. You must determine how this group will connect to resources using the app. Will the data that the app accesses live in the cloud or on-premises? Also, how will the users connect to resources by using the app? 

Intune also supports enabling access to client apps that require secure access to on-premises data, such as line-of-business app servers. You ordinarily provide this type of access by using [Intune-managed certificates](../protect/certificates-configure.md) for access control, combined with a standard VPN gateway or proxy in the perimeter, such as Azure Active Directory Application Proxy. The Intune [App Wrapping Tool and App SDK](../developer/apps-prepare-mobile-application-management.md) can help contain the accessed data within your line-of-business app, so that it can't pass corporate data to consumer apps or services.

Use the [Intune deployment planning, design and implementation guide](../fundamentals/intune-planning-guide.md) to help determine how you identify the organizational groups. For information about assigning apps to groups, see [Assign apps to groups with Microsoft Intune](apps-deploy.md).

### Determine the type of app for your solution

You can choose from the following app types:
- **Apps from the store**: Apps that have been uploaded to either the Microsoft store, the iOS/iPadOS store, or the Android store are store apps. The provider of a store app maintains and provides updates to the app. You select the app in the store list and add it by using Intune as an available app for your users.
- **Apps written in-house or as a custom app (line-of-business)**: Apps that are created in-house or as a custom app are line-of-business (LOB) apps. The functionality of this type of app has been created for one of the Intune supported platforms, such as Windows, iOS/iPadOS, macOS, or Android. Your organization creates and provides you with updates as a separate file. You provide updates of the app to users by adding and deploying the updates using Intune.
- **Apps on the web**: Web apps are client-server applications. The server provides the web app, which includes the UI, content, and functionality. Additionally, modern web hosting platforms commonly offer security, load balancing, and other benefits. This type of app is separately maintained on the web. You use Intune to point to this app type. You also assign which groups of users can access the app.
- **Apps from other Microsoft services**: Apps that have been sourced from either Azure AD or Office Online. **Azure AD Enterprise applications** are registered and assigned via the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431). **Office Online applications** are assigned using the licensing controls available in the [M365 Admin Center](https://admin.microsoft.com). You can hide or show Azure AD Enterprise and Office Online applications to end-users in the Company Portal. From the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Tenant administration** > **Customization** to find this configuration setting. Select to **Hide** or **Show** either **Azure AD Enterprise applications** or **Office Online applications** in the Company Portal for each end-user. Each end-user will see their entire application catalog from the chosen Microsoft service. By default, each additional app source will be set to **Hide**. For more information, see [App source setting options](../apps/company-portal-app.md#app-source-setting-options). 

As you're determining which apps your organization needs, consider how the apps integrate with cloud services, what data the apps access, whether the apps are available to BYOD users, and whether the apps require internet access.

For more information about the types of apps that your organization needs, [Create a design](../fundamentals/intune-planning-guide.md).

### Understanding app management and protection policies
Intune lets you modify the functionality of apps that you deploy to help align them with your company's compliance and security policies. This control allows you to determine how your company data is protected. Intune-managed apps are enabled with a rich set of mobile application protection policies, such as:

- Restricting copy-and-paste and save-as functions.
- Configuring web links to open inside the Microsoft Edge app.
- Enabling multi-identity use and app-level Conditional Access.

Intune-managed apps can also enable app protection without requiring enrollment, which gives you the choice of applying data loss-prevention policies without managing the user's device. Additionally, you can incorporate mobile-app management in your mobile and line-of-business apps by using the Intune App SDK and App Wrapping Tool. For more information about these tools, see [Intune App SDK overview](../developer/app-sdk.md).

### Understanding licensed apps
In addition to understanding web apps, store apps, and LOB apps, you should also be aware of the destination of volume-purchase-program apps and licensed apps, such as: 
- **Apple Volume Purchasing Program for Business (iOS)**: The iOS/iPadOS App Store lets you purchase multiple licenses for an app that you want to run in your company. Purchasing multiple copies helps you to efficiently manage apps in your company. For more information, see [Manage iOS/iPadOS volume-purchased apps](vpp-apps-ios.md).
- **Android Enterprise fully managed work profile**: How you assign apps to Android Enterprise fully managed work profile devices differs from how you assign them to standard Android devices. All apps you install for Android Enterprise fully managed work profiles come from the Managed Google Play store. You use Intune to browse for the apps you want and approve them. The app then appears in the **Licensed apps** node of the portal, and you can manage assignment of the app as you would any other app.
- **Microsoft Store for Business (Windows 10)**: Microsoft Store for Business gives you a place to find and purchase apps for your organization, individually or in volume. By connecting the store to Microsoft Intune, you can manage volume-purchased apps in the portal. For more information, see [Manage apps from Microsoft Store for Business](windows-store-for-business.md).

    > [!NOTE]
    > The file extensions for Windows apps include **.msi**, **.appx**, **.appxbundle**, **.msix** and **.msixbundle**.  

## Before you add apps
Before you begin to add and assign apps, consider the following points:

- When you add and assign an app from a store, your users must have an account with that store to be able to install the app.
- Some apps or items that you assign might depend on built-in iOS/iPadOS apps. For example, if you assign a book in the iOS/iPadOS store, the iBooks app must be present on the device. If you have removed the iBooks built-in app, you cannot use Intune to reinstate it.

> [!IMPORTANT]
> If you change the name of the app through Intune after you have deployed and installed the app, the app will no longer be able to be targeted using commands.

## Cloud storage space
All apps that you create by using the software installer installation type (for example, a line-of-business app) are packaged and uploaded to Intune cloud storage. A trial subscription of Intune includes 2 gigabytes (GB) of cloud-based storage that is used to store managed apps and updates. A full subscription does not limit the total amount of storage space.

Requirements for cloud storage space are as follows:

- All app installation files must be in the same folder.
- The maximum file size for any file that you upload is 8 GB.

  > [!NOTE]
  > Windows Line-of-business (LOB) apps, including Win32, Windows Universal AppX, Windows Universal AppX bundle, Windows Universal MSI X, and Windows Universal MSI X bundle, have a maximum size limit of 8 GB per app. All other LOB apps, including iOS/iPadOS LOB apps, have a maximum size limit of 2 GB per app.

## Create and edit categories for apps

App categories can be used to help you sort apps to make them easier for users to find in the company portal. You can assign one or more categories to an app, for example, *Developer apps* or *Communication apps*.

When you add an app to Intune, you are given the option to select the category you want. Use the platform-specific topics to add an app and assign categories. To create and edit your own categories, use the following procedure:

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Select **Apps** > **App categories**.  
    The **App categories** pane displays a list of current categories. 
5. Do either of the following:
    - To add a category, in the **Create category** pane, select **Add**, and then enter a name for the category.  
    Names can be entered in one language only, and they are not translated by Intune.
    - To edit a category, select the ellipsis (**...**) next to the category, and then select **Pin to dashboard** or **Delete**.
6. Select **Create**.

## Apps that are added automatically by Intune

Previously, Intune contained a number of built-in apps that you could quickly assign. Based on Intune customer feedback, we removed this list, and the built-in apps are no longer displayed. However, if you have already assigned any built-in apps, the apps remain visible in the list of apps. You can continue to assign the apps as required.

> [!NOTE]
> For the installation of a required non-Line-of-Business app, Intune will attempt to install the app by sending an install command whenever the device checks-in, given that the app is not detected and the app's install state is not *Install Pending*.

## Installing, updating, or removing required apps

Intune will automatically reinstall, update, or remove a required app within 24 hours, rather than waiting for the 7 day re-evaluation cycle.

Intune will automatically reinstall, update, or remove a required app based on the following conditions:
- If an end user uninstalls an app that you have required to be installed on the end user's device, Intune will automatically reinstall the app when this schedule elapses.
- If a required app install fails or somehow the app is not present on the device, Intune evaluates compliance and reinstalls the app when this schedule elapses.  
- An admin targets an app as available to a user group and an end user installs the app from the company portal on the device. Later, the admin updates the app from v1 to v2. Intune will update the app when this schedule elapses, provided that any previous version of the app is still present on the device.
- If the admin deploys uninstall intent and the app is present on the device and failed to uninstall, Intune evaluates compliance and uninstalls the app when this schedule elapses.   

> [!NOTE]
> Using the Windows Company Portal, end users can restart an app installation if the progress seems to have stalled or is frozen. This functionality is allowed if the app installation progress has not changed in two hours.
> 
> From the **Installed apps** page of the Windows Company Portal or the Company Portal website, end users can view the installation status and details for device-assigned required apps. This functionality is provided in addition to the installation status and details of user-assigned required apps.

## Uninstall an app

When you need to uninstall an app from user's devices, use the following steps.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All apps** > *the app* > **Assignments** > **Add group**.
3. In the **Add group** pane, select **Uninstall**.
4. Select **Included Groups** to select the groups of users that are affected by this app assignment.
5. Select the groups that you want to apply the uninstall assignment.
6. Click **Select** on the **Select groups** pane.
7. Click **OK** on the **Assign** pane to set the assignment.
8. If you want to exclude any groups of users from being affected by this app assignment, select **Exclude Groups**.
9. If you have chosen to exclude any groups, in **Select groups**, select **Select**.
10. Select **OK** in the **Add group** pane.
11. Select **Save** in the app **Assignments** pane.

> [!IMPORTANT]
> To uninstall the app successfully, make sure to remove the members or group assignment for install before assigning them to be uninstalled. If a group is assigned to both install an app and uninstall an app, the app will remain and not be removed.

## App installation errors

For details about Intune app installation errors, see [App installation errors](/troubleshoot/mem/intune/troubleshoot-app-install).

## Next steps

To learn how to add apps for each platform to Intune, see:

- [Android store apps](store-apps-android.md)
- [Android LOB apps](lob-apps-android.md)
- [iOS store apps](store-apps-ios.md)
- [iOS LOB apps](lob-apps-ios.md)
- [macOS LOB apps](lob-apps-macos.md)
- [Web apps (for all platforms)](web-app.md)
- [Microsoft store apps](store-apps-windows.md)
- [Windows LOB app](lob-apps-windows.md)
- [Microsoft 365 apps for Windows 10](apps-add-office365.md)
- [Microsoft 365 apps for macOS](apps-add-office365-macos.md)
- [Managed Google Play apps](apps-add-android-for-work.md)
- [Microsoft Edge for Windows 10](apps-windows-edge.md)
- [Microsoft Edge for macOS](apps-edge-macos.md)
- [Built-in apps](apps-add-built-in.md)
- [Android Enterprise system app](apps-ae-system.md)
- [Win32 apps](apps-win32-app-management.md)
