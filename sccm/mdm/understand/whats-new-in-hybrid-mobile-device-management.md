---
title: "What's new hybrid MDM  | Microsoft Docs"
description: "Learn about the new mobile device management features available for hybrid deployments with System Center Configuration Manager and Intune."
ms.custom: na
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
caps.latest.revision: 40
author: Mtillmanms.author: mtillmanmanager: angrobe
---
# What's new in hybrid mobile device management with System Center Configuration Manager and Microsoft Intune*Applies to: System Center Configuration Manager (Current Branch)*
This article provides details on the new mobile device management (MDM) features available for hybrid deployments with System Center Configuration Manager and Microsoft Intune.  

##  Compatibility with Configuration Manager versions  

 Each section of this article lists hybrid features under 3 different categories. Use the following guidance to determine compatibility of the features in each category  with different versions of Configuration Manager:  

|Feature categories|
|-|  
|**New in Microsoft Intune** - In general, all the features listed under this category should work with all Configuration Manager releases including System Center 2012 R2 Configuration Manager releases, since these features only require the  Intune service and do not require additional functionality in  Configuration Manager.<br /><br /> **New in Configuration Manager Technical Preview** - All the features listed under this category only work with the specified Technical Preview release. To try out these features, you must install the Technical Preview version specified in the feature description. For more information, see [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md).<br /><br /> **New in Configuration Manager (current branch)** - All the features listed under this category only work with the specified version of Configuration Manager (current branch), such as version 1511 or 1602. If you're using an older version of Configuration Manager for your hybrid deployment, you must upgrade to the Configuration Manager (current branch)  version specified in the feature description. For more information, see [Upgrade to System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md).|  

## New hybrid features in November 2016

### New in Configuration Manager (current branch)

The following features that were previously available in Configuration Manager Technical Preview releases are now available in hybrid deployments with Intune and Configuration Manager (current branch) version 1610.

* [Additional settings and improved experience for Configuration items](/sccm/core/plan-design/changes/whats-new-in-version-1610?branch=sccm-1610-release#new-compliance-settings-for-configuration-items)
* [Additional settings for DEP profiles](#new-in-configuration-manager-technical-preview-1609)
* [Paid apps in Windows Store for Business](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)
* [Native connection types for Windows 10 VPN profiles](#new-in-configuration-manager-technical-preview-1609)
* [Intune compliance charts](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)
* [Request to policy sync from console](/sccm/mdm/deploy-use/sync-intune-device)
* [Windows Defender configuration settings](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client#windows-defender)

The following additional hybrid features are also included in version 1610 of Configuration Manager (current branch):

- **Addtional security support**

  In addition to Full Administrator, the following built-in security roles now have full access to items in the All Corporate-owned Devices node, including Predeclared Devices, iOS Enrollment Profiles, and Windows Enrollment Profiles:

    - Asset Manager
    - Company Resource Access Manager

  Read-only access to these areas of the Configuration Manager console is still granted to the Read-only Analyst role.

- **Auto-trigger VPN access from Windows Information Protection apps**

  You can add a Windows Information Protection primary domain to Windows 10 VPN profiles that causes all associated apps to automatically trigger a VPN connection when they are run on the device. This option is only available when choosing a native connection type.

  - **Conditional access for Windows 10 VPN profiles**

    You can now require Windows 10 devices enrolled in Azure Active Directory to be compliant in order to have VPN access through Windows 10 VPN profiles created in the Configuration Manager console. This is possible through the new **Enable conditional access for this VPN connection** checkbox on the Authentication Method page in the VPN profile wizard and VPN profile properties for Windows 10 VPN profiles. You can also specify a separate certificate for single sign-on authentication if you enable conditional access for the profile.

## New hybrid features in October 2016

### New in Microsoft Intune

The following Intune features introduced in October 2016 work in hybrid deployments.

- **Conditional access for mobile application management**

  You can restrict access to Exchange Online so that access comes only from apps that support Intune mobile application management policies such as Outlook. [This new feature](/intune/deploy-use/allow-policy-managed-apps-access-to-o365) pairs up perfectly with Intune mobile app management (MAM) policies as you can block access to built-in mail clients or other apps that have not been configured with the Intune MAM policies. This ensures your users are accessing your organization’s data with apps that can be protected using Intune MAM. You can get started in Intune mobile app management via the Azure portal. Look for the new Conditional Access section in the “Settings” blade.

-	**Intune App Wrapping Tool for Android**

  You can enable your apps to use Intune mobile application management (MAM) policies by using the Intune App Wrapping Tool.

- **Android Samsung KNOX Standard compatibility with Intune**

  Certain models of the Samsung Galaxy Ace phone cannot be managed by Intune as Samsung KNOX Standard devices. When you enroll these devices with Intune, they will instead be managed as standard Android devices.

  The model numbers affected are:

  - SM-G313HU
  -	SM-G313HY
  -	SM-G313M
  -	SM-G313MY
  -	SM-G313U

  You and your end users need take no further action. For more information, visit the Samsung KNOX website.

### New in Configuration Manager Technical Preview 1610

The following new hybrid features have been introduced in October 2016 for Configuration Manager Technical Preview 1610.

- **Request a policy sync from the admin console**

  You can request a policy sync on an enrolled mobile device from the Configuration Manager console, instead of needing to request the sync in the Company Portal app on the device itself. This is a new action called **Send Sync Request** in the Remote Device Actions menu, which appears in the ribbon when a mobile device is selected in the Devices node.

- **Windows Defender Configuration Settings**

  You can now configure Windows Defender client settings on Intune-enrolled Windows 10 computers using configuration items in the Configuration Manager console. There’s a new setting group called **Windows Defender** in the Configuration Item wizard. Note that this is supported only on Windows 10 Version 1511 and above.


### New in Configuration Manager (current branch)

No new hybrid features have been introduced in August 2016 for Configuration Manager (current branch).

## New hybrid features in September 2016

### New in Microsoft Intune

The following Intune features introduced in September 2016 work in hybrid deployments.

- **Addition of "Notifications" to the Company Portal for Android**

  A new Notifications icon has been added to the Company Portal for Android on the homepage. Tapping this icon accesses the Notifications page, which shows your end users all items that require attention in the Company Portal app, such as device noncompliance, enrollment update, and enrollment activation. The iOS Company Portal app already has this notifications experience. Having the new Notifications page means that user won’t see the Company Access Setup page every time they launch or resume the Company Portal as long as the device is already enrolled. If you create your own end-user guidance, you might want to update your documentation to reflect this change. Find updated screenshots [here](https://aka.ms/androidcpupdate).

- **Changes in support for the iOS Company Portal app**

  All users of the Microsoft Intune Company Portal app for iOS are now required to use its latest version. New users are able to download only the latest version, and current users are required to update to it. The latest version requires iOS 8.0 or later, so devices running older iOS versions cannot use the Company Portal or enroll until they update their device to iOS 8.0 or later, and then update the Company Portal app to the latest version. Enrolled devices running versions below iOS 8.0 will continue to be managed and listed in the Intune Admin Console.

- **Feedback button added to Windows Phone 8.1 Company Portal app**

  The Windows Phone 8.1 Company Portal app enables end users to send feedback about the app by using a new "send feedback" button. To find the button, users tap the “three dots” menu at the bottom right of the Company Portal app screen and then tap **send feedback**. The collected, anonymized feedback will help Microsoft improve the Company Portal app experience for users.

### New in Configuration Manager Technical Preview 1609

The following new hybrid features have been introduced in September 2016 for Configuration Manager Technical Preview 1609.

- **Additional settings and improved experience for Configuration Item settings**

  New settings have been added for Android, iOS, and Windows, and only settings that apply to the platforms you select on the Supported Platforms page are displayed in the wizard. For more information see [New compliance settings for configuration items in TP 1609](/sccm/core/get-started/capabilities-in-technical-preview-1609#new-compliance-settings-for-configuration-items).

- **Additional settings for DEP profiles**

  TouchID, ApplePay, and Zoom have been added as configurable settings in DEP profiles for iOS devices.

- **Paid Apps in Windows Store for Business**

  You can now add both paid and free applications to Windows Store for Business and deploy them to users in your organization. For more information see [Enhancements to Windows Store for Business in TP 1609](/sccm/core/get-started/capabilities-in-technical-preview-1609#enhancements-to-windows-store-for-business-integration-with-configuration-manager).

- **Native connection types for Windows 10 VPN profiles**

  You can now create Windows 10 VPN profiles for MDM with Microsoft Automatic, IKEv2, and PPTP connection types in the Configuration Manager console without using OMA-URI.

- **Intune Compliance Charts**

  You can get a quick view of overall device compliance and top reasons for non-compliance using new charts under the Monitoring workspace. For more information, see [Intune compliance charts in TP 1609](/sccm/core/get-started/capabilities-in-technical-preview-1609#intune-compliance-charts).

### New in Configuration Manager (current branch)

The following new feature introduced in September 2016 is available for hybrid deployments with Microsoft Intune and Configuration Manager version 1606 (current branch).

- **iOS 10 support**

  If you have profiles or configuration items targeted to all iOS platforms, these will also be pushed to iOS 10. We’ve also released an update to Configuration Manager version 1606 that allows you to target profiles and configuration items to individual iOS platforms including iOS 10. You can install the update with the Configuration Manager admin console at **Administration > Overview > Cloud Services > Updates and Servicing**. You can find more information about the update at [http://support.microsoft.com/kb/3192616](http://support.microsoft.com/kb/3192616).

## New hybrid features in August 2016

### New in Microsoft Intune

The following Intune features introduced in August 2016 work in hybrid deployments.

- **Android 7 support in the Company Portal app**

  The Intune Company Portal app for Android provides “day 0” support for the forthcoming Android 7.0 operating system for mobile devices.

- **Google removal of remote passcode reset capability on Android 7.0 devices**

  Google is removing the ability of IT administrators and end users to remotely reset the passcode of Android 7.0 devices. Previously, IT administrators could remotely reset a user’s passcode, and end users could reset their passcodes from the Company Portal website.

- **Allowed and blocked apps policy for Samsung KNOX Standard devices**

  You can now configure a custom policy for Samsung KNOX Standard devices that lets you create one of the following:

  - A list of apps that are blocked from running on the device. Even if installed, an app defined in the blocked list cannot be activated on the device.
  - A list of apps that users of the device are allowed to install from the Google Play store. No other apps can be installed from the store.

  These settings can only be used by devices that run Samsung KNOX Standard. For details, see [Use custom policies to allow and block apps for Samsung KNOX Standard devices](/intune/deploy-use/custom-policy-to-allow-and-block-samsung-knox-apps).

- **Feedback link from the Company Portal to Microsoft**

   The Company Portal website enables end users to tap a new "Feedback" link, at the bottom of the page, to send feedback to Microsoft about their experience with the site. The collected, anonymized feedback will help Microsoft improve the Company Portal website experience for users.

- **Minimum iOS Managed Browser version updated to 8.0**

  The Microsoft Intune Managed Browser app for iOS has been updated to support devices running iOS 8.0 or later. While iOS 7.1 devices can still use the existing Managed Browser app, encourage your users to update to iOS 8.0 or later to access and take full advantage of new Managed Browser features.

### New in Configuration Manager Technical Preview

No new hybrid features have been introduced in August 2016 for Configuration Manager Technical Preview.

### New in Configuration Manager (current branch)

No new hybrid features have been introduced in August 2016 for Configuration Manager (current branch).

## New hybrid features in July 2016

### New in Microsoft Intune

The following Intune features introduced in July 2016 work in hybrid deployments.

- **Xamarin SDK for Intune apps is available**

  The Intune App SDK Xamarin component allows you to enable the Intune mobile app management features in your mobile iOS and Android apps built with Xamarin. You can find the component in the [Xamarin store](https://components.xamarin.com/view/Microsoft.Intune.MAM) or on the [Microsoft Intune Github page](https://github.com/msintuneappsdk).

- **Improved end-user experience when enrolling Windows devices**

  When you are using conditional access, the enrollment steps for Windows 8.1, Windows 10 Desktop, and Windows 10 Mobile have been clarified in the Company Portal website. Users will now see separate **Device enrollment** and **Workplace Join** steps, making it easier for them to see the status of their device and to complete the process if they experience a Workplace Join (WPJ) failure. The separate steps are also expected to simplify the troubleshooting process for IT administrators. Previously, when end users tried to enroll and all enrollment steps succeeded except for WPJ, the enrolled device would not appear on the list of devices for users to identify, causing confusion for users.

 - **Full wipe now available for Windows 10 devices**

    Windows 10 PCs and laptops enrolled as mobile devices can be wiped to reset the device to its factory settings. For more information, see [How to protect your devices with remote wipe](/sccm/mdm/deploy-use/wipe-lock-reset).

- **Changes to Device Enrollment Managers accounts in the iOS Company Portal app**

  To improve performance and scale, Intune no longer displays all Device Enrollment Managers (DEM) devices in the My Devices pane of the iOS Company Portal app. Only the local device running the app is displayed, and only if it is enrolled via the Company Portal app.

  The DEM user may perform actions on the local device, but remote management of other enrolled devices can only be performed from the Intune admin console. Additionally, Intune is deprecating use of DEM accounts with either the Apple Device Enrollment Program or the Apple Configurator tool. Both these enrollment methods already support user-less enrollment for shared iOS devices.

  Only use DEM accounts when user-less enrollment for shared devices is unavailable. For more information, see [Enroll corporate-owned devices with the Device Enrollment Manager in Microsoft Intune](../deploy-use/enroll-devices-with-device-enrollment-manager.md).

- **Changes to the Android Company Portal app**

  If Android end users see an error message that says their device is missing a required certificate, they can tap a "How to resolve this" button to get steps for installing the missing certificate. If users complete the steps, but see an additional "missing certificate" error message, they are asked to contact their IT administrator and provide this link, which contains steps that IT administrators can use to fix the certificate issue.

- **Restrict side-loaded app installations to enrolled Android devices**

  Android devices can no longer install applications through the Company Portal website unless the devices have been enrolled in Intune by using the Intune Company Portal app for Android.


### New in Configuration Manager Technical Preview

No new hybrid features have been introduced in July 2016 for Configuration Manager Technical Preview.

### New in Configuration Manager (current branch)

The following features that were previously available in Configuration Manager Technical Preview releases are now available in hybrid deployments with Intune and Configuration Manager (current branch) version 1606.

* Find, manage, and distribute Windows Store for Business apps for Windows 10 devices from the Configuration Manager console ([1604](whats-new-hybrid-archive.md#new-in-1604-technical-preview))
* 	SmartLock setting for Android devices ([1604](whats-new-hybrid-archive.md#new-in-1604-technical-preview))
*	App-triggered VPN for Windows 10 devices ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*	New experience for remote device actions ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*	Windows Store for Business apps ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*	General improvements for volume-purchased apps ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*	Windows Information Protection (WIP) ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*	Pre-declare corporate-owned devices with IMEI or iOS serial number ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*	Automatically categorize devices into collections ([1606](whats-new-hybrid-archive.md#new-in-1606-technical-preview))

For information on the new functionality, see the documentation for the specified Technical Preview release.

## Notices

- **October 25, 2016: Windows Phone 8 Company Portal upload deprecated**

  The ability to upload a signed Company Portal app has been removed from the Configuration Manager console, as Intune support is being deprecated for Windows 8, Windows Phone 8, and Windows RT, and support for the Windows Phone 8 Company Portal is ending in November.  Windows 8, Windows Phone 8, and Windows RT devices that are already enrolled will continue to be supported, but enrolling additional devices with these platforms will not be supported.


### See Also

- [Past hybrid MDM features](whats-new-hybrid-archive.md)
- [What's new for MDM in System Center 2012 Configuration Manager](https://technet.microsoft.com/library/mt445560.aspx)
