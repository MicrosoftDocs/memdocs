---
title: "What's new in hybrid MDM"
titleSuffix: "Configuration Manager"
description: "Learn about the new mobile device management features available for hybrid deployments with Configuration Manager and Intune."
ms.custom: na
ms.date: 02/21/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# What's new in hybrid mobile device management with System Center Configuration Manager and Microsoft Intune

*Applies to: System Center Configuration Manager (Current Branch)*

This article provides details on the new mobile device management (MDM) features available for hybrid deployments with System Center Configuration Manager and Microsoft Intune.     

> [!Note]    
> Intune on Azure is Microsoft’s recommended MDM solution.     
> - For details about new features and updates in Intune standalone, see [What's new in Intune](https://docs.microsoft.com/intune/whats-new).    
> - For details about how to migrate to Intune standalone, see [Migrate hybrid MDM users and devices to Intune standalone](https://docs.microsoft.com/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).
> - For details about UI updates for Intune and hybrid MDM, see [UI updates for Intune end user apps](https://docs.microsoft.com/intune/whats-new-app-ui). 

##  Compatibility with Configuration Manager versions  
Each section of this article lists hybrid features under three different categories. Use the following guidance to determine compatibility of the features in each category with different versions of Configuration Manager:  

|Feature categories|Description|
|-|-|
|**New in Microsoft Intune** | In general, all the features listed under this category should work with all Configuration Manager releases. This including System Center 2012 R2 Configuration Manager releases, since these features only require the Intune service and do not require additional functionality in Configuration Manager.|
|**New in Configuration Manager Technical Preview**| All the features listed under this category only work with the specified Technical Preview release. To try out these features, you must install the Technical Preview version specified in the feature description. For more information, see [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md).|
|**New in Configuration Manager (current branch)**| All the features listed under this category only work with the specified version of Configuration Manager (current branch), such as version 1511 or 1602. If you're using an older version of Configuration Manager for your hybrid deployment, you must upgrade to the Configuration Manager (current branch)  version specified in the feature description. For more information, see [Upgrade to System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md).|



## January 2018

### New in Microsoft Intune

- **Approve the Company Portal app for Android for Work**  
  If your organization uses Android for Work, manually approve the Company Portal app for Android. It then continues to receive automatic updates from the managed Google Play store.
  <!--1797090 -->  

- **Conditional Access policies for Intune are only available from the Azure portal**   
  Starting with this release, you must configure and manage your Conditional Access policies in the [Azure portal](https://portal.azure.com) from **Azure Active Directory** > **Conditional Access**. For your convenience, you can also access this blade from Intune in the Azure portal at **Intune** > **Conditional Access**.
  <!-- 1737088 1634311 --> 

- **Updates to compliance emails**    
  When an email is sent to report a noncompliant device, details about the noncompliant device are included. 
  <!--1637547 -->

- **New functionality for the "Resolve" action for Android devices**    
  The Company Portal app for Android is expanding the "Resolve" action for **Update device settings** to resolve [device encryption issues](https://docs.microsoft.com/intune-user-help/encrypt-your-device-android).
  <!--1583480-->

- **Remote lock available in Company Portal app for Windows 10**    
  End users can now remotely lock their devices from the Company Portal app for Windows 10. This action is not displayed for the local device they're actively using.
  <!--676506-->

- **Easier resolution of compliance issues for the Company Portal app for Windows 10**   
  End users with Windows devices can tap the non-compliance reason in the Company Portal app. When possible, this action takes them directly to the correct location in the settings app to fix the issue.
  <!--676546-->    



## December 2017

### New in Microsoft Intune

- **Available application deployments now supported for Android Enterprise**    
  You can now deploy Android Enterprise (formerly Android for Work) apps as **Available**, in addition to **Required**. For details, see [Create Android applications with System Center Configuration Manager](/sccm/mdm/deploy-use/creating-android-applications).



## November 2017

### New in Microsoft Intune

- **Text protocol allowed from managed Apps**  
  Apps managed by the Intune App SDK are able to send SMS messages.
  <!-- 1414050  -->   

- **Company Portal app for macOS is available**   
  The Intune Company Portal on macOS has an updated experience. It is optimized to cleanly display all the information and compliance notifications your users need for all the devices they have enrolled. And, once the Intune Company Portal has been deployed to a device, Microsoft AutoUpdate for macOS provides updates to it. Download the new Intune Company Portal for macOS by logging into the Intune Company Portal website from a macOS device.
  <!--1541700-->   

- **Microsoft Planner is now part of the mobile app management (MAM) list of approved apps**    
  The Microsoft Planner app for iOS and Android is now part of the approved apps for mobile app management (MAM). Configure the app through the Intune App Protection blade in the Azure portal to all tenants. For details, see [MAM list of approved apps](https://www.microsoft.com/cloud-platform/microsoft-intune-apps).
  <!-- 1248473 -->    

- **Access to managed app logs for iOS**    
  End users with the managed Browser installed can now view the management status of all Microsoft published apps and send logs for troubleshooting their managed iOS apps.
  <!-- 1469920 -->    

  Learn how to enable the troubleshooting mode in the Managed Browser on an iOS device, see [How to access to managed app logs using the Managed Browser on iOS](https://docs.microsoft.com/intune/app-configuration-managed-browser#how-to-access-to-managed-app-logs-using-the-managed-browser-on-ios).

- **Improvements to device setup workflow in the Company Portal for iOS in version 2.9.0**    
  We've improved the device setup workflow in the Company Portal app for iOS. The language is more user-friendly and we've combined screens where possible. We have also made the language more specific to your company by using your company name throughout the setup text. You can see this updated workflow on the [what's new in app UI](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-november-13-2017) page.

- **Feedback prompts for the Company Portal app for Android**    
  The Company Portal app for Android now requests end-user feedback. This feedback is sent directly to Microsoft, and provides end users with an opportunity to review the app in the public Google Play store. Feedback is not required, and can easily be dismissed so users can continue using the app. 
  <!--1165249-->    

- **Inform end users what device information can be seen for Windows 10 devices**    
  We have added **Ownership Type** to the Device Details screen on the Company Portal app for Windows 10. This information allows users to find out more about privacy directly from the Intune end-user docs. They can also locate this information on the **About** screen.
  <!--1337920-->    

- **New 'Resolve' action available for Android devices**    
  The Company Portal app for Android is introducing a 'Resolve' action on the _Update device settings_ page. Selecting this option takes the end user directly to the setting that is causing their device to be noncompliant. The Company Portal app for Android currently supports this action for the [device passcode](https://docs.microsoft.com/intune-user-help/set-your-pin-or-password-android), [device encryption](https://docs.microsoft.com/intune-user-help/encrypt-your-device-android), [USB debugging](https://docs.microsoft.com/intune-user-help/you-need-to-turn-off-usb-debugging-android), and [Unknown Sources](https://docs.microsoft.com/intune-user-help/you-need-to-turn-off-unknown-sources-android) settings. 
  <!--1583480-->    


### New in Configuration Manager (current branch)

- **Actions for non-compliance**    
  You can now configure a time-ordered sequence of actions that are applied to devices that fall out of compliance. For example, you can notify users of non-compliant devices via e-mail or mark those devices non-compliant. For details, see [Set up actions for non-compliance](/sccm/mdm/deploy-use/actions-for-noncompliance).
  <!--1321366 -->

- **New mobile application management policy settings**     
  The following settings have been added to the mobile application management policy settings:
  - **Disable contact sync**: Prevents the app from saving data to the native Contacts app on the device.
  - **Disable printing**: Prevents the app from printing work or school data.
  <!-- 1324760 -->    

  See [protect apps using app protection policies in Configuration Manager](/sccm/mdm/deploy-use/protect-apps-using-mam-policies) to try the new app protection policy settings.

- **Windows 10 ARM64 device support**     
  Hybrid mobile device management (MDM) scenarios are supported on ARM64 devices running Windows 10 when these devices are available. For details, see [Windows 10 ARM64 device support](/sccm/core/plan-design/changes/whats-new-in-version-1710#windows-10-arm64-device-support).
  <!-- 1355000 -->    

- **Improved VPN profile experience in the Configuration Manager console**     
  With this release, we’ve updated the VPN profile wizard and properties pages to display settings appropriate for the selected platform. This feature was previously available in Configuration Manager Technical Preview 1709. It is now available in hybrid deployments with Intune and Configuration Manager (Current Branch) version 1710. For more information, see [Improved VPN profile experience in Configuration Manager console](/sccm/core/plan-design/changes/whats-new-in-version-1710#improved-vpn-profile-experience-in-configuration-manager-console).
  <!-- 1318232 -->


### New in Configuration Manger Technical Preview 1711

- **New compliance policy options for Windows 10**   
  You can now configure new options for compliance policies for Windows 10 devices. The new settings include policies for Firewall, User Account Control, Windows Defender Antivirus, and OS build versioning. For details, see [New compliance policy options for Windows 10](/sccm/core/get-started/capabilities-in-technical-preview-1711#new-compliance-policy-options-for-windows-10).



## October 2017

### New in Configuration Manager Technical Preview 1709

- **Improved VPN Profile experience in Configuration Manager console**      
  VPN profile settings are now filtered according to platform. When you create new VPN profiles, each supported platform contains only the settings appropriate for the platform. Existing VPN profiles are not affected. You can read more about this change [here](/sccm/core/get-started/capabilities-in-technical-preview-1709#improved-vpn-profile-experience-in-configuration-manager-console).
  <!-- 1313282 -->


### New in Microsoft Intune  

- **Help your users help themselves with the Company Portal app for Android**     
  The Company Portal app for Android has added instruction for end users to help them understand, and possibly self-solve on new use cases.
    - If end users have reached the maximum number of devices that they are allowed to add, they are guided to the [Azure Active Directory portal](https://account.activedirectory.windowsazure.com/r/#/profile) to remove a device.
    - End users are given steps to follow to help them [fix activation errors on Samsung Knox devices](https://go.microsoft.com/fwlink/?linkid=859718) or to [turn off power-saving mode](https://docs.microsoft.com/intune-user-help/power-saving-mode-android). If neither of those solutions resolve their issue, we provide an explanation of how to [submit logs to Microsoft](https://docs.microsoft.com/intune-user-help/send-logs-to-microsoft-android).
  <!-- 1573324, 1573150, 1558616, 1564878 -->      

- **Device setup progress indicator in Android Company Portal**    
  The Company Portal app for Android shows a device setup progress indicator when a user is enrolling their device. The indicator shows new statuses, beginning with "Setting up your device...", then "Registering your device...", then "Finishing registering your device...", then "Finishing setting up your device...".  
  <!--1565657-->    

- **Certificate-based authentication support on the Company Portal for iOS**    
  We have added support for certificate-based authentication (CBA) in the Company Portal app for iOS. Users with CBA enter their username, then tap the “Sign in with a certificate” link. CBA is already supported on the Company Portal apps for Android and Windows. You can learn more on the [sign in to the Company Portal app](https://docs.microsoft.com/intune-user-help/sign-in-to-the-company-portal) page.
  <!--1029830-->   

- **Improvements to device setup workflow in Company Portal**     
  We've improved the device setup workflow in the Company Portal app for Android. The language is more user-friendly and specific to your company, and we've combined screens where possible. You can see these improvements on the [what's new in app UI](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-october-2-2017) page.
  <!--1490692-->     

- **Improved guidance around the request for access to contacts on Android devices**     
  The Company Portal app for Android often requires the end user to accept the Contacts permission. If an end user declines this access, they see an in-app notification that alerts them to grant it for conditional access. 
  <!--1484985-->     

- **Secure startup remediation for Android**     
  End users with Android devices can tap the non-compliance reason in the Company Portal app. When possible, this action takes them directly to the correct location in the settings app to fix the issue. 
  <!--1490712-->    

- **Additional push notifications for end users on the Company Portal app for Android Oreo**    
  End users see additional notifications to indicate to them when the Company Portal app for Android Oreo is performing background tasks, such as retrieving policies from the Intune service. The notifications increase transparency for end users about when the Company Portal is performing administrative tasks on their device. This improvement is part of the overall [optimization of the Company Portal UI](https://blogs.technet.microsoft.com/intunesupport/2017/08/21/android-8-0-o-behaviour-changes-and-microsoft-intune) for the Company Portal app for Android Oreo. 
  <!--1475932 -->     

- **New behaviors for the Company Portal app for Android with work profiles**     
  When you enroll an Android for Work device with a work profile, it's the Company Portal app in the work profile that performs management tasks on the device. 

  Unless you're using a MAM-enabled app in the personal profile, the Company Portal app for Android no longer serves any use. To improve the work profile experience, Intune automatically hides the personal Company Portal app after a successful work profile enrollment.

  The Company Portal app for Android can be enabled at any time in the personal profile by browsing for [Company Portal in the Play Store](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal) and tapping **Enable**.
  <!--1485783-->    

- **Company Portal for Windows 8.1 and Windows Phone 8.1 moving to sustaining mode**    
  A notice was added to announce that Company Portal apps for Windows 8.1 and Windows Phone 8.1 are moving to sustaining mode. For details, see [Notices](#notices).  
  <!--1428681-->    

- **Block unsupported Samsung Knox device enrollment**   
  The Company Portal app only attempts to enroll supported Samsung Knox devices. To avoid KNOX activation errors that prevent MDM enrollment, device enrollment is only attempted if the device appears in the [list of devices published by Samsung](https://www.samsungknox.com/knox-supported-devices/knox-workspace). Samsung devices can have model numbers that support KNOX while others that don't. Verify Knox compatibility with your device reseller before purchase and deployment. You can find the full list of verified devices in the [Android and Samsung KNOX Standard policy settings](https://docs.microsoft.com/intune-classic/deploy-use/android-policy-settings-in-microsoft-intune#supported-samsung-knox-standard-devices).
  <!-- 1490695 -->     

- **End of support for Android 4.3 and lower**     
  A notice was added for end of support for Android 4.3 and lower. For details, see [Notices](#notices).
  <!--1171126, 1326920 -->     

- **Inform end users what device information can be seen on enrolled devices**     
  We are adding **Ownership Type** to the Device Details screen on all Company Portal apps. This information allows users to find out more about privacy directly from the [What information can your company see?](https://docs.microsoft.com/intune-user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune) article. This improvement rolls out across all Company Portal apps in the near future. We announced this feature for iOS in [September](https://docs.microsoft.com/intune/whats-new#week-of-september-11-2017). 
  <!--1165314-->     



## September 2017

### New in Microsoft Intune     

- **Refresh action added to the Company Portal app for Windows 10**    
    The Company Portal app for Windows 10 allows users to refresh the data in the app by either pulling to refresh or, on desktops, pressing F5.
    <!-- 1132468 -->     

- **Inform end users what device information can be seen for iOS**   
    We added  **Ownership Type** to the Device Details screen on the Company Portal app for iOS. This information allows users to find out more about privacy directly from the Intune end-user docs. They can also locate this information on the About screen. 
    <!--739894-->    

- **Easier-to-understand phrasing for the Company Portal app for Android**   
    The enrollment process for the Company Portal app for Android has been simplified with new text to make it easier for end users to enroll. If you have custom enrollment documentation, update it to reflect the new screens. You can find sample images on our [UI updates for Intune end user apps](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-september-11-2017) page.
    <!---1396349-->    

- **Windows 10 Company Portal app added to Windows Information Protection allow policy**    
    The Windows 10 Company Portal app has been updated to support Windows Information Protection (WIP). The app can be added to the WIP allow policy. With this change, the app no longer has to be added to the **Exempt** list. 

    Only a single WIP configuration item can be delivered to a device. If two WIP configuration items are targeted to the same device, neither WIP policy applies.
    <!-- 677129 -->    

- **End of support notice added for iOS 8.0**    
    A notice was added for end of support for iOS 8.0. For details, see [Notices](#notices).



## August 2017

### New in Microsoft Intune     

- **New signed-in experience for Android Company Portal users and App Protection Policy users**    
  End users can now browse apps, manage devices, and view IT contact information using the Android Company Portal app without enrolling their Android devices. In addition, if an end user already uses an app protected by Intune App Protection Policies, and launches the Android Company Portal, the end user no longer receives a prompt to enroll the device.
  <!-- 621669 -->



## July 2017

### New in Microsoft Intune

- **End of support notices added for Android and Windows Phone**    
    New notices were added for end of support for Android and Windows Phone versions. For details, see [Notices](#notices).


### New in Configuration Manager (current branch)

The following features were previously available in Configuration Manager Technical Preview releases. These features are now available in hybrid deployments with Intune and Configuration Manager (current branch) version 1706.

- [Entrust support for Entrust certification authorities](/sccm/core/get-started/capabilities-in-technical-preview-1706#support-for-entrust-certification-authorities)
- [New mobile application management policy settings](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-mobile-application-management-policy-settings)
- [Updates to Android for Work sharing configuration](/sccm/core/plan-design/changes/whats-new-in-version-1706#updates-to-android-for-work-sharing-configuration)
- [New device compliance policy rules](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-device-compliance-policy-rules)
- [New configuration settings for Windows 10 devices that are not managed with the Configuration Manager client](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-configuration-settings-for-windows-10-devices-that-are-not-managed-with-the-configuration-manager-client)
- [Cisco (IPsec) support for macOS VPN profiles](/sccm/core/get-started/capabilities-in-technical-preview-1706#cisco-ipsec-support-for-macos-vpn-profiles)
- [Android and iOS enrollment restrictions](/sccm/core/plan-design/changes/whats-new-in-version-1706#android-and-ios-enrollment-restrictions) 



## June 2017

### New in Microsoft Intune

- **Change your MDM authority**    
  Beginning in Configuration Manager version 1610, you can change your MDM authority without having to contact Microsoft Support. You also do not have to unenroll and reenroll your existing managed devices. For details, see [Change your MDM authority](/sccm/mdm/deploy-use/change-mdm-authority).

- **Managed browser and app proxy integration**    
  The Intune Managed Browser can now integrate with the Azure AD Application Proxy service to let users access internal web sites even when they are working remotely. Users of the browser enter the site URL as they normally would and the Managed Browser routes the request through the application proxy web gateway. For more information, see [Manage Internet access using Managed browser policies](https://docs.microsoft.com/intune/app-configuration-managed-browser).

- **Company Portal app for Android now has a new end-user experience for App Protection Policies**  
  Based on customer feedback, we've modified the Company Portal app for Android to show an **Access Company Content** button. The intent is to prevent end users from unnecessarily going through the enrollment process when they only need to access apps that support App Protection Policies, a feature of Intune mobile application management. You can see these changes on the [what's new in app UI](https://docs.microsoft.com/intune/whats-new-app-ui) page.

- **New menu action to easily remove Company Portal**  
  Based on user feedback, the Company Portal app for Android has added a new menu action to initiate the removal of Company Portal from your device. This action removes the device from Intune management so that the app can be removed from the device by the user. You can see these changes on the [what's new in app UI](https://docs.microsoft.com/intune/whats-new-app-ui) page and in the [Android end-user documentation](https://docs.microsoft.com/intune-user-help/unenroll-your-device-from-intune-android).

- **Improvements to app syncing with Windows 10 Creators Update**  
  The Company Portal app for Windows 10 now automatically initiates a sync for app install requests for devices with Windows 10 Creators Update (version 1703). This behavior reduces the issue of app installs stalling during the "Pending Sync" state. In addition, users are able to manually initiate a sync from within the app. You can see these changes on the [what's new in app UI](https://docs.microsoft.com/intune/whats-new-app-ui) page.

- **New guided experience for Windows 10 Company Portal**  
  The Company Portal app for Windows 10 includes a guided Intune walkthrough experience for devices that haven't been identified or enrolled. The new experience provides step-by-step instructions that guides the user through registering into Azure Active Directory (required for Conditional Access features) and MDM enrollment (required for device management features). The guided experience is accessible from the Company Portal home page. If users don't complete registration and enrollment, they can continue to use the app, but experience limited functionality.

  This update is only visible on devices running Windows 10 Anniversary Update (build 1607) or higher. You can see these changes on the [what's new in app UI](https://docs.microsoft.com/intune/whats-new-app-ui) page.

- **Improvements to the app tiles in the Company Portal app for iOS**  
  We updated the design of the app tiles on the homepage to reflect the branding color you set for the Company Portal. For more information, see [what's new in app UI](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Account picker now available for the Company Portal app for iOS**  
  If users of iOS devices use their work or school account to sign into other Microsoft apps, they might see our new account picker when they sign into the Company Portal. For more information, see [what's new in app UI](https://docs.microsoft.com/intune/whats-new-app-ui).

### New in Configuration Manager Technical Preview 1706

- **New Windows configuration item settings**      
  New Windows configuration items are available for the Password, Device, Store, and Microsoft Edge setting categories. For more information, see [New Windows configuration item settings](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-windows-configuration-item-settings).
  <!-- 1354715 -->

- **New device compliance policy rules**   
  You can now configure new options for compliance policies that were previously only available in Intune standalone. For details, see [Device compliance policy improvements](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-device-compliance-policy-rules).

- **Android and iOS enrollment restrictions**       
  Admins can now specify that users cannot enroll personal Android or iOS devices in their hybrid environment. This action allows you to limit enrolled devices to predeclared, company-owned devices, or iOS devices enrolled with Device Enrollment Program only. For details, see [Android and iOS enrollment restrictions](/sccm/core/get-started/capabilities-in-technical-preview-1706#android-and-ios-enrollment-restrictions).
  <!-- 1290826 -->

- **Support for Entrust certification authorities**      
  Configuration Manager now supports Entrust certification authorities. This support enables PFX certificate delivery to devices enrolled into Microsoft Intune.    
  <!-- 1350740 -->

  You can configure Entrust as the certification authority when adding a Certificate Registration Point role in Configuration Manager. When adding a new certificate profile that issues PFX certificates, you can select either a Microsoft or Entrust certification authority.

  **Known issue**: In the 1706 technical preview, PFX certificates aren't issued for Microsoft certification authorities. This issue doesn't affect imported PFX certificates or SCEP profiles.

- **Cisco (IPsec) support for macOS VPN profiles**      
  You can create a macOS VPN profile with Cisco (IPsec) as the connection type. For more information, see [Create VPN profiles](/sccm/mdm/deploy-use/create-vpn-profiles#create-vpn-profiles).
  <!-- 1321367 -->


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



## Notices

### Company Portal for Windows 8.1 and Windows Phone 8.1 moving to sustaining mode 
<!--1428681-->
*October 6, 2017*   
 
Beginning in October 2017, the Company Portal apps for Windows 8.1 and Windows Phone 8.1 move to sustaining mode. This mode means that the apps and existing scenarios, such as enrollment and compliance, continue to be supported for these platforms. These apps continue to be available for download through existing release channels, such as the Microsoft Store. 

Once in sustaining mode, these apps only receive critical security updates. No additional updates or features will be released for these apps. For new features, we recommend that you update devices to Windows 10 or Windows 10 Mobile. 

### End of support for iOS 8.0 
<!---1164477--->
Managed apps and the Company Portal app for iOS require iOS 9.0 and higher to access company resources. Devices that aren't updated before September are no longer able to access the Company Portal or those apps. 

### Platform Support Reminder: Windows Phone 8.1 mainstream support ended July 11, 2017
<!-- 1327781 -->
*July 11, 2017*

The Windows Phone 8.1 platform has reached end of mainstream support. Windows 8.1 PC support isn't impacted.

There is no immediate impact to any Windows Phone 8.1 device that is managed by the Intune service, including those devices enrolled in hybrid MDM. Devices that are enrolled continue to work. All policies, configurations, and apps continue to work as expected. Note, there are no improvements targeted for the Windows Phone 8.1 platform within the Intune service, and for the Windows Phone 8.1 Company Portal app.

We recommend upgrading eligible Windows Phone 8.1 devices to Windows 10 Mobile at your earliest opportunity.  

### End of support for Android 4.3 and lower
<!---1171127--->
*July 6, 2017*

Managed apps and the Company Portal app for Android require Android 4.4 and higher to access company resources. Devices that aren't updated before the beginning of October are no longer able to access the Company Portal or those apps. By December, all enrolled devices are force retired in December, resulting in loss of access to company resources. If you are using app protection policies without MDM, apps won't receive updates, and the quality of their experience diminishes over time.



## See Also

- [Past hybrid MDM features and notices](whats-new-hybrid-archive.md)
- [What's new for MDM in System Center 2012 Configuration Manager](https://technet.microsoft.com/library/mt445560.aspx)
