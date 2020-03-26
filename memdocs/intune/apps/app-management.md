---
# required metadata

title: What is app management in Microsoft Intune?
titleSuffix:
description: Learn about client app management capabilities by platform for Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/17/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology:
ms.assetid: 1975a2dc-3a14-4cb9-9afb-e2ba01a1c51b

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# What is Microsoft Intune app management?


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

As an IT admin, you can use Microsoft Intune to manage the client apps that your company's workforce uses. This functionality is in addition to managing devices and protecting data. One of an admin's priorities is to ensure that end users have access to the apps they need to do their work. This goal can be a challenge because:
- There are a wide range of device platforms and app types.
- You might need to manage apps on both company devices and users' personal devices.
- You must ensure that your network and your data remain secure.

Additionally, you might want to assign and manage apps on devices that are not enrolled with Intune.

## Mobile Application Management (MAM) basics

[Intune mobile application management](app-lifecycle.md) refers to the suite of Intune management features that lets you publish, push, configure, secure, monitor, and update mobile apps for your users.

MAM allows you to manage and protects your organization's data within an application. With **MAM without enrollment** (MAM-WE), a work or school-related app that contains sensitive data can be managed on almost any [device](app-management.md#app-management-capabilities-by-platform), including personal devices in **bring-your-own-device** (BYOD) scenarios. Many productivity apps, such as the Microsoft Office apps, can be managed by Intune MAM. See the official list of [Microsoft Intune protected apps](apps-supported-intune-apps.md) available for public use.

Intune MAM supports two configurations:
- **Intune MDM + MAM**: IT administrators can only manage apps using MAM and app protection policies on devices that are enrolled with Intune mobile device management (MDM). To manage apps using MDM + MAM, customers should use the Intune console in the Azure portal at https://portal.azure.com.
- **MAM without device enrollment**: MAM without device enrollment, or MAM-WE, allows IT administrators to manage apps using MAM and app protection policies on devices not enrolled with Intune MDM. This means apps can be managed by Intune on devices enrolled with third-party EMM providers. To manage apps using MAM-WE, customers should use the Intune console in the Azure portal at https://portal.azure.com. Also, apps can be managed by Intune on devices enrolled with third-party Enterprise Mobility Management (EMM) providers or not enrolled with an MDM at all. For more information about BYOD and Microsoft's EMS, see [Technology decisions for enabling BYOD with Microsoft Enterprise Mobility + Security (EMS)](../fundamentals/byod-technology-decisions.md).

## App management capabilities by platform

Intune offers a range of capabilities to help you get the apps you need on the devices you want to run them on. The following table provides a summary of app management capabilities.

|  | Android/Android Enterprise | iOS/iPadOS | macOS | Windows 10 | Windows Phone 8.1 |
|-------------------------------------------------------------------------------------|---------|-----|-------|------------|-------------------|
| Add and assign   apps to devices and users | Yes | Yes | Yes | Yes | Yes |
| Assign apps to   devices not enrolled with Intune | Yes | Yes | No | No | No |
| Use app   configuration policies to control the startup behavior of apps | Yes | Yes | No | No | No |
| Use mobile app   provisioning policies to renew expired apps | No | Yes | No | No | No |
| Protect company   data in apps with app protection policies | Yes | Yes | No | No <sup>1</sup> | No |
| Remove only   corporate data from an installed app (app selective wipe) | Yes | Yes | No | Yes | Yes |
| Monitor app   assignments | Yes | Yes | Yes | Yes | Yes |
| Assign and   track volume-purchased apps from an app store | No | No | No | Yes | No |
| Mandatory   install of apps on devices (required) <sup>2</sup> | Yes | Yes | Yes | Yes | Yes |
| Optional   installation on devices from the Company Portal (available installation) | Yes <sup>3</sup> | Yes | Yes | Yes | Yes |
| Install   shortcut to an app on the web (web link) | Yes <sup>4</sup> | Yes | Yes | Yes | Yes |
| In-house   (line-of-business) apps | Yes | Yes | Yes | Yes | No |
| Apps from a   store | Yes | Yes | No | Yes | Yes |
| Update apps | Yes | Yes | No | Yes | Yes |

<sup>1</sup> Consider using [Windows Information Protection](../protect/windows-information-protection-configure.md) to protect apps on devices that run Windows 10.<br>
<sup>2</sup> Applies to devices managed by Intune only.<br>
<sup>3</sup> Intune supports available apps from Managed Google Play store on Android Enterprise devices.<br>
<sup>4</sup> Intune does not provide installing a shortcut to an app as a web link on standard Android Enterprise devices. However, Web link support is provided for [multi-app dedicated Android Enterprise devices](../configuration/device-restrictions-android-for-work.md#dedicated-device-settings). 


## Get started

You can find most app-related information in the **Apps** workload, which you can access by doing the following:

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Select **Apps**.

    ![The Apps workload pane](./media/app-management/apps-workload.png)

The apps workload provides links to access common app information and functionality. 

The top of the App workload navigation menu provide commonly used app details:
- **Overview**: Select this option to view the tenant name, the MDM authority, the tenant location, the account status, app installation status, and app protection policy status.
- **All apps**: Select this option to display a list of all available apps. You can add additional apps from this page. Additionally, you can see the status of each app, as well as whether each app is assigned. For more information, see [Add apps](apps-add.md) and [Assign apps](apps-deploy.md).
- **Monitor apps**
    - **App licenses**: View, assign, and monitor volume-purchased apps from the app stores. For more information, see [iOS volume-purchased program (VPP) apps](vpp-apps-ios.md) and [Microsoft Store for Business volume-purchased apps](windows-store-for-business.md).
    - **Discovered apps**: View apps that were assigned by Intune or installed on a device. For more information, see [Intune discovered apps](app-discovered-apps.md).
    - **App install status**: View the status of an app assignment that you created. For more information, see [Monitor app information and assignments with Microsoft Intune](apps-monitor.md#device-and-user-status-graphs).
    - **App protection status**: View the status of an app protection policy for a user that you select.
- **By Platform**: Select these platforms to view the available apps by platform.
    - Windows
    - iOS
    - macOS
    - Android
- **Policy**:
    - **App protection policies**: Select this option to associate settings with an app and help protect the company data it uses. For example, you might restrict the capabilities of an app to communicate with other apps, or you might require the user to enter a PIN to access a company app. For more information, see [App protection policies](app-protection-policies.md).
    - **App configuration policies**: Select this option to supply settings that might be required when a user runs an app. For more information, see [App configuration policies](app-configuration-policies-use-ios.md), [iOS app configuration policies](app-configuration-policies-use-ios.md), and [Android app configuration policies](app-configuration-policies-overview.md).
    - **iOS app provisioning profiles**: iOS apps include a provisioning profile and code that is signed by a certificate. When the certificate expires, the app can no longer be run. Intune gives you the tools to proactively assign a new provisioning profile policy to devices that have apps that are nearing expiration. For more information, see [iOS app provisioning profiles](app-provisioning-profile-ios.md).
    - **S mode supplemental policies**: Select this option to authorize additional applications to run on your managed S mode devices. For more information, see [S mode supplemental policies](apps-win32-s-mode.md).
    - **Policy sets**: Select this option to create an assignable collection of apps, policies, and other management objects you've created. For more information, see [Policy sets](../fundamentals/policy-sets.md).
- **Other**:   
    - **App selective wipe**: Select this option to remove only corporate data from a selected user's device. For more information, see [App selective wipe](apps-selective-wipe.md).
    - **App categories**: Add, pin, and delete app category names.
    - **E-books**: Some app stores give you the ability to purchase multiple licenses for an app or books that you want to use in your company. For more information, see [Manage volume-purchased apps and books with Microsoft Intune](vpp-apps.md).
- **Help and support**: Troubleshoot, request support, or view Intune status. For more information, see [Troubleshoot problems](../fundamentals/help-desk-operators.md).

## Additional information
The following items within the console provide app related functionality:
- **Microsoft Store for Business**: Set up integration to the Microsoft Store for Business. Afterward, you can synchronize purchased applications to Intune, assign them, and track your license usage. For more information, see [Microsoft Store for Business volume-purchased apps](windows-store-for-business.md).
- **Windows enterprise certificate**: Apply or view the status of a code-signing certificate that's used to distribute line-of-business apps to your managed Windows devices.
- **Windows Symantec certificate**: Apply or view the status of a Symantec code-signing certificate, which is needed to distribute XAP and WP8.x appx files to Windows 10 Mobile devices.
- **Windows side loading keys**: Add a Windows side-loading key that can be used to install an app directly to devices rather than publishing and downloading the app from the Windows store. For more information, see [Side-load a Windows app](app-sideload-windows.md).
- **Apple VPP tokens**: Apply and view your iOS/iPadOS Volume Purchase Program (VPP) licenses. For more information, see [iOS/iPadOS volume-purchased apps](vpp-apps-ios.md).
- **Managed Google Play**: Managed Google Play is Google's enterprise app store and sole source of applications for Android Enterprise. For more information, see [Add Managed Google Play apps to Android Enterprise devices with Intune](apps-add-android-for-work.md).
- **Customization**: Customize the Company Portal to give it your company branding. For more information, see [Company Portal configuration](company-portal-app.md).

## Next steps

- [Add an app to Microsoft Intune](apps-add.md)
