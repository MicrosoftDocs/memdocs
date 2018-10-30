---
title: What's new in hybrid MDM
titleSuffix: Configuration Manager
description: Learn about the new mobile device management features available for hybrid deployments with Configuration Manager and Intune.
ms.date: 10/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# What's new in hybrid mobile device management with Configuration Manager and Microsoft Intune

*Applies to: System Center Configuration Manager (Current Branch)*

This article provides details on the new mobile device management (MDM) features available for hybrid deployments with System Center Configuration Manager and Microsoft Intune.     

> [!Important]  
> As of August 14, 2018, hybrid mobile device management is a [deprecated feature](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). For more information, see [What is hybrid MDM](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  


> [!Note]    
> Intune on Azure is Microsoft's recommended MDM solution.     
> - For details about new features and updates in Intune standalone, see [What's new in Intune](https://docs.microsoft.com/intune/whats-new).    
> - For details about how to migrate to Intune standalone, see [Migrate hybrid MDM users and devices to Intune standalone](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).
> - For details about UI updates for Intune and hybrid MDM, see [UI updates for Intune end user apps](https://docs.microsoft.com/intune/whats-new-app-ui). 



##  Compatibility with Configuration Manager versions  

Each section of this article lists hybrid features under three different categories. Use the following guidance to determine compatibility of the features in each category with different versions of Configuration Manager:  

|Feature categories|Description|
|-|-|
|**New in Microsoft Intune** | In general, all the features listed under this category should work with all Configuration Manager releases. This including System Center 2012 R2 Configuration Manager releases, since these features only require the Intune service and don't require additional functionality in Configuration Manager.|
|**New in Configuration Manager Technical Preview**| All the features listed under this category only work with the specified technical preview branch. To try out these features, you must install the technical preview version specified in the feature description. For more information, see [Technical preview for Configuration Manager](/sccm/core/get-started/technical-preview).|
|**New in Configuration Manager (current branch)**| All the features listed under this category only work with the specified version of Configuration Manager (current branch). If you're using an older version of Configuration Manager for your hybrid deployment, upgrade to the Configuration Manager (current branch)  version specified in the feature description. For more information, see [Upgrade to Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).|



## October 2018

### New in Microsoft Intune

#### Updates for Application Transport Security 
<!--748318-->
Microsoft Intune supports Transport Layer Security (TLS) 1.2+ to provide best-in-class encryption, to ensure Intune is more secure by default, and to align with other Microsoft services such as Microsoft Office 365. In order to meet this requirement, the iOS and macOS company portals will enforce Apple's updated Application Transport Security (ATS) requirements which also require TLS 1.2+. ATS is used to enforce stricter security on all app communications over HTTPS. This change impacts Intune customers using the iOS and macOS Company Portal apps. For more information, see [Intune moving to TLS 1.2 for encryption](https://blogs.technet.microsoft.com/intunesupport/2018/06/05/intune-moving-to-tls-1-2-for-encryption/).

#### Remove an email profile from a device, even when there's only one email profile 
<!--1818139-->
Previously, you couldn't remove an email profile from a device if it's the only email profile. With this update, this behavior changes. Now, you can remove an email profile, even if it's the only email profile on the device. 

#### Remove PKCS and SCEP certificates from your devices 
<!--3218390-->
In some scenarios, PKCS and SCEP certificates remained on devices, even when removing a policy from a group, deleting a configuration or compliance deployment, or an admin updating an existing SCEP or PKCS profile. 

This update changes the behavior. There are some scenarios where PKCS and SCEP certificates are removed from devices, and some scenarios where these certificates remain on the device. 

#### Access to key profile properties using the company portal app
<!--772203-->  
End users can now access key account properties and actions, such as password reset, from the Company Portal app. 

#### PIN prompt when you change fingerprints or face ID on an iOS device  
<!--2637704-->  
Users are now prompted for a PIN after making biometric changes on their iOS device. This includes changes to registered fingerprints or face ID. The timing of the prompt depends on how the configuration of the *Recheck access requirements after (minutes)* timeout.  When no PIN is set, the user is prompted to set one.  

This feature is only available for iOS, and requires the participation of applications that integrate the Intune APP SDK for iOS, version 8.1.1 or later. Integration of the SDK is necessary so that the behavior can be enforced on the targeted applications. This integration happens on a rolling basis and is dependent on the specific application teams. Some apps that participate include WXP, Outlook, Managed Browser, and Yammer.

#### End user device and app content menu 
<!--2771453-->  
End users can now use context menu on device and apps to trigger common actions like renaming a device or checking compliance. 

#### Windows Company Portal keyboard shortcuts
<!--2771518-->  
End users can now trigger app and device actions in the Windows Company Portal using keyboard shortcuts (accelerators).



## August 2018

### New in Microsoft Intune

#### New user experience update for the Company Portal website
<!--2000968-->
Based on your feedback, we've added new features to the Company Portal website. You'll experience a significant improvement in existing functionality and usability from your Android, iOS, and Windows devices. Areas of the site have received a new, modern, responsive design. These areas include device details, feedback and support, and device overview. You'll also see the following improvements:

- Streamlined workflows across all device platforms
- Improved device identification and enrollment flows
- More helpful error messages
- Friendlier language, less tech jargon
- Ability to share direct links to apps
- Improved performance for large app catalogs
- Increased accessibility for all users



## July 2018

### New in Microsoft Intune

#### Updated Intune App SDK for Android is now available
<!--2744271-->
An updated version of the Intune App SDK for Android is available to support the Android 9 Pie release. If you're an app developer and use the Intune SDK for Android, install the updated version of the Intune app SDK. This update makes sure that Intune functionality within your Android apps continue to work as expected on Android 9 Pie devices. This version of the Intune App SDK provides a built-in plugin that performs the SDK updates. You don't need to rewrite any existing code that's integrated. For more information, see [Intune SDK for Android](https://github.com/msintuneappsdk/ms-intune-app-sdk-android). 

If you're using the old badging style for Intune, switch to use the briefcase icon. For more information on branding, see the [Intune App Badging System](https://github.com/msintuneappsdk/intune-app-partner-badge).


#### Support for security enhancement in Intune service
<!--2520152-->
You can now specify that devices without any assigned compliance policies aren't compliant in hybrid. Configure this setting in the Intune on Azure portal. We strongly recommend that you enable this feature to secure your internal resources.

This feature is off by default in hybrid tenants. When you enable this feature, devices that don't have an assigned compliance policy are considered non-compliant. If you also enable conditional access, these devices lose access to internal resources. Such resources may be Outlook or SharePoint, based on the conditional access policies in your environment. If you leave this setting off, these devices continue to have the same level of access as they do currently.

To help you determine the impact of turning on this feature, we've provided a [script on the TechNet Gallery](https://gallery.technet.microsoft.com/SQL-Query-for-Hybrid-MDM-5bcb8695). When you run this script against your Configuration Manager database, it lists the devices that aren't targeted by any compliance policies.

For more information, see the following articles:
- [Security Enhancements in the Intune Service](https://aka.ms/compliance_policies) blog post 
- [Device compliance policies in Configuration Manager](/sccm/mdm/deploy-use/device-compliance-policies)

#### Updates to out-of-compliance messages in Company Portal app 
<!--1832222--> 
We're revising the messages that device users see when a device is out-of-compliance. Messages retain their original meanings, but are updated with friendlier language and less technical jargon. We're also refreshing links to documentation and remediation steps to keep them up-to-date.  

The following text is one example of the improvements in messaging you'll see:  

- Before: *This device hasn't contacted the Intune service in the specified time period required by your IT admin. To resolve this issue, please open the company portal app on your device and click on the Check Compliance button.*  

- After: *Your device has not checked in with your organization in a while. To reestablish a connection, open the Company Portal app on your device and tap Check Settings for your device.*  

#### Select device categories by using the Access Work or School settings 
<!--1058963--> 
If you've enabled [device group mapping](https://docs.microsoft.com/intune/device-group-mapping), users on Windows 10 are now prompted to select a device category after enrolling through the **Connect** button in **Settings** > **Accounts** > **Access work or school**.  

#### New browsing experiences in the Company portal app for Windows 
<!--2317227-->
Now when browsing or searching for apps in the Company Portal app for Windows, toggle between the existing **Tiles** view and the newly added **Details** view. The new view lists application details such as name, publisher, publication date, and installation status. 

The **Apps** page's **Installed** view lets you see details about completed and in-progress app installations. To see what the new view looks like, see [What's new in the UI](https://docs.microsoft.com/intune/whats-new-app-ui).

#### More opportunities to sync in the Company portal app for Windows  
<!--2683177-->
The Company Portal app for Windows now lets you initiate a sync directly from the Windows taskbar and Start menu. This feature is especially useful if your only task is to sync devices and get access to corporate resources. To access the new feature, right-click the Company Portal icon that's pinned to your taskbar or Start menu. In the menu options, select **Sync this device**. (This menu is also referred to as a jump list.) The Company Portal opens to the **Settings** page and initiates your sync. For the updated procedure, see [Sync your Windows device manually](https://docs.microsoft.com/intune/intune-user-help/sync-your-device-manually-windows#sync-from-device-taskbar-or-start-menu).



## June 2018

### New in Microsoft Intune

#### Access to macOS Company Portal pre-release build 
<!--1734766-->
Using Microsoft AutoUpdate, sign up to receive builds early by joining the Insider program. Signing up enables you to use the updated Company Portal before it's available to your end users.

#### Intune app protection policies and Microsoft Edge 
<!--1818968,1818969-->
The Microsoft Edge browser for mobile devices (iOS and Android) now supports Microsoft Intune app protection policies. Users of iOS and Android devices who sign in with their corporate Azure Active Directory accounts in the Edge application are protected by Intune. On iOS devices, the policy to **Require managed browser for web content** allows users to open links in Edge when it's managed.



## May 2018

### New in Microsoft Intune

#### Requesting help in the Company Portal for Windows 10 
<!--1874137-->
The Company Portal for Windows 10 now sends app logs directly to Microsoft when the user initiates the workflow to get help with an issue. This behavior makes it easier to troubleshoot and resolve issues that are raised to Microsoft.  


### New in Configuration Manager (current branch)

#### Android for Work and Lookout onboarding moved to Intune on Azure
<!--2355022,2357366-->
With the latest Intune update, you can enable and manage Android for Work integration and Lookout mobile threat defense integration on hybrid mobile device management tenants in the Intune on Azure portal. Prior to the update, these settings were only configurable in the Intune Classic (Silverlight) portal.
 
Note: Lookout is the only mobile threat defense (MTD) provider supported in hybrid. If you've previously integrated with any other MTD provider, it still appears in the Intune on Azure portal. If you delete the connector for it, then you can't add it back.
 
These changes don't impact existing functionality. Continue to use the Configuration Manager console for managing related apps, reporting, and policies.
 
For more information, see the following articles:
- [Set up Android hybrid device management](/sccm/mdm/deploy-use/enroll-hybrid-android)
- [Manage access to company resource based on device, network, and application risk](/sccm/mdm/deploy-use/lookout-mobile-threat-defense-in-configuration-manager)


#### Support for new versions of Cisco AnyConnect client for iOS
<!--1357393-->
You can enable support for Cisco AnyConnect for iOS version 4.0.7 or later. If you do this, existing Cisco AnyConnect VPN profiles are labeled **Cisco Legacy AnyConnect**, and continue to work as before. The **Cisco AnyConnect** option is for new VPN profiles that work with Cisco AnyConnect on iOS version 4.0.7 or later.

  > [!Tip]  
  > Cisco AnyConnect 4.0.07x and later for iOS was first introduced in version 1802 as a [pre-release feature](/sccm/core/servers/manage/pre-release-features). Beginning with [update 4163547](https://support.microsoft.com/help/4163547) to version 1802, this feature is no longer a pre-release feature.  

> [!Note]  
> Continue to use the **Cisco Legacy AnyConnect** option for macOS VPN profiles. 



## April 2018

### New in Microsoft Intune

#### Intune adapts to Fluent Design System in the Company Portal app for Windows 10 
<!--1195010-->
The Intune Company Portal app for Windows 10 has been updated with the [Fluent Design System's navigation view](/windows/uwp/design/basics/navigation-basics). Along the side of the app notice a static, vertical list of all top-level pages. Click any link to quickly view and switch between pages. This update is the first of several you'll see as part of our ongoing effort to create a more adaptive, empathetic, and familiar experience in Intune. To see the updated look, go to [What's new in the app UI](/intune/whats-new-app-ui).

#### Improved device tiles in the Windows 10 Company Portal
<!--2213364-->
The tiles have been updated to be more accessible to low-vision users and to perform better for screen reading tools.


#### Test the Company Portal for macOS on virtual machines
<!--2216679-->
We've published guidance to help IT admins test the Company Portal app for macOS on virtual machines in Parallels Desktop and VMware Fusion. For more information, see [enroll virtual macOS machines for testing](/intune/macos-enroll#enroll-virtual-macos-machines-for-testing).


#### Send diagnostic reports in Company Portal app for macOS
<!--2216677-->
The Company Portal app for macOS devices was updated to improve how users report Intune-related errors. From the Company Portal app, your employees can:

- Upload diagnostic reports directly to the Microsoft developer team.
- Email an incident ID to your company's IT support team.


#### Updated Help experience on Company Portal app for Android 
<!--1631531-->
We've updated the Help experience in the Company Portal app for Android to align with best practices for the Android platform. Now when users encounter a problem in the app, they can tap **Menu** > **Help** and:
- Upload diagnostic logs to Microsoft.
- Send an email that describes the problem and incident ID to a company support person.


#### Update where to configure your app protection policies 
<!--2144597-->
In the Azure portal within the Microsoft Intune service, we're going to temporarily redirect you from the **Intune App Protection** area to the **Mobile app** section. All of your app protection policies are already in the **Mobile app** section in Intune under app configuration. Instead of going to Intune App Protection, you'll just go to Intune. In April 2018, we'll stop the redirection and fully remove **Intune App Protection**. After this time, there's only one location for app protection policies within Intune. 

**How does this change affect me?** This change will affect both Intune standalone customers and hybrid (Intune with Configuration Manager) customers. This integration will help simplify your cloud management administration.

**What do I need to do to prepare for this change?** Tag **Intune** as a favorite instead of **Intune App Protection**. Familiarize yourself with the App protection policy workflow in the **Mobile app** area within Intune. We'll redirect for a short period of time and then remove **App Protection**. Remember, all app protection policies are already in Intune and you can modify any of your conditional access policies. For more information about modifying conditional access policies, see [Conditional access in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal). For more information, see [What are app protection policies?](https://docs.microsoft.com/intune/app-protection-policy) 




#### User experience update for the Company Portal app for iOS 
<!--1412866-->
We've released a major user experience update to the Company Portal app for iOS. The update features a complete visual redesign that includes a modernized look and feel. We've maintained the functionality of the app, but increased its usability and accessibility.  

You'll also see:
- Support for iPhone X.
- Faster app launch and loading responses, to save users time.
- Additional progress bars to provide users with the most up-to-date status information.
- Improvements to the way users upload logs, so if something goes wrong, it's easier to report.  

To see the updated look, go to [What's new in the app UI](https://docs.microsoft.com/intune/whats-new-app-ui).



## March 2018

### New in Microsoft Intune

#### Windows Company Portal Send Feedback Option may no longer work
<!--2070166-->
The Windows Company Portal app has a 'Send Feedback' option allowing users to send feedback about the app to Microsoft. From April 30, 2018, this option continues to be supported only on the Windows 10 Company Portal app running on Windows 10 version 1607 and later.   

**How does this change affect me?**

If you don't have the Windows Company Portal app installed for end users, then disregard this message.

If any of your end users have the Company Portal app, then starting April 30 the 'Send Feedback' button no longer works for the app in the following scenarios:  

 - Windows 10 Company Portal app on Windows 10 version 1507 and version 1511  

 - Windows Phone 8.1 Company Portal app  

For impacted devices, the 'Send Feedback' option fails and doesn't succeed even on retrying. To send feedback to Microsoft about experiences on these platforms, there are alternate feedback channels listed below.

**What do I need to do to prepare for this change?**

Inform your end users of this change and update any user guidance if necessary. 

Inform end users using the Company Portal on Windows Phone 8.1, Windows 10 version 1507, and Windows 10 version 1511 that they have two alternate feedback channels available. They can:  

- Use the Feedback Hub app on Windows 10  
- Send an email to WinCPfeedback@microsoft.com  

Ask end users on Windows 10 version 1607 or later to update to the latest version of the Windows Company Portal available in the Microsoft Store.



#### Azure Active Directory web sites can require the Intune Managed Browser App and support Single Sign-On for the Managed Browser (Public Preview)
<!-- 710595 --> 
Using Azure Active Directory (Azure AD), you can now restrict access to web sites on mobile devices to the Intune Managed Browser app. In the managed browser, web site data will remain secure and separate from end-user personal data. In addition, the Managed Browser will support Single Sign-On capabilities for sites protected by Azure AD. Signing in to the Managed Browser, or using the Managed Browser on a device with another app managed by Intune, allows the Managed Browser to access corporate sites protected by Azure AD without the user having to enter their credentials. This functionality applies to sites like Outlook Web Access (OWA) and SharePoint Online, as well as other corporate sites like intranet resources accessed through the Azure App Proxy.



## February 2018

### New in Microsoft Intune

- **macOS Company Portal support for enrollments that use the Device Enrollment Manager**  
    Users can now use the Device Enrollment Manager when enrolling with the macOS Company Portal.
    <!-- 1352411 -->


## January 2018

### New in Microsoft Intune

- **Approve the Company Portal app for Android for Work**  
  If your organization uses Android for Work, manually approve the Company Portal app for Android. It then continues to receive automatic updates from the managed Google Play store.
  <!--1797090 -->  

- **Conditional Access policies for Intune are only available from the Azure portal**   
  Starting with this release, you must configure and manage your Conditional Access policies in the [Azure portal](https://portal.azure.com) from **Azure Active Directory** > **Conditional Access**. For your convenience, you can also access these settings from Intune in the Azure portal at **Intune** > **Conditional Access**.
  <!-- 1737088 1634311 --> 

- **Updates to compliance emails**    
  When an email is sent to report a noncompliant device, details about the noncompliant device are included. 
  <!--1637547 -->

- **New functionality for the "Resolve" action for Android devices**    
  The Company Portal app for Android is expanding the "Resolve" action for **Update device settings** to resolve [device encryption issues](https://docs.microsoft.com/intune-user-help/encrypt-your-device-android).
  <!--1583480-->

- **Remote lock available in Company Portal app for Windows 10**    
  End users can now remotely lock their devices from the Company Portal app for Windows 10. This action isn't displayed for the local device they're actively using.
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
  Apps managed by the Intune App SDK can send SMS messages.
  <!-- 1414050  -->   

- **Company Portal app for macOS is available**   
  The Intune Company Portal on macOS has an updated experience. It's optimized to cleanly display all the information and compliance notifications your users need for all the devices they've enrolled. And, once the Intune Company Portal has been deployed to a device, Microsoft AutoUpdate for macOS provides updates to it. Download the new Intune Company Portal for macOS by logging into the Intune Company Portal website from a macOS device.
  <!--1541700-->   

- **Microsoft Planner is now part of the mobile app management (MAM) list of approved apps**    
  The Microsoft Planner app for iOS and Android is now part of the approved apps for mobile app management (MAM). Configure the app from Intune App Protection in the Azure portal to all tenants. For details, see [MAM list of approved apps](https://www.microsoft.com/cloud-platform/microsoft-intune-apps).
  <!-- 1248473 -->    

- **Access to managed app logs for iOS**    
  End users with the managed Browser installed can now view the management status of all Microsoft published apps and send logs for troubleshooting their managed iOS apps.
  <!-- 1469920 -->    

  Learn how to enable the troubleshooting mode in the Managed Browser on an iOS device, see [How to access to managed app logs using the Managed Browser on iOS](https://docs.microsoft.com/intune/app-configuration-managed-browser#how-to-access-to-managed-app-logs-using-the-managed-browser-on-ios).

- **Improvements to device setup workflow in the Company Portal for iOS in version 2.9.0**    
  We've improved the device setup workflow in the Company Portal app for iOS. The language is more user-friendly and we've combined screens where possible. We have also made the language more specific to your company by using your company name throughout the setup text. You can see this updated workflow on the [what's new in app UI](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-november-13-2017) page.

- **Feedback prompts for the Company Portal app for Android**    
  The Company Portal app for Android now requests end-user feedback. This feedback is sent directly to Microsoft, and provides end users with an opportunity to review the app in the public Google Play store. Feedback isn't required, and can easily be dismissed so users can continue using the app. 
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
  With this release, we've updated the VPN profile wizard and properties pages to display settings appropriate for the selected platform. This feature was previously available in Configuration Manager Technical Preview 1709. It's now available in hybrid deployments with Intune and Configuration Manager (Current Branch) version 1710. For more information, see [Improved VPN profile experience in Configuration Manager console](/sccm/core/plan-design/changes/whats-new-in-version-1710#improved-vpn-profile-experience-in-configuration-manager-console).
  <!-- 1318232 -->


### New in Configuration Manger Technical Preview 1711

- **New compliance policy options for Windows 10**   
  You can now configure new options for compliance policies for Windows 10 devices. The new settings include policies for Firewall, User Account Control, Windows Defender Antivirus, and OS build versioning. For details, see [New compliance policy options for Windows 10](/sccm/core/get-started/capabilities-in-technical-preview-1711#new-compliance-policy-options-for-windows-10).



## October 2017

### New in Configuration Manager Technical Preview 1709

- **Improved VPN Profile experience in Configuration Manager console**      
  VPN profile settings are now filtered according to platform. When you create new VPN profiles, each supported platform contains only the settings appropriate for the platform. Existing VPN profiles aren't affected. You can read more about this change [here](/sccm/core/get-started/capabilities-in-technical-preview-1709#improved-vpn-profile-experience-in-configuration-manager-console).
  <!-- 1313282 -->


### New in Microsoft Intune  

- **Help your users help themselves with the Company Portal app for Android**     
  The Company Portal app for Android has added instruction for end users to help them understand, and possibly self-solve on new use cases.
    - If end users have reached the maximum number of devices that they're allowed to add, they're guided to the [Azure Active Directory portal](https://account.activedirectory.windowsazure.com/r/#/profile) to remove a device.
    - End users are given steps to follow to help them [fix activation errors on Samsung Knox devices](https://go.microsoft.com/fwlink/?linkid=859718) or to [turn off power-saving mode](https://docs.microsoft.com/intune-user-help/power-saving-mode-android). If neither of those solutions resolve their issue, we provide an explanation of how to [submit logs to Microsoft](https://docs.microsoft.com/intune-user-help/send-logs-to-microsoft-android).
  <!-- 1573324, 1573150, 1558616, 1564878 -->      

- **Device setup progress indicator in Android Company Portal**    
  The Company Portal app for Android shows a device setup progress indicator when a user is enrolling their device. The indicator shows new statuses, beginning with "Setting up your device...", then "Registering your device...", then "Finishing registering your device...", then "Finishing setting up your device...".  
  <!--1565657-->    

- **Certificate-based authentication support on the Company Portal for iOS**    
  We have added support for certificate-based authentication (CBA) in the Company Portal app for iOS. Users with CBA enter their username, then tap the "Sign in with a certificate" link. CBA is already supported on the Company Portal apps for Android and Windows. You can learn more on the [sign into the Company Portal app](https://docs.microsoft.com/intune-user-help/sign-in-to-the-company-portal) page.
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
  We're adding **Ownership Type** to the Device Details screen on all Company Portal apps. This information allows users to find out more about privacy directly from the [What information can your company see?](https://docs.microsoft.com/intune-user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune) article. This improvement rolls out across all Company Portal apps in the near future. We announced this feature for iOS in [September](https://docs.microsoft.com/intune/whats-new#week-of-september-11-2017). 
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



## Notices

### Plan for Change: Intune supports macOS 10.12 and higher in December 
<!--2970975--> 

Apple released macOS 10.14, so starting in December 2018, Intune will support macOS 10.12 and higher. 

#### How does this affect me?

Starting in December, users on devices with macOS 10.11 and prior can't use the Company Portal to enroll into Intune. To continue to receive support and new features, they'll need to upgrade their device to macOS 10.12 or higher, and upgrade the Company Portal app to the latest version. 

MacOS versions 10.12 and higher are currently supported on: 
- MacBook (late 2009 or newer)  
- iMac (late 2009 or newer)
- MacBook Air (late 2010 or newer)  
- MacBook Pro (late 2010 or newer)  
- Mac Mini (late 2010 or newer)  
- Mac Pro (late 2010 or newer)  

After December, end users who have devices other than the ones listed above can't access the latest version of the Company Portal app for macOS. You can continue to manage existing enrolled devices running unsupported versions below macOS 10.12.

#### What do I need to do to prepare for this change?

- Request your users to upgrade their devices to a supported OS version before December 2018.  
- Check your Intune reporting in the Azure portal, to see what devices or users may be affected. Go to **Devices** > **All devices**, and filter by **OS**. You can add in additional columns to help identify who in your organization has devices running macOS 10.11.  
- If you're using hybrid mobile device management (MDM), in the Configuration Manager console, go to the **Assets and Compliance** workspace, and select the **Devices** node. Right-click the columns to add the **Operating System** and **Client Version** columns. Then sort by OS version. Note that hybrid MDM is now deprecated, and you should move to Intune on Azure as soon as possible. 
 
#### Additional Information
For more information, see [Enroll your macOS device in Intune with the Company Portal app](https://docs.microsoft.com/intune-user-help/enroll-your-device-in-intune-macos-cp).


### Plan for Change: New Intune support experience for Premier customers 
<!--2828727-->
As a Microsoft Premier customer, you can currently use the [Microsoft Premier Online (MPO) portal](https://premier.microsoft.com) and [Intune on Azure](https://portal.azure.com) to create support requests for Intune. Starting on December 3, 2018, to continue enhancing the Premier support experience, you will be able to create support requests only in Intune on Azure.

#### How does this affect me?
After December 3, you can't create support requests in MPO. If you try, you’ll see a prompt that you can't dismiss redirecting you to Intune on Azure. When you create a support request in the Azure portal, it's routed to Intune-dedicated Microsoft Support. They'll diagnose and resolve your issue in a timely manner. If you create a support request in the MPO portal, you can't view it in the Azure portal. Start only creating support requests in Intune on Azure.  

If you use hybrid mobile device management (hybrid MDM) or use co-management, continue to use MPO to create support requests for Configuration Manager, but use the Azure portal to create support requests for Intune. As a reminder, hybrid MDM is deprecated, and you should plan to move to Intune on Azure as soon as possible. For more information, see [Move from Hybrid Mobile Device Management to Intune on Azure](https://aka.ms/hybrid_notification).

Note that only users with Global Administrator, Intune Service Administrator, and Service Support Administrator roles can create support tickets in the Azure portal.

#### What can I do to prepare for this change?
- Stop using MPO for Intune-related support requests. Use Intune on Azure to create and manage all your Intune support requests.  
- Notify your helpdesk and update documentation, if necessary.  
- If you have users without Global administrator or Intune Service Administrator roles currently creating support requests in MPO, assign them the Service Support Administrator role in Azure Active Directory. Users require one of these roles to create support tickets in the Azure portal.  

#### Additional Information
For more information, see the [Microsoft Intune support team blog post](https://aka.ms/IntuneSupport_MPO_to_Azure).


### Plan for change: Use Intune on Azure now for your MDM management 
<!--1227338-->
Over a year ago, we announced [public preview of Intune on Azure](https://cloudblogs.microsoft.com/enterprisemobility/2016/12/07/public-preview-of-intune-on-azure/) and followed up six months ago with [general availability of the new admin experience](https://cloudblogs.microsoft.com/enterprisemobility/2017/06/08/the-new-intune-and-conditional-access-admin-consoles-are-ga/) for Intune. Starting on August 31, 2018, we will turn off mobile device management (MDM) in the classic Silverlight console for those customers using Intune standalone. Instead, use [Intune on Azure](https://aka.ms/Intune_on_Azure) for your MDM needs. If you're still using the classic console for MDM, please stop and familiarize yourself with Intune on Azure. We don't expect any end user impact with this change. Classic PC management with Intune remains in Silverlight. For more information, see the [Intune support team blog post](https://aka.ms/Intune_on_Azure_mdm).


### Plan for Change: Upcoming macOS and Intune password enforcement change
<!--1873216-->
In the September service release, Intune plans to integrate Apple's newly released "Change Password at Next Auth" setting for devices running macOS versions 10.13 and above. Before this setting was introduced, MDM providers had no way of verifying that the passcode on a device had been changed to ensure compliance. Intune's configuration and compliance policies only validated that the next time a password was changed on the device, it would be marked as compliant. Your macOS users will receive a request to update their password when we integrate this new Apple feature, even if their password is already compliant.

#### How does this change affect me?
This change only affects Intune standalone or hybrid MDM customers with a macOS device policy. Apple has introduced the Change Password at New Auth setting. Now Intune can force users to update their password to one that's compliant when you push a password policy. If you block company resources until the device is marked compliant, then know your end users may be blocked from accessing company resources such as email or SharePoint sites until they reset their password. In the future, all updates to configuration and compliance password policies will force targeted users to update their passwords.

#### What do I need to do to prepare for this change?
You may want to let your helpdesk know. If you don't want to enforce this macOS device policy, unassign or delete your existing macOS policy. Our customer research prior to implementing this change indicated most customers won't be affected by this change. End users typically update their password after receiving a request to enroll with a password, or reset their password to remain compliant.  


### Plan for change: Intune moving to support iOS 10 and later in September 2018 
<!--2454656-->

In September 2018, Apple is expected to release iOS 12. Shortly after the release, we'll move Intune enrollment, the Company Portal, and the managed browser to support iOS 10 and later.

#### How does this change affect me?

Office 365 mobile apps are supported on iOS 10 and later, so you may have already upgraded your OS or devices. If so, this move won't affect you.

However, if you have any of the devices listed below, or want to enroll any of the devices listed below, they only support iOS 9 and earlier. To continue to access the Intune Company Portal, you must upgrade these devices by September to devices that support iOS 10 or later: 

- iPhone 4S
- iPod Touch 
- iPad 2
- iPad (Third Generation)
- iPad Mini (First Generation)

Starting in July, MDM-enrolled devices with both iOS 9 and the Company Portal will receive a prompt to upgrade their OS or device. If you use app protection policies, you can also set the "Require minimum iOS operating system (Warning only)" access setting.  

#### What do I need to do to prepare for this change?

Check for devices or users that are affected in your organization. In Intune in the Azure portal, go to **Devices** > **All devices**, and filter by **OS**.  Click **Columns** to surface details such as OS version. Request that your users upgrade their devices to a supported OS version before September.


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

There's no immediate impact to any Windows Phone 8.1 device that is managed by the Intune service, including those devices enrolled in hybrid MDM. Devices that are enrolled continue to work. All policies, configurations, and apps continue to work as expected. Note, there are no improvements targeted for the Windows Phone 8.1 platform within the Intune service, and for the Windows Phone 8.1 Company Portal app.

We recommend upgrading eligible Windows Phone 8.1 devices to Windows 10 Mobile at your earliest opportunity.  

### End of support for Android 4.3 and lower
<!---1171127--->
*July 6, 2017*

Managed apps and the Company Portal app for Android require Android 4.4 and higher to access company resources. Devices that aren't updated before the beginning of October are no longer able to access the Company Portal or those apps. By December, all enrolled devices are force retired in December, resulting in loss of access to company resources. If you're using app protection policies without MDM, apps won't receive updates, and the quality of their experience diminishes over time.



## See Also

- [Past hybrid MDM features and notices](whats-new-hybrid-archive.md)
- [What's new for MDM in System Center 2012 Configuration Manager](https://technet.microsoft.com/library/mt445560.aspx)
