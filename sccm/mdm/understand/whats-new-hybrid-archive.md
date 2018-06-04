---
title: Archive of  What's new hybrid MDM
titleSuffix: Configuration Manager
description: Archive of past mobile device management features available for hybrid deployments with System Center Configuration Manager and Intune.
ms.date: 05/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 4c27b161-9eb7-4cdd-b469-d8eb27e71aea
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: "NOINDEX, NOFOLLOW"
---
# Past hybrid features with System Center Configuration Manager and Microsoft Intune

*Applies to: System Center Configuration Manager (Current Branch)*

This article provides details on the past mobile device management (MDM) features available for hybrid deployments with System Center Configuration Manager and Microsoft Intune.  

##  Compatibility with Configuration Manager versions  

 Each section of this article lists hybrid features under 3 different categories. Use the following guidance to determine compatibility of the features in each category  with different versions of Configuration Manager:  

|Feature categories|
|-|  
|**New in Microsoft Intune** - In general, all the features listed under this category should work with all Configuration Manager releases including System Center 2012 R2 Configuration Manager releases, since these features only require the  Intune service and do not require additional functionality in  Configuration Manager.<br /><br /> **New in Configuration Manager Technical Preview** - All the features listed under this category only work with the specified Technical Preview release. To try out these features, you must install the Technical Preview version specified in the feature description. For more information, see [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md).<br /><br /> **New in Configuration Manager (current branch)** - All the features listed under this category only work with the specified version of Configuration Manager (current branch), such as version 1511 or 1602. If you're using an older version of Configuration Manager for your hybrid deployment, you must upgrade to the Configuration Manager (current branch)  version specified in the feature description. For more information, see [Upgrade to System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md).|  



## April 2017

### New in Microsoft Intune

- **MyApps available for Managed Browser**  
  Microsoft MyApps now have better support within the Managed Browser. Managed Browser users who aren't targeted for management are brought directly to the MyApps service, where they can access their admin-provisioned SaaS apps. Users who are targeted for Intune management continue to access MyApps from the built-in Managed Browser bookmark.

- **New icons for the Managed Browser and the Company Portal**  
  The Managed Browser is receiving updated icons for both the Android and iOS versions of the app. The new icon contains the updated Intune badge to make it more consistent with other apps in Enterprise Mobility + Security (EM+S). You can see the new icon for the Managed Browser on the [what's new in Intune app UI page](https://docs.microsoft.com/intune/whats-new-app-ui).

  The Company Portal is also receiving updated icons for the Android, iOS, and Windows versions of the app to improve consistency with other apps in EM+S. These icons are gradually released across platforms from April to late May.

- **Sign-in progress indicator in Android Company Portal**  
  An update to the Android Company Portal app shows a sign-in progress indicator when the user launches or resumes the app. The indicator progresses through new statuses, beginning with "Connecting...", then "Signing in...", then "Checking for security requirements..." before allowing the user to access the app. You can see the new screens for the Company Portal app for Android on the [what's new in Intune app UI page](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Block apps from accessing SharePoint Online**  
  You can now create an app-based conditional access policy to block apps, which don't have app protection policies applied to them, from accessing [SharePoint Online](https://docs.microsoft.com/intune-classic/deploy-use/mam-ca-for-sharepoint-online). In the apps-based conditional access scenario, you can specify the apps that you want to have access to SharePoint Online using the Azure portal.

### New in Configuration Manager Technical Preview 1704

- **Configure Android apps with app configuration policies**  
  When a user runs an app on Android for Work devices, use app configuration policies in Configuration Manager to distribute pre-configured settings. Android app configuration policies are available only on devices running Android for Work. These policies apply to approved apps from the Play for Work store. For more information, see [Configure Android apps with app configuration policies](/sccm/core/get-started/capabilities-in-technical-preview-1704#configure-android-apps-with-app-configuration-policies).



## March 2017

### New in Microsoft Intune

- **New user experience for the Company Portal app for Android**  
  The Company Portal app for Android has a more modern look and feel to its user interface. The notable updates are:

  - Colors: Company Portal tab headers are colored in IT-defined branding.
  - Apps: In the **Apps** tab, the **Featured Apps** and **All Apps** buttons are updated.
  - Search: In the **Apps** tab, the **Search** button is a floating action button.
  - Navigating Apps: **All Apps** view shows a tabbed view of **Featured**, **All**, and **Categories** for easier navigation.
  - Support: **My Devices** and **Contact IT** tabs are updated to improve readability.

  For more information about these changes, see [UI updates for Intune end-user apps](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Signing Script for Windows 10 Company Portal**  
  If you need to download and sideload the Windows 10 Company Portal app, you can now use a script to simplify and streamline the app-signing process for your organization. To download the script and the instructions for using it, see  [Microsoft Intune Signing Script for Windows 10 Company Portal](https://aka.ms/win10cpscript) on TechNet Gallery. For more information about this announcement, see [Updating your Windows 10 Company Portal app](https://blogs.technet.microsoft.com/intunesupport/2017/03/13/updating-your-windows-10-company-portal-app/) on the Intune Support Team Blog.

- **Improved support for Android users based in China**  
  Due to the absence of the Google Play Store in China, Android devices must obtain apps from Chinese marketplaces. The Company Portal supports this workflow. It redirects Android users in China to download the Company Portal and Outlook apps from local app stores. This behavior improves the user experience when Conditional Access policies are enabled, both for Mobile Device Management and for Mobile Application Management. The Company Portal and Outlook apps for Android are available on the following Chinese app stores:

  - [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
  - [Xiaomi](https://go.microsoft.com/fwlink/?linkid=836947)
  - [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
  - [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
  - [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)

- **Make sure your Company Portal apps are up-to-date**  
  In December 2016, we released an update that enabled enforcement for multi-factor authentication (MFA) on a group of users when they enroll an iOS, Android, Windows 8.1+, or Windows Phone 8.1+ device. This feature can't work without certain baseline versions of the Company Portal app for Android (v5.0.3419.0+) and iOS (v2.1.17+).

  Intune's management capabilities are continuously improving. Many improvements have coordinated updates to the Company Portal apps on all supported platforms. We recommend you keep the latest versions of the Company Portal apps on installed on devices. This practice takes advantage of improvements in Intune and for the best user experience.

  >[!Tip]
  > Have your users set their devices to automatically update apps from the appropriate app store. If you have made the Android Company Portal app available on a network share, you can download the latest version from [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=49140).

- **Microsoft Teams is now enabled for MAM on iOS and Android**  
  The Microsoft Teams apps for iOS and Android are now enabled with Intune mobile app management (MAM) capabilities. Empower your teams to work freely across devices, while ensuring that conversations and corporate data are protected. For more information, see [the Microsoft Teams announcement](https://blogs.technet.microsoft.com/enterprisemobility/2017/03/14/microsoft-teams-is-now-generally-available-and-mam-enabled-on-ios-and-android/) on the Enterprise Mobility and Security blog.

### New in Configuration Manager Technical Preview 1703

- **Additional support for Apple Volume Purchase Program scenarios**  
   Beginning in Technical Preview 1703, you now have support for the following Volume Purchase Program (VPP) scenarios:

   - Device licensing - Apps that support device licensing and are deployed to device collections now only require one license per device. Previously, you had to use a license for each user on a device. For more information, see [Deploy volume-purchased iOS apps to device collections](/sccm/core/get-started/capabilities-in-technical-preview-1703#deploy-volume-purchased-ios-apps-to-device-collections).
   - Use of multiple VPP tokens to a single hybrid tenant with both tokens used for managing VPP apps.
   - Use of VPP education tokens with the ability to distinguish between business and education tokens.

### New in Configuration Manager (current branch)

The following features were previously available in Configuration Manager Technical Preview releases. These features are now available in hybrid deployments with Intune and Configuration Manager (current branch) version 1702.

- [Android for Work Support](/sccm/core/plan-design/changes/whats-new-in-version-1702##android-for-work-support)
- [Non-Compliant Apps Compliance Settings](/sccm/core/plan-design/changes/whats-new-in-version-1702#conditional-access-device-compliance-policy-improvements)
- [PFX Certificate Creation and Distribution and S/MIME Support](/sccm/core/plan-design/changes/whats-new-in-version-1702#improvements-to-certificate-profiles)
- [Android and iOS versions are no longer targetable in creation wizards for hybrid MDM](/sccm/core/plan-design/changes/whats-new-in-version-1702#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm)

The following additional hybrid features are also included in version 1702 of Configuration Manager (current branch):

- **Improved support for Apple Volume Purchase Program (VPP)**  
  - You can now deploy licensed apps to devices as well as users. Depending on the apps ability to support device licensing, an appropriate license is claimed when you deploy it, as follows:

    | Configuration Manager version | App supports device licensing? | Deployment collection type | Claimed license |
    |-|-|-|-|
    |Earlier than 1702|Yes|User|User license|
    |Earlier than 1702|No|User|User license|
    |Earlier than 1702|Yes|Device|User license|
    |Earlier than 1702|No|Device|User license|
    |1702 and later|Yes|User|User license|
    |1702 and later|No|User|User license|
    |1702 and later|Yes|Device|Device license|
    |1702 and later|No|Device|User license|

  - You can now also deploy and track apps you purchased from the iOS Volume Purchase Program for Education.

  - You can now associate multiple Apple volume-purchase program tokens with Configuration Manager.

  For more information about volume-purchased iOS apps, see [Manage volume-purchased iOS apps](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

- **Support for line-of-business apps in Microsoft Store for Business**  
  You can now sync custom line-of-business apps from the Microsoft Store for Business.

- **New Mobile Threat Defense monitoring tools**  
    You now have new ways to monitor the compliance status with your Mobile Threat Defense service provider.

    For more information, see [how to monitor Mobile Threat Defense compliance](/sccm/mdm/deploy-use/monitor-mobile-threat-defense-compliance).





## February 2017

### New in Microsoft Intune

- **Modernizing the Company Portal website**

  The Company Portal website supports apps that are targeted to users who do not have managed devices. The website aligns with other Microsoft products and services by using a new contrasting color scheme, dynamic illustrations, and a "hamburger menu," which contains helpdesk contact details and information on existing managed devices. The landing page is rearranged to emphasize apps that are available to users, with carousels for Featured and Recently Updated apps. You can find before-and-after images available on the [UI updates](https://docs.microsoft.com/intune/whats-new-app-ui) page.

- **New MDM server address for Windows devices**

  The MDM server address for enrolling Windows and Windows Phone devices has changed from manage.microsoft.com to enrollment.manage.microsoft.com. Notify your user to use enrollment.manage.microsoft.com as the MDM server address if prompted for it while enrolling a Windows or and Windows Phone device. This update also requires any CNAME in DNS that redirects EnterpriseEnrollment.contoso.com to manage.microsoft.com to be replaced with a CNAME in DNS that redirects EnterpriseEnrollment.contoso.com to EnterpriseEnrollment-s.manage.microsoft.com. For additional information about this change, visit http://aka.ms/intuneenrollsvrchange.

### New in Configuration Manager Technical Preview 1702

- **Android for Work Support**

  You can now manage Android devices using Android for Work in hybrid MDM environments using Configuration Manager Technical Preview 1702. Supported Android devices can now be enrolled as Android for Work devices, which creates a work profile on the device to which apps approved in Play for Work can be deployed. You can also configure and deploy configuration items, compliance policies, and resource access profiles for these devices. For more information, see [Android for Work support](/sccm/core/get-started/capabilities-in-technical-preview-1702#android-for-work-support).

- **Non-Compliant Apps Compliance Settings**

  You can now create non-compliant apps rules for Android and iOS apps in compliance policies. If devices have the specified applications installed, they are marked “non-compliant” and lose access to company resources according to conditional access policies in place. For more information, see [Conditional access device compliance policy improvements](/sccm/core/get-started/capabilities-in-technical-preview-1702#conditional-access-device-compliance-policy-improvements).

- **PFX Certificate Creation and Distribution and S/MIME Support**

  You can now create and deploy PFX certificates to users in a hybrid environment. These certificates can then be used for S/MIME email encryption and decryption by devices that the user has enrolled. For more information, see [Create PFX certificates with S MIME support](/sccm/core/get-started/capabilities-in-technical-preview-1702#create-pfx-certificates-with-s-mime-support).

- **Support for additional iOS configuration settings**
   
    You now have 42 additional iOS settings that you can configure as part of a configuration item. Most of the settings (35 in all) have been added for supervised iOS devices. For more information, see  [New compliance settings for iOS devices](/sccm/core/get-started/capabilities-in-technical-preview-1702#new-compliance-settings-for-ios-devices).



## January 2017

### New in Microsoft Intune

- **Android 7.1.1 support**

  Intune now fully supports and manages Android 7.1.1.

- **Resolve issue where iOS devices are inactive, or the admin console cannot communicate with them**

  When users’ devices lose contact with Intune, you can give them new troubleshooting steps to help them regain access to company resources. See [Devices are inactive, or the admin console cannot communicate with them](https://docs.microsoft.com/intune/troubleshoot/troubleshoot-device-enrollment-in-intune#devices-are-inactive-or-the-admin-console-cannot-communicate-with-them).

### New in Configuration Manager Technical Preview 1701

- **Android and iOS versions are no longer targetable in creation wizards for hybrid MDM**

  Beginning in Technical Preview 1701 for hybrid mobile device management (MDM), you no longer need to target specific versions of Android and iOS when creating new policies and profiles for Intune-managed devices. With this change, hybrid deployments can provide support more quickly for new Android and iOS versions without needing a new Configuration Manager release or extension. To learn more, see [Android and iOS versions are no longer targetable in creation wizards](/sccm/core/get-started/capabilities-in-technical-preview-1701#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm).



## December 2016

### New in Microsoft Intune

- **Multi-Factor authentication (MFA) on enrollment is moving to the Azure portal**

  Previously, you would go to either the Intune console or the Configuration Manager console to set MFA for Intune enrollments. With this updated feature, you now login to the [Microsoft Azure portal] (https://manage.windowsazure.com) using your Intune credentials and configure MFA settings through Azure AD. To learn more, see [Multi-factor authentication for Microsoft Intune] (https://aka.ms/mfa_ad).

- **Company Portal app for Android now available in China**

  The Company Portal app for Android is now available in China. Due to the absence of Google Play Store in China, Android devices must obtain apps from Chinese app marketplaces. The Company Portal app for Android is available for download on the following stores:

  -	[Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
  -	[Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
  -	[Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
  -	[Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)
  -	[Xiaomi](https://go.microsoft.com/fwlink/?linkid=836947)

  The Company Portal app for Android uses Google Play Services to communicate with the Microsoft Intune service. Since Google Play Services are not yet available in China, performing any of the following tasks can take up to 8 hours to complete.

  | Configuration Manager Admin Console | Intune Company Portal app for Android | Intune Company Portal Website |
  |----|----|----|		
  | Retire/wipe (remove all data)	| Remove a remote device | Remove device (local and remote) |
  | Retire/wipe (remove company data)	| Reset device | Reset device|
  | New or updated app deployments | Install available line-of-business apps | Device passcode reset|
  | Remote lock	| | |
  | Passcode reset | | |		


## November 2016

### New in Microsoft Intune

- **New Microsoft Intune Company Portal available for Windows 10 devices**

  Microsoft has released a new [Company Portal app for Windows 10 devices](https://www.microsoft.com/store/apps/9wzdncrfj3pz). This app, which leverages the new Windows 10 Universal format, provides an updated user experience that is identical across all Windows 10 devices, PC and Mobile alike, while still enabling all the same functionality provided by previous Company Portal apps.

  The new app leverages platform features like single sign-on (SSO) and certificate-based authentication on Windows 10 devices. The app is available as an upgrade to the existing Windows 8.1 Company Portal and Windows Phone 8.1 Company Portal installs from the Windows Store. For more details, go to the [Intune Support Team Blog](http://aka.ms/intunecp_universalapp).

  The new Company Portal app also displays any Windows Store for Business applications marked **Available** in the Configuration Manager console.


### New in Configuration Manager (current branch)

The following features that were previously available in Configuration Manager Technical Preview releases are now available in hybrid deployments with Intune and Configuration Manager (current branch) version 1610.

* [Additional settings and improved experience for Configuration items](/sccm/core/plan-design/changes/whats-new-in-version-1610#new-compliance-settings-for-configuration-items)
* [Additional settings for DEP profiles](whats-new-hybrid-archive.md#new-in-configuration-manager-technical-preview-1609)
* [Paid apps in Windows Store for Business](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)
* [Native connection types for Windows 10 VPN profiles](whats-new-hybrid-archive.md#new-in-configuration-manager-technical-preview-1609)
* [Intune compliance charts](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)
* [Request to policy sync from console](/sccm/mdm/deploy-use/sync-intune-device)
* [Windows Defender configuration settings](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client#windows-defender)

The following additional hybrid features are also included in version 1610 of Configuration Manager (current branch):

- **Increased number of enrolled devices**

  You can now enable users to enroll up to 15 devices. The previous limit was 5 devices per user.


- **Addtional security support**

  In addition to Full Administrator, the following built-in security roles now have full access to items in the All Corporate-owned Devices node, including Predeclared Devices, iOS Enrollment Profiles, and Windows Enrollment Profiles:

    - Asset Manager
    - Company Resource Access Manager

  Read-only access to these areas of the Configuration Manager console is still granted to the Read-only Analyst role.

- **Auto-trigger VPN access from Windows Information Protection apps**

  You can add a Windows Information Protection primary domain to Windows 10 VPN profiles that causes all associated apps to automatically trigger a VPN connection when they are run on the device. This option is only available when choosing a native connection type.

- **Conditional access for Windows 10 VPN profiles**

    You can now require Windows 10 devices enrolled in Azure Active Directory to be compliant in order to have VPN access through Windows 10 VPN profiles created in the Configuration Manager console. This is possible through the new **Enable conditional access for this VPN connection** checkbox on the Authentication Method page in the VPN profile wizard and VPN profile properties for Windows 10 VPN profiles. This option is only available when choosing a native connection type.

    You can also specify a separate certificate for single sign-on authentication if you enable conditional access for the profile.

## October 2016

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

## September 2016

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

## August 2016

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

## July 2016

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

* Find, manage, and distribute Windows Store for Business apps for Windows 10 devices from the Configuration Manager console ([1604](#new-in-1604-technical-preview))
* 	SmartLock setting for Android devices ([1604](#new-in-1604-technical-preview))
*	App-triggered VPN for Windows 10 devices ([1605](#new-in-1605-technical-preview))
*	New experience for remote device actions ([1605](#new-in-1605-technical-preview))
*	Windows Store for Business apps ([1605](#new-in-1605-technical-preview))
*	General improvements for volume-purchased apps ([1605](#new-in-1605-technical-preview))
*	Windows Information Protection (WIP) ([1605](#new-in-1605-technical-preview))
*	Pre-declare corporate-owned devices with IMEI or iOS serial number ([1605](#new-in-1605-technical-preview))
*	Automatically categorize devices into collections ([1606](#new-in-1606-technical-preview))

For information on the new functionality, see the documentation for the specified Technical Preview release.

## June 2016

### New in Microsoft Intune
The following Intune features introduced in June 2016 work in hybrid deployments.

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


### New in 1606 Technical Preview
The following new features introduced in June 2016 are available in hybrid deployments with Intune and Configuration Manager Technical Preview 1606.

- **Automatically categorize devices into collections**

  You can create device categories, which can be used to automatically place devices in device collections when you are using Configuration Manager with Intune. Users are then required to choose a device category when they enroll a device in Intune. You can additionally change the category of a device from the Configuration Manager console. For more information, see [Automatically categorize devices into collections](/sccm/core/get-started/capabilities-in-technical-preview-1606#dmp_category) in [Capabilities in Technical Preview 1606 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1606).

  > [!IMPORTANT]
  > This capability works with the June 2016 release of Microsoft Intune. Ensure that you have been updated to this release before you try out these procedures.

### New in Configuration Manager (current branch)
No new hybrid features have been introduced in June 2016 for Configuration Manager (current branch).

##  May 2016  

### New in Microsoft Intune  
 The following Intune features introduced in May 2016 work in hybrid deployments.

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


### New in 1605 Technical Preview  
 The following new features introduced in May 2016 are available in hybrid deployments with Intune and Configuration Manager Technical Preview 1605. These features require you to use the Configuration Manager console to configure and manage them.  

- **App-triggered VPN for Windows 10 devices**

  For Windows 10 devices managed using Configuration Manager with Intune, you can add a list of apps that automatically open a VPN connection that you have configured through the Configuration Manager admin console. For more information, see [App-triggered VPN for Windows 10 devices](/sccm/core/get-started/capabilities-in-technical-preview-1605) in [Capabilities in Technical Preview 1605 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605)  

- **New experience for remote device actions**

  The experience for performing remote device actions from the Configuration Manager console has been improved.

  Common actions such as **Retire/Wipe**, **Reset Passcode**, **Remote Lock**, and **Bypass Activation Lock** can now be found in the **Remote Device Actions** menu accessed from the **Assets and Compliance** workspace

  For more information, see [New experience for remote device actions](/sccm/core/get-started/capabilities-in-technical-preview-1605#new-experience-for-remote-device-actions) in [Capabilities in Technical Preview 1605 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Windows Store for Business apps**

  The [Windows Store for Business](https://www.microsoft.com/en-us/business-store) is where you can find and purchase apps for your organization, individually or in volume. By connecting the store to Configuration Manager, you can manage volume-purchased apps from the Configuration Manager console. For more information, see [Windows Store for Business apps](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#windows-store-for-business-apps) in [Capabilities in Technical Preview 1605 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **General improvements for volume-purchased apps**

  Volume-purchased apps from the Windows Store for Business and the iOS app store have been consolidated into the same view, **License Information for Store Apps**. Also, the way in which you create volume-purchased apps for iOS has been improved. For more information, see[General improvements for volume-purchased apps](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#general-improvements-for-volume-purchased-apps) in [Capabilities in Technical Preview 1605 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Pre-declare corporate-owned devices with IMEI or iOS serial number**

  You can now identify corporate-owned devices by importing their international station mobile equipment identity (IMEI) numbers. You can upload a comma-separated values (.csv) file containing device IMEI numbers or you can manually enter device information.  You can also import serial numbers for iOS devices.  For more information, see [Pre-declare corporate-owned devices with IMEI or iOS serial number](../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_IMEI) in [Capabilities in Technical Preview 1605 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Windows Information Protection (WIP)**

  You can create configuration items that let you deploy your Windows Information Protection (WIP) policies, including letting you choose your protected apps, your WIP-protection level, and how to find enterprise data on the network. For more information about WIP, see the following topics:  

  -   [Protect your enterprise data using Windows Information Protection (WIP)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip)  

  -   [Create and deploy a Windows Information Protection (WIP) policy using System Center Configuration Manager](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-sccm)  

### New in Configuration Manager (current branch)  
 No new hybrid features have been introduced in May 2016 for Configuration Manager (current branch).  

##  April 2016  

### New in Microsoft Intune  
 The following Intune features introduced in April 2016 work in hybrid deployments.  

- **MAM user compliance**

  You can now view the status of your application management policies for any user in your Azure Active Directory (AAD) tenant.  For more information see [Monitor mobile app management policies with Microsoft Intune](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) in the Intune library.  

- **MAM controls to prevent Outlook contacts sync (Android)**

  A new setting is available that allows you to prevent an application from syncing contacts to the native address book on Android devices. This new setting is supported initially by the Outlook application on Android devices. For more information, see [Create and deploy mobile app management policies with Microsoft Intune](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) in the Intune library.  

- **Improvements to the Company Portal website**

  When Windows 10 Mobile and Windows Phone 8.1 users are installing line-of-business apps, they will now see the following new statuses, which provide them with more detail about the status of their installation:  

  -   **Waiting for device to sync** – the user has tapped “Install” and the device now tries to sync with the Intune infrastructure. The sync is required before the installation can complete. The "Waiting for device to sync" message is also a link that users can tap to see instructions on how to manually sync their device with Intune if the sync process is taking a long time or gets stalled.  

  -   **Downloading** – the user’s download request is being processed and the device is downloading and installing the app.  

- **Improvements to the Android Company portal app**

  Users who have not enrolled their device in Intune and who do not have the correct certificate installed will not be able to sign in to the Android Company Portal app and will see the message, “You cannot sign in because your device is missing a required certificate.” The message includes a “How to resolve this” link that users can tap to see instructions for installing the certificate. To see the steps that end users follow to resolve the issue, see [Your device is missing a required certificate](/intune/enduser/using-your-android-device-with-intune) in the Intune library.  

- **Improvements to the iOS Company Portal app**

  Support has been added for the pull-to-refresh action to refresh the content on the home screen, which includes listed apps, listed devices, and IT contact information. The pull-to-refresh action does not check compliance or policy information, which can be done by selecting the tile for your current device and tapping the **Sync** button.  

- **Improvements to Windows 10 Mobile and Windows Phone 8.1 Company Portal app**

  When end users are installing line-of-business apps, they will now see an improved app installation experience. If the app installation is taking a long time, users can manually sync their device to force the sync process to resume. To review the end-user instructions, see [Sync your device manually to speed up app installations](/intune/enduser/using-your-windows-device-with-intune) in the Intune library.  

###  New in 1604 Technical Preview
 The following new features introduced in April 2016 are available in hybrid deployments with Intune and Configuration Manager Technical Preview 1604. These features require you to use the Configuration Manager console to configure and manage them.  

- **Find, manage, and distribute Windows Store for Business apps for Windows 10 devices from the Configuration Manager console**


  Support for Windows Store for Business is available in Configuration Manager Technical Preview 1604 to help you find, manage, and distribute apps to the Windows 10 devices you’re managing. For details, see [Manage volume-purchased apps from the Windows Store for Business](/sccm/core/get-started/capabilities-in-technical-preview-1604#manage-volume-purchased-apps-from-the-windows-store-for-business) in [Capabilities in Technical Preview 1604 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1604).  

- **SmartLock setting for Android devices**

  A new setting has been added to the Android and Samsung KNOX Standard configuration item that lets you control the SmartLock feature on compatible Android devices.  You can use this setting to prevent end users from configuring SmartLock. See [SmartLock setting for Android devices](/sccm/get-started/capabilities-in-technical-preview-1604#smartlock-setting-for-android-devices) in [Capabilities in Technical Preview 1604 for System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1604.md).  

### New in Configuration Manager (current branch)  
 No new hybrid features were introduced in April 2016 for Configuration Manager (current branch).  

##  March 2016  

### New in Microsoft Intune  
 The following Intune features introduced in March 2016 work in hybrid deployments.  

- **MAM controls to prevent Outlook contacts sync (iOS)**

  A new setting is available that allows you to prevent an application from syncing contacts to the native address book on iOS devices. This new setting is supported by the Outlook application on iOS devices. For more details about this and other settings, see [Create and deploy MAM policies](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) in the Intune library.  

- **Skype for Business Online supports conditional access**

  You can set a conditional access policy for Skype for Business Online so that it can only be accessed by managed and compliant iOS and Android devices.  For details, see [Manage access to Skype for Business Online](/intune/deploy-use/restrict-access-to-skype-for-business-online-with-microsoft-intune) in the Intune library.  

- **Support for iOS 9.3**

  On Monday March 21st, Apple announced the availability of iOS 9.3. All existing Intune features currently available for managing iOS devices will continue to work seamlessly as users upgrade their devices to iOS 9.3.  

- **Windows app packages available directly from the Company Portal website**

  Users of Windows 8, Windows 8.1, and Windows RT PCs can now install Windows app packages (with the .appx extension) directly from the Company Portal website. Previously, you had to deploy, or users had to install the Company Portal app on their devices to install apps.  

- **Users can remotely lock their device from the Company Portal website**

  A new Remote Lock option has been added to the Company Portal website to enable users to remotely lock their device from the Portal if their device is lost or stolen.  

- **Take advantage of iOS "Open-in" management for devices that are enrolled in a third-party MDM solution**

  You can use your third-party mobile device management (MDM) vendor to take advantage of iOS "Open-In" management. You can set the restrictions in the configuration profile settings and deploy the app using your MDM software. When the user installs the managed app, the restrictions are applied. Read the details: [Microsoft Intune mobile app management policies and iOS Open In](/intune/deploy-use/introduction-to-device-compliance-policies-in-microsoft-intune) in the Intune library.  

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

  In version 1602 of Configuration Manager (current branch) you can use app configuration policies to supply settings that might be required when the user runs an iOS app. For details, see [Configure iOS apps with app configuration policies in System Center Configuration Manager](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies).  

- **Manage volume-purchased iOS apps**

  In version 1602 of Configuration Manager (current branch), you can deploy and manage apps you purchased in volume from the Apple Volume-Purchase Program (VPP) by importing the license information from the app store and tracking how many of the licenses you have used. For details, see [Manage volume-purchased iOS apps with System Center Configuration Manager](/sccm/apps/deploy-use/manage-volume-purchased-ios-apps).  

- **Automatic creation of Office mobile apps**

  Beginning in version 1602 of Configuration Manager (current branch), the following Microsoft Office mobile apps for Android and iOS are created when you upgrade from version 1511:  

  -   Microsoft Word  
  -   Microsoft Excel  
  -   Microsoft PowerPoint  
  -   Microsoft OneDrive  
  -   Microsoft OneNote (iOS only)  
  -   Microsoft Outlook  

  You will find these apps in the Applications node of the Configuration Manager console. For more information about deploying applications, see [How to deploy applications with System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md).  

- **Kiosk mode settings for Android Samsung KNOX Standard devices**

  Kiosk mode allows you to lock a device to only allow certain features to work.  Beginning in version 1602 of  Configuration Manager (current branch), you can now specify kiosk mode settings for Samsung KNOX Standard devices. For details, see [How to create configuration items for Android and Samsung KNOX Standard devices managed without the System Center Configuration Manager client](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client).  

- **iOS Activation Lock**

  Beginning in version 1602 of Configuration Manager (current branch), you can manage iOS Activation Lock, a feature of the Find My iPhone app for iOS 7.1 and later devices. Activation Lock is enabled automatically when the Find My iPhone app is used on a device.  For details, see [Manage iOS Activation Lock bypass for System Center Configuration Manager](/sccm/mdm/deploy-use/manage-ios-activation-lock#bypass-activation-lock).  



## Notices

### System Center 2012 Configuration SP1 and System Center 2012 R2 Configuration Manager (RTM): Support for hybrid mobile device management ending on April 10, 2017
*January 11, 2017*

Support for System Center 2012 Configuration Manager SP1 and System Center 2012 R2 Configuration Manager RTM ended on July 12, 2016. Subsequently, support for these releases connecting to the Microsoft Intune service for hybrid MDM ends on April 10, 2017. After this date, hybrid MDM will stop functioning with these releases. Managed devices will essentially become unmanaged as the Intune Connector will no longer connect to the Intune service. Configuration Manager data (such as policies and applications) will not flow up to Intune and managed device data will not flow down to Configuration Manager until an upgrade takes place.

If you're running a hybrid deployment with Configuration Manager 2012 SP1 or R2 RTM, we recommend that before April 10, 2017 you upgrade to Configuration Manager (current branch) or the latest supported service pack for Configuration Manager 2012 (either R2 SP1 or SP2) to avoid disruption of service.

Additional resources:
-	[Upgrade to System Center Configuration Manager (current branch)](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
-	[Planning to upgrade to System Center 2012 R2 Configuration Manager SP1](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningR2SP1Upgrade)
-	[Planning to upgrade to System Center 2012 Configuration Manager SP2](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningSP2Upgrade)

### Windows Phone 8 Company Portal upload deprecated
*October 25, 2016*

The ability to upload a signed Company Portal app has been removed from the Configuration Manager console, as Intune support is being deprecated for Windows 8, Windows Phone 8, and Windows RT, and support for the Windows Phone 8 Company Portal is ending in November.  Windows 8, Windows Phone 8, and Windows RT devices that are already enrolled will continue to be supported, but enrolling additional devices with these platforms will not be supported.
