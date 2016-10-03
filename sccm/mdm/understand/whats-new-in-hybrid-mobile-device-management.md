---
title: "What&#39;s new hybrid MDM | Microsoft Intune | System Center Configuration Manager"
ms.custom: na
ms.date: 08/10/2016
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
# What&#39;s new in hybrid mobile device management with System Center Configuration Manager and Microsoft Intune
This article provides details on the new mobile device management (MDM) features available for hybrid deployments with System Center Configuration Manager and Microsoft Intune.  

 In this article:

*    [Compatibility with Configuration Manager versions](#compat)
*    [New hybrid features in July 2016](#New-hybrid-features-in-July-2016)
*    [New hybrid features in June 2016](#June)  
*    [New hybrid features in May 2016](#May)   
*    [New hybrid features in April 2016](#april)   
*    [New hybrid features in March 2016](#march)  

##  <a name="compat"></a> Compatibility with Configuration Manager versions  
 Each section of this article lists hybrid features under 3 different categories. Use the following guidance to determine compatibility of the features in each category  with different versions of Configuration Manager:  

|Feature categories|
|-|  
|**New in Microsoft Intune** - In general, all the features listed under this category should work with all Configuration Manager releases including System Center 2012 R2 Configuration Manager releases, since these features only require the  Intune service and do not require additional functionality in  Configuration Manager.<br /><br /> **New in Configuration Manager Technical Preview** - All the features listed under this category only work with the specified Technical Preview release. To try out these features, you must install the Technical Preview version specified in the feature description. For more information, see [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md).<br /><br /> **New in Configuration Manager (current branch)** - All the features listed under this category only work with the specified version of Configuration Manager (current branch), such as version 1511 or 1602. If you're using an older version of Configuration Manager for your hybrid deployment, you must upgrade to the Configuration Manager (current branch)  version specified in the feature description. For more information, see [Upgrade to System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md).|  

## New hybrid features in July 2016

### New in Microsoft Intune

The following features introduced in July 2016 work in hybrid deployments exactly as they do in the standalone Intune service. No changes or administration in Configuration Manager are required to use these features.

- **Xamarin SDK for Intune apps is available**

  The Intune App SDK Xamarin component allows you to enable the Intune mobile app management features in your mobile iOS and Android apps built with Xamarin. You can find the component in the [Xamarin store](https://components.xamarin.com/view/Microsoft.Intune.MAM) or on the [Microsoft Intune Github page](https://github.com/msintuneappsdk).

- **Improved end-user experience when enrolling Windows devices**

  When you are using conditional access, the enrollment steps for Windows 8.1, Windows 10 Desktop, and Windows 10 Mobile have been clarified in the Company Portal website. Users will now see separate **Device enrollment** and **Workplace Join** steps, making it easier for them to see the status of their device and to complete the process if they experience a Workplace Join (WPJ) failure. The separate steps are also expected to simplify the troubleshooting process for IT administrators. Previously, when end users tried to enroll and all enrollment steps succeeded except for WPJ, the enrolled device would not appear on the list of devices for users to identify, causing confusion for users.

 - **Full wipe now available for Windows 10 devices**

    Windows 10 PCs and laptops enrolled as mobile devices can be wiped to reset the device to its factory settings. For more information, see [How to protect your devices with remote wipe](/sccm/mdm/deploy-use/wipe-lock-reset-devices).

- **Changes to Device Enrollment Managers accounts in the iOS Company Portal app**

  To improve performance and scale, Intune no longer displays all Device Enrollment Managers (DEM) devices in the My Devices pane of the iOS Company Portal app. Only the local device running the app is displayed, and only if it is enrolled via the Company Portal app.

  The DEM user may perform actions on the local device, but remote management of other enrolled devices can only be performed from the Intune admin console. Additionally, Intune is deprecating use of DEM accounts with either the Apple Device Enrollment Program or the Apple Configurator tool. Both these enrollment methods already support user-less enrollment for shared iOS devices.

  Only use DEM accounts when user-less enrollment for shared devices is unavailable. For more information, see [Enroll corporate-owned devices with the Device Enrollment Manager in Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/enroll-corporate-owned-devices-with-the-device-enrollment-manager-in-microsoft-intune).

- **Changes to the Android Company Portal app**

  If Android end users see an error message that says their device is missing a required certificate, they can tap a "How to resolve this" button to get steps for installing the missing certificate. If users complete the steps, but see an additional "missing certificate" error message, they are asked to contact their IT administrator and provide this link, which contains steps that IT administrators can use to fix the certificate issue.

- **Restrict side-loaded app installations to enrolled Android devices**

  Android devices can no longer install applications through the Company Portal website unless the devices have been enrolled in Intune by using the Intune Company Portal app for Android.


### New in Configuration Manager Technical Preview

No new hybrid features have been introduced in July 2016 for Configuration Manager Technical Preview.

### New in Configuration Manager (current branch)

The following features that were previously available in Configuration Manager Technical Preview releases are now available in hybrid deployments with Intune and Configuration Manager (current branch) version 1606. These features require you to use the Configuration Manager console to configure and manage them.

* Find, manage, and distribute Windows Store for Business apps for Windows 10 devices from the Configuration Manager console ([1604](#TP1604))
* 	SmartLock setting for Android devices ([1604](#TP1604))
*	App-triggered VPN for Windows 10 devices ([1605](#TP1605))
*	New experience for remote device actions ([1605](#TP1605))
*	Windows Store for Business apps ([1605](#TP1605))
*	General improvements for volume-purchased apps ([1605](#TP1605))
*	Windows Information Protection (WIP) ([1605](#TP1605))
*	Pre-declare corporate-owned devices with IMEI or iOS serial number ([1605](#TP1605))
*	Automatically categorize devices into collections ([1606](#TP1606))

For information on the new functionality, see the documentation for the specified Technical Preview release.

## <a name="June"></a> New hybrid features in June 2016

### New in Microsoft Intune
The following features introduced in June 2016 work in hybrid deployments exactly as they do in the standalone Intune service. No changes or administration in Configuration Manager are required to use these features.

- **Intune service health**
  Service health information for Intune has been moved to a central location with other Microsoft services. You'll now find this information in the Office 365 management portal under Service Health. For more information, see this [blog post](https://blogs.technet.microsoft.com/enterprisemobility/2016/04/28/intune-service-health-is-now-available-in-the-office-365-portal/).

- **Enhanced Windows 10 enterprise data policy configuration experience**

  Intune now has an improved experience for configuring Windows 10 information protection policy. Improvements include better ways to create app rules, specify network boundary definition, and other Windows Information Protection settings. To learn more, see [Create a Windows Information Protection (WIP) policy using Microsoft Intune](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-intune).

- **Cisco ISE network access control policy for Intune**

  Customers who use the Cisco Identity Service Engine (ISE) 2.1 and also use Microsoft Intune can set a network access control policy in ISE.Using this policy, devices that need to connect to the network using WiFi or VPN must meet the following conditions before they are allowed access:

  - Must be managed by Intune
  - Must be compliant with any deployed Intune compliance policies

  End users of noncompliant devices will be prompted to enroll, and remediate any compliance issues to gain access.

- **Conditional access for browser**

  You can set a conditional access policy for Exchange Online and SharePoint Online so that they can only be accessed from supported web browsers on managed and compliant iOS and Android devices. End users who try to sign in to Outlook Web Access (OWA) and SharePoint sites with iOS and Android devices will be prompted to enroll their device with Intune as well as to fix any non-compliance issues before they can complete sign-in. For more information, see

  * [Restrict email access to Exchange Online and new Exchange Online Dedicated with Intune](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-exchange-online-with-microsoft-intune)
  * [Restrict access to SharePoint Online with Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-sharepoint-online-with-microsoft-intune)

- **Dynamics CRM Online supports conditional access**

  You can set a conditional access policy for Dynamics CRM Online so that it can only be accessed by managed and compliant iOS and Android devices. End users who try to sign in to the Dynamics CRM mobile app on iOS and Android will be prompted to enroll with Intune as well as remediate any non-compliance issues before sign-in can complete. For more information, see [Restrict access to Dynamics CRM Online with Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-dynamics-crm-online-with-microsoft-intune).

- **Updates to the Android Company Portal app**

  Intune now has the following new policies that will affect Android Company Portal users:   

  Policy  |Effect on users  
  ---------|---------
  Require that devices disallow installation of apps from unknown sources (Android 4.0+)     |  End users with Android 4.0 or later devices will see the message, "Installation from Unknown sources must be disabled." Users will need to go to **Settings > Security** on their devices, and turn off **Unknown sources**. A link in the compliance message lets users get more information about the message and why they are being required to turn off the setting.
  Require that devices disallow installation of apps from unknown sources (Android 4.0+)  |    End users with Android 4.0 or later devices will see the message, "Scan device for security threats." Users will need to go to **Settings > Google > Security** on their devices, and turn on **Scan device for security threats**. A link in the compliance message lets users get more information about the message and why they are being required to turn on the setting.     
  Require that USB debugging is disabled (Android 4.2+)  | End users with Android 4.2 or later devices will see the message, "USB debugging must be disabled." Users will need to go to **Settings > Developer options** on their devices, and turn off **USB debugging**. A link in the compliance message lets users get more information about the message and why they are being required to turn off the setting.
  Minimum Android security patch level (Android 6.0+)  | End users with Android 6.0 or later devices will see the message, "This device does not meet the minimum Android security patch level." Users will need to install the required security patch. A link in the compliance message lets users get information about how to install the required security patch and to see which security patch they currently have installed.

- **Updates to the iOS Company Portal app**

  * When end users are installing line-of-business apps, they will now see an improved app installation experience. If the app installation is taking a long time, users can manually sync their device to force the sync process to resume. To review the end-user instructions, see Sync your iOS device manually.
  * The Microsoft Intune Company Portal app for iOS has been updated to support iOS version 8.0 and later. This update means that end users can install the Company Portal app and enroll new devices in Intune only if the device is running iOS version 8.0 or later. Users who have already enrolled devices that are running on an unsupported version of iOS can continue to use the Company Portal app that is on their device.

### <a name="TP1606"></a> New in Configuration Manager Technical Preview
The following new features introduced in June 2016 are available in hybrid deployments with Intune and Configuration Manager Technical Preview 1606. These features require you to use the Configuration Manager console to configure and manage them.

- **Automatically categorize devices into collections**

  You can create device categories, which can be used to automatically place devices in device collections when you are using Configuration Manager with Intune. Users are then required to choose a device category when they enroll a device in Intune. You can additionally change the category of a device from the Configuration Manager console. For more information, see [Automatically categorize devices into collections](../../core/get-started/capabilities-in-technical-preview-1606.md#dmp_category) in [Capabilities in Technical Preview 1606 for System Center Configuration Manager](../../core/get-started/capabilities-in-technical-preview-1606.md).

  > [!IMPORTANT]
  > This capability works with the June 2016 release of Microsoft Intune. Ensure that you have been updated to this release before you try out these procedures.

### New in Configuration Manager (current branch)
No new hybrid features have been introduced in June 2016 for Configuration Manager (current branch).

##  <a name="May"></a> New hybrid features in May 2016  

### New in Microsoft Intune  
 The following  features introduced in May 2016 work in hybrid deployments exactly as they do in the standalone Intune service. No changes or administration in Configuration Manager are required to use these features.  

- **MAM SDK: Support PIN length configuration**

  You can now specify the length of the PIN for MAM apps similar to a device PIN. This requires end users to comply with the new restrictions you set. The PIN screen is slightly modified to account for the longer input. For details, see [MAM policy settings for Android](https://docs.microsoft.com/intune/deploy-use/android-mam-policy-settings), and [MAM policy settings for iOS](https://docs.microsoft.com/intune/deploy-use/ios-mam-policy-settings).  

- **Skype for Business for iOS and Android**

  You can now target Skype for business with [MAM without enrollment policies](https://docs.microsoft.com/intune/deploy-use/get-ready-to-configure-mobile-app-management-policies-with-microsoft-intune). Once users log in, the MAM policies will be applied.  

- **New apps available for management with MAM policies**

  The Microsoft Word, Excel, and PowerPoint apps for Android can now be associated with MAM policies on devices that are not enrolled with Intune. For a full list of supported apps, go the Microsoft Intune mobile application gallery on the [Microsoft Intune application partners](https://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/partners.aspx) page.  

- **Android Company portal app: End user toast notifications**

  Toast notifications from the Android Company Portal app appear when end users enroll or remove their devices from the Company Portal.  

- **Company Portal website: Device identification banner will provide more information to end users**

  End users can now more easily identify the device they’ve selected when they are using the Company Portal website. If the wrong device is selected, they can select the correct device by tapping the **Tap here** link in the home page banner.  

### <a name="TP1605"></a> New in Configuration Manager Technical Preview  
 The following new features introduced in May 2016 are available in hybrid deployments with Intune and Configuration Manager Technical Preview 1605. These features require you to use the Configuration Manager console to configure and manage them.  

- **App-triggered VPN for Windows 10 devices**

  For Windows 10 devices managed using Configuration Manager with Intune, you can add a list of apps that automatically open a VPN connection that you have configured through the Configuration Manager admin console. For more information, see [App-triggered VPN for Windows 10 devices](../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_PerAppVPN) in [Capabilities in Technical Preview 1605 for System Center Configuration Manager](../../core/get-started/capabilities-in-technical-preview-1605.md)  

- **New experience for remote device actions**

  The experience for performing remote device actions from the Configuration Manager console has been improved.

  Common actions such as **Retire/Wipe**, **Reset Passcode**, **Remote Lock**, and **Bypass Activation Lock** can now be found in the **Remote Device Actions** menu accessed from the **Assets and Compliance** workspace

  For more information, see [New experience for remote device actions](../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_Remote) in [Capabilities in Technical Preview 1605 for System Center Configuration Manager](../../core/get-started/capabilities-in-technical-preview-1605.md).  

- **Windows Store for Business apps**

  The [Windows Store for Business](https://www.microsoft.com/en-us/business-store) is where you can find and purchase apps for your organization, individually or in volume. By connecting the store to Configuration Manager, you can manage volume-purchased apps from the Configuration Manager console. For more information, see [Windows Store for Business apps](../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_WSFB) in [Capabilities in Technical Preview 1605 for System Center Configuration Manager](../../core/get-started/capabilities-in-technical-preview-1605.md).  

- **General improvements for volume-purchased apps**

  Volume-purchased apps from the Windows Store for Business and the iOS app store have been consolidated into the same view, **License Information for Store Apps**. Also, the way in which you create volume-purchased apps for iOS has been improved. For more information, see[General improvements for volume-purchased apps](../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_VPP2) in [Capabilities in Technical Preview 1605 for System Center Configuration Manager](../../core/get-started/capabilities-in-technical-preview-1605.md).  

- **Pre-declare corporate-owned devices with IMEI or iOS serial number**

  You can now identify corporate-owned devices by importing their international station mobile equipment identity (IMEI) numbers. You can upload a comma-separated values (.csv) file containing device IMEI numbers or you can manually enter device information.  You can also import serial numbers for iOS devices.  For more information, see [Pre-declare corporate-owned devices with IMEI or iOS serial number](../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_IMEI) in [Capabilities in Technical Preview 1605 for System Center Configuration Manager](../../core/get-started/capabilities-in-technical-preview-1605.md).  

- **Windows Information Protection (WIP)**

  You can create configuration items that let you deploy your Windows Information Protection (WIP) policies, including letting you choose your protected apps, your WIP-protection level, and how to find enterprise data on the network. For more information about WIP, see the following topics:  

  -   [Protect your enterprise data using Windows Information Protection (WIP)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip)  

  -   [Create and deploy a Windows Information Protection (WIP) policy using System Center Configuration Manager](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-sccm)  

### New in Configuration Manager (current branch)  
 No new hybrid features have been introduced in May 2016 for Configuration Manager (current branch).  

##  <a name="april"></a> New hybrid features in April 2016  

### New in Microsoft Intune  
 The following  features introduced in April 2016 work in hybrid deployments exactly as they do in the standalone Intune service. No changes or administration in Configuration Manager are required to use these features.  

- **MAM user compliance**

  You can now view the status of your application management policies for any user in your Azure Active Directory (AAD) tenant.  For more information see [Monitor mobile app management policies with Microsoft Intune](https://technet.microsoft.com/library/mt627824.aspx) in the Intune library.  

- **MAM controls to prevent Outlook contacts sync (Android)**

  A new setting is available that allows you to prevent an application from syncing contacts to the native address book on Android devices. This new setting is supported initially by the Outlook application on Android devices. For more information, see [Create and deploy mobile app management policies with Microsoft Intune](https://technet.microsoft.com/library/mt627829.aspx) in the Intune library.  

- **Improvements to the Company Portal website**

  When Windows 10 Mobile and Windows Phone 8.1 users are installing line-of-business apps, they will now see the following new statuses, which provide them with more detail about the status of their installation:  

  -   **Waiting for device to sync** – the user has tapped “Install” and the device now tries to sync with the Intune infrastructure. The sync is required before the installation can complete. The "Waiting for device to sync" message is also a link that users can tap to see instructions on how to manually sync their device with Intune if the sync process is taking a long time or gets stalled.  

  -   **Downloading** – the user’s download request is being processed and the device is downloading and installing the app.  

- **Improvements to the Android Company portal app**

  Users who have not enrolled their device in Intune and who do not have the correct certificate installed will not be able to sign in to the Android Company Portal app and will see the message, “You cannot sign in because your device is missing a required certificate.” The message includes a “How to resolve this” link that users can tap to see instructions for installing the certificate. To see the steps that end users follow to resolve the issue, see [Your device is missing a required certificate](https://technet.microsoft.com/library/mt502762.aspx) in the Intune library.  

- **Improvements to the iOS Company Portal app**

  Support has been added for the pull-to-refresh action to refresh the content on the home screen, which includes listed apps, listed devices, and IT contact information. The pull-to-refresh action does not check compliance or policy information, which can be done by selecting the tile for your current device and tapping the **Sync** button.  

- **Improvements to Windows 10 Mobile and Windows Phone 8.1 Company Portal app**

  When end users are installing line-of-business apps, they will now see an improved app installation experience. If the app installation is taking a long time, users can manually sync their device to force the sync process to resume. To review the end-user instructions, see [Sync your device manually to speed up app installations](https://technet.microsoft.com/library/mt427782.aspx) in the Intune library.  

### <a name="TP1604"></a> New in Configuration Manager Technical Preview  
 The following new features introduced in April 2016 are available in hybrid deployments with Intune and Configuration Manager Technical Preview 1604. These features require you to use the Configuration Manager console to configure and manage them.  

- **Find, manage, and distribute Windows Store for Business apps for Windows 10 devices from the Configuration Manager console**

  Support for Windows Store for Business is available in Configuration Manager Technical Preview 1604 to help you find, manage, and distribute apps to the Windows 10 devices you’re managing. For details, see [Manage volume-purchased apps from the Windows Store for Business](../../core/get-started/capabilities-in-technical-preview-1604.md#BKMK_WindowsVPP) in [Capabilities in Technical Preview 1604 for System Center Configuration Manager](../../core/get-started/capabilities-in-technical-preview-1604.md).  

- **SmartLock setting for Android devices**

  A new setting has been added to the Android and Samsung KNOX configuration item that lets you control the SmartLock feature on compatible Android devices.  You can use this setting to prevent end users from configuring SmartLock. See [SmartLock setting for Android devices](../../core/get-started/capabilities-in-technical-preview-1604.md#BKMK_Smart) in [Capabilities in Technical Preview 1604 for System Center Configuration Manager](../../core/get-started/capabilities-in-technical-preview-1604.md).  

### New in Configuration Manager (current branch)  
 No new hybrid features were introduced in April 2016 for Configuration Manager (current branch).  

##  <a name="march"></a> New hybrid features in March 2016  

### New in Microsoft Intune  
 The following Intune features introduced in March 2016 work in hybrid deployments exactly as they do in the standalone Intune service. No changes or administration in Configuration Manager are required to use these features.  

- **MAM controls to prevent Outlook contacts sync (iOS)**

  A new setting is available that allows you to prevent an application from syncing contacts to the native address book on iOS devices. This new setting is supported by the Outlook application on iOS devices. For more details about this and other settings, see [Create and deploy MAM policies](https://technet.microsoft.com/library/mt627829.aspx) in the Intune library.  

- **Skype for Business Online supports conditional access**

  You can set a conditional access policy for Skype for Business Online so that it can only be accessed by managed and compliant iOS and Android devices.  For details, see [Manage access to Skype for Business Online](https://technet.microsoft.com/library/mt695297.aspx) in the Intune library.  

- **Support for iOS 9.3**

  On Monday March 21st, Apple announced the availability of iOS 9.3. All existing Intune features currently available for managing iOS devices will continue to work seamlessly as users upgrade their devices to iOS 9.3.  

- **Windows app packages available directly from the Company Portal website**

  Users of Windows 8, Windows 8.1, and Windows RT PCs can now install Windows app packages (with the .appx extension) directly from the Company Portal website. Previously, you had to deploy, or users had to install the Company Portal app on their devices to install apps.  

- **Users can remotely lock their device from the Company Portal website**

  A new Remote Lock option has been added to the Company Portal website to enable users to remotely lock their device from the Portal if their device is lost or stolen.  

- **Take advantage of iOS "Open-in" management for devices that are enrolled in a third-party MDM solution**

  You can use your third-party mobile device management (MDM) vendor to take advantage of iOS "Open-In" management. You can set the restrictions in the configuration profile settings and deploy the app using your MDM software. When the user installs the managed app, the restrictions are applied. Read the details: [Microsoft Intune mobile app management policies and iOS Open In](https://technet.microsoft.com/library/mt627821.aspx) in the Intune library.  

- **Microsoft apps that support MAM**

  The list of Microsoft apps you can use with Intune mobile application management policies has been updated to include the latest apps (for devices that are enrolled with Intune only).  

- **Deploy Adobe Reader for Microsoft Intune to Intune-managed iOS devices in your enterprise**

  The Adobe Reader app for iOS can now be managed on enrolled devices with the Intune mobile application management policy.  

- The Rights Management sharing app is supported for Android

  IT administrators can deploy mobile application management policies so end users can view images, AV, and PDF files more securely, whether or not IT uses Intune to manage the devices.  

- **Improvements to the Android and iOS Company Portal app**

  -   When your users launch an app that is managed by mobile application management (MAM), they will see a message notifying them that the app is managed by their company. Users can now tap a “Learn More” link to get more information here about what “managed apps” means. They can also tap “Don’t Show Again” so that the message no longer appears when they launch the app.  

  -   New screens have been added to guide users through the enrollment process and provide more information about why users should enroll and what IT administrators can and can’t see on their enrolled devices.  

  -   Enrollment error messages are now displayed in the Company Portal app.  

### New in Configuration Manager Technical Preview  
 No new hybrid features were introduced in March 2016 for Configuration Manager Technical Preview.  

### New in Configuration Manager (current branch)  
 The following new features introduced in March 2016 are available in hybrid deployments with Intune and Configuration Manager (current branch) version 1602. These features require you to use the Configuration Manager console to configure and manage them.  

- **iOS app configuration policies**

  In version 1602 of Configuration Manager (current branch) you can use app configuration policies to supply settings that might be required when the user runs an iOS app. For details, see [Configure iOS apps with app configuration policies in System Center Configuration Manager](../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md).  

- **Manage volume-purchased iOS apps**

  In version 1602 of Configuration Manager (current branch), you can deploy and manage apps you purchased in volume from the Apple Volume-Purchase Program (VPP) by importing the license information from the app store and tracking how many of the licenses you have used. For details, see [Manage volume-purchased iOS apps with System Center Configuration Manager](../../apps/deploy-use/manage-volume-purchased-ios-apps.md).  

- **Automatic creation of Office mobile apps**

  Beginning in version 1602 of Configuration Manager (current branch), the following Microsoft Office mobile apps for Android and iOS are created when you upgrade from version 1511:  

  -   Microsoft Word  
  -   Microsoft Excel  
  -   Microsoft PowerPoint  
  -   Microsoft OneDrive  
  -   Microsoft OneNote (iOS only)  
  -   Microsoft Outlook  

  You will find these apps in the Applications node of the Configuration Manager console. For more information about deploying applications, see [How to deploy applications with System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md).  

- **Kiosk mode settings for Android Samsung KNOX devices**

  Kiosk mode allows you to lock a device to only allow certain features to work.  Beginning in version 1602 of  Configuration Manager (current branch), you can now specify kiosk mode settings for Samsung KNOX devices. For details, see [How to create configuration items for Android and Samsung KNOX devices managed without the System Center Configuration Manager client](../../compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md).  

- **iOS Activation Lock**

  Beginning in version 1602 of Configuration Manager (current branch), you can manage iOS Activation Lock, a feature of the Find My iPhone app for iOS 7.1 and later devices. Activation Lock is enabled automatically when the Find My iPhone app is used on a device.  For details, see [Manage iOS Activation Lock bypass for System Center Configuration Manager](/sccm/mdm/deploy-use/manage-ios-activation-lock#bypass-activation-lock).  

### See Also  
 [What's new for MDM in System Center 2012 Configuration Manager](https://technet.microsoft.com/library/mt445560.aspx)
