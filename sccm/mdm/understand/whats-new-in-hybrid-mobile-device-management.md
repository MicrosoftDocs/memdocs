---
title: "What's new in hybrid MDM with Configuration Manager | Microsoft Docs"
description: "Learn about the new mobile device management features available for hybrid deployments with Configuration Manager and Intune."
ms.custom: na
ms.date: 03/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
caps.latest.revision: 40
author: Mtillman
ms.author: mtillman
manager: angrobe
---
# What's new in hybrid mobile device management with System Center Configuration Manager and Microsoft Intune

*Applies to: System Center Configuration Manager (Current Branch)*

This article provides details on the new mobile device management (MDM) features available for hybrid deployments with System Center Configuration Manager and Microsoft Intune.  

##  Compatibility with Configuration Manager versions  

 Each section of this article lists hybrid features under 3 different categories. Use the following guidance to determine compatibility of the features in each category  with different versions of Configuration Manager:  

|Feature categories|Description|
|-|-|
|**New in Microsoft Intune** | In general, all the features listed under this category should work with all Configuration Manager releases including System Center 2012 R2 Configuration Manager releases, since these features only require the  Intune service and do not require additional functionality in  Configuration Manager.|
|**New in Configuration Manager Technical Preview**| All the features listed under this category only work with the specified Technical Preview release. To try out these features, you must install the Technical Preview version specified in the feature description. For more information, see [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md).|
|**New in Configuration Manager (current branch)**| All the features listed under this category only work with the specified version of Configuration Manager (current branch), such as version 1511 or 1602. If you're using an older version of Configuration Manager for your hybrid deployment, you must upgrade to the Configuration Manager (current branch)  version specified in the feature description. For more information, see [Upgrade to System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md).|

## New in April 2017

### New in Microsoft Intune

The following Intune features introduced in April 2017 work in hybrid deployments:

- **MyApps available for Managed Browser**

  Microsoft MyApps now have better support within the Managed Browser. Managed Browser users who are not targeted for management will be brought directly to the MyApps service, where they can access their admin-provisioned SaaS apps. Users who are targeted for Intune management will continue to be able to access MyApps from the built-in Managed Browser bookmark.

- **New icons for the Managed Browser and the Company Portal**

  The Managed Browser is receiving updated icons for both the Android and iOS versions of the app. The new icon will contain the updated Intune badge to make it more consistent with other apps in Enterprise Mobility + Security (EM+S). You can see the new icon for the Managed Browser on the [what's new in Intune app UI page](/intune/whats-new/whats-new-in-intune-app-ui.md).

  The Company Portal is also receiving updated icons for the Android, iOS, and Windows versions of the app to improve consistency with other apps in EM+S. These icons will be gradually released across platforms from April to late May.

- **Sign-in progress indicator in Android Company Portal**

  An update to the Android Company Portal app shows a sign-in progress indicator when the user launches or resumes the app. The indicator progresses through new statuses, beginning with "Connecting...", then "Signing in...", then "Checking for security requirements..." before allowing the user to access the app. You can see the new screens for the Company Portal app for Android on the [what's new in Intune app UI page](/intune/whats-new/whats-new-in-intune-app-ui.md).

## New hybrid features in February 2017

### New in Microsoft Intune

The following Intune features introduced in February 2017 work in hybrid deployments:

- **Modernizing the Company Portal website**

  The Company Portal website supports apps that are targeted to users who do not have managed devices. The website aligns with other Microsoft products and services by using a new contrasting color scheme, dynamic illustrations, and a "hamburger menu," which contains helpdesk contact details and information on existing managed devices. The landing page is rearranged to emphasize apps that are available to users, with carousels for Featured and Recently Updated apps. You can find before-and-after images available on the [UI updates](/intune/whats-new/whats-new-in-intune-app-ui) page.

- **New MDM server address for Windows devices**

  The MDM server address for enrolling Windows and Windows Phone devices has changed from manage.microsoft.com to enrollment.manage.microsoft.com. Notify your user to use enrollment.manage.microsoft.com as the MDM server address if prompted for it while enrolling a Windows or and Windows Phone device. This update also requires any CNAME in DNS that redirects EnterpriseEnrollment.contoso.com to manage.microsoft.com to be replaced with a CNAME in DNS that redirects EnterpriseEnrollment.contoso.com to EnterpriseEnrollment-s.manage.microsoft.com. For additional information about this change, visit http://aka.ms/intuneenrollsvrchange.

### New in Configuration Manager Technical Preview 1702

- **Android for Work Support**

  You can now manage Android devices using Android for Work in hybrid MDM environments using Configuration Manager Technical Preview 1702. Supported Android devices can now be enrolled as Android for Work devices, which creates a work profile on the device to which apps approved in Play for Work can be deployed. You can also configure and deploy configuration items, compliance policies, and resource access profiles for these devices. For more information, see [Android for Work support](/sccm/core/get-started/capabilities-in-technical-preview-1702#android-for-work-support).

- **Non-Compliant Apps Compliance Settings**

  You can now create non-compliant apps rules for Android and iOS apps in compliance policies. If devices have the specified applications installed, they will be marked “non-compliant” and will lose access to company resources according to conditional access policies in place. For more information [Conditional access device compliance policy improvements](/sccm/core/get-started/capabilities-in-technical-preview-1702#conditional-access-device-compliance-policy-improvements).

- **PFX Certificate Creation and Distribution and S/MIME Support**

  You can now create and deploy PFX certificates to users in a hybrid environment. These certificates can then be used for S/MIME email encryption and decryption by devices that the user has enrolled. For more information, see [Create PFX certificates with S MIME support](/sccm/core/get-started/capabilities-in-technical-preview-1702#create-pfx-certificates-with-s-mime-support).

- **Support for additional iOS configuration settings**
   
    You now have 42 additional iOS settings that you can configure as part of a configuration item. Most of the settings (35 in all) have been added for supervised iOS devices. For more information, see  [New compliance settings for iOS devices](/sccm/core/get-started/capabilities-in-technical-preview-1702#new-compliance-settings-for-ios-devices).

## New hybrid features in January 2017

### New in Microsoft Intune

The following Intune features introduced in January 2017 work in hybrid deployments:

- **Android 7.1.1 support**

  Intune now fully supports and manages Android 7.1.1.

- **Resolve issue where iOS devices are inactive, or the admin console cannot communicate with them**

  When users’ devices lose contact with Intune, you can give them new troubleshooting steps to help them regain access to company resources. See [Devices are inactive, or the admin console cannot communicate with them](/intune/troubleshoot/troubleshoot-device-enrollment-in-intune#devices-are-inactive-or-the-admin-console-cannot-communicate-with-them).

### New in Configuration Manager Technical Preview 1701

- **Android and iOS versions are no longer targetable in creation wizards for hybrid MDM**

  Beginning in Technical Preview 1701 for hybrid mobile device management (MDM), you no longer need to target specific versions of Android and iOS when creating new policies and profiles for Intune-managed devices. With this change, hybrid deployments can provide support more quickly for new Android and iOS versions without needing a new Configuration Manager release or extension. To learn more, see [Android and iOS versions are no longer targetable in creation wizards](/sccm/core/get-started/capabilities-in-technical-preview-1701#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm).


## New hybrid features in December 2016

### New in Microsoft Intune

The following Intune features introduced in Decmember 2016 work in hybrid deployments:

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


## New hybrid features in November 2016

### New in Microsoft Intune

The following Intune features introduced in November 2016 work in hybrid deployments:

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


### See Also

- [Past hybrid MDM features](whats-new-hybrid-archive.md)
- [What's new for MDM in System Center 2012 Configuration Manager](https://technet.microsoft.com/library/mt445560.aspx)
