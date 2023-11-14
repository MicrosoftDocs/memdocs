---
title: include file
description: include file
author: ErikjeMS  
ms.service: microsoft-intune
ms.topic: include
ms.date: 09/08/2023
ms.author: erikje
ms.custom: include file
---

These notices provide important information that can help you prepare for future Intune changes and features.

### Wrapped iOS apps and iOS apps using the Intune App SDK will require Azure AD app registration

We're making updates to improve the security of the Intune mobile application management (MAM) service. This update will require iOS wrapped apps and SDK integrated apps to be [registered with Microsoft Entra ID](/entra/identity-platform/quickstart-register-app) (formerly Azure Active Directory (Azure AD)) by March 31, 2024 to continue receiving MAM policy. 

#### How does this affect you or your users?

If you have wrapped apps or SDK integrated apps that aren't registered with Azure AD, these apps will be unable to connect to the MAM service to receive policy and your users will not be able to access apps that are not registered.

#### How can you prepare?

Prior to this change, you will need to register the apps with Azure AD. See below for detailed instructions.

1. Register your apps with Azure AD by following these instructions: [Register an application with the Microsoft identity platform](/entra/identity-platform/quickstart-register-app).
1. Add the custom redirect URL to your app settings as documented [here](https://github.com/AzureAD/microsoft-authentication-library-for-objc#configuring-msal).
1. Give your app access to the Intune MAM service, for instructions see [here](../developer/app-sdk-get-started.md#give-your-app-access-to-the-intune-mobile-app-management-service).
1. Once the above changes are completed, configure your apps for Microsoft Authentication Library (MSAL):
   1. For wrapped apps: Add the Azure AD application client ID into the command-line parameters with the Intune App Wrapping Tool as outlined in the documentation: [Wrap iOS apps with the Intune App Wrapping Tool | Microsoft Learn](../developer/app-wrapper-prepare-ios.md#command-line-parameters) -ac and -ar are required parameters. Each app will need a unique set of these parameters. -aa is only required for single tenant applications.
   1. For SDK integrated apps see, [Microsoft Intune App SDK for iOS developer guide | Microsoft Learn](../developer/app-sdk-ios.md#configure-msal-settings-for-the-intune-app-sdk). ADALClientId and ADALRedirectUri/ADALRedirectScheme are now required parameters. ADALAuthority is only required for single tenant applications.
1. Deploy the app.
1. To validate the above steps:
   1. Target "com.microsoft.intune.mam.IntuneMAMOnly.RequireAADRegistration" application configuration policy and set it to Enabled - [Configuration policies for Intune App SDK managed apps - Microsoft Intune | Microsoft Learn](../apps/app-configuration-policies-managed-app.md)
   1. Target App Protection Policy to the application. Enable the [“Work or school account credentials for access” policy](../apps/app-protection-policy-settings-ios.md#access-requirements) and set “Recheck the access requirements after (minutes of inactivity)” setting to a low number like 1.
1. Then launch the application on a device and verify if the sign-in (which should be required every minute on app launch) happens successfully with the configured parameters.
1. Note that if you only do step #6 and #7 before doing the other steps, you might be blocked on application launch. You will also notice the same behavior if some of the parameters are incorrect.
1. Once you’ve completed the validation steps, you can undo the changes made in step #6.
> [!NOTE]
> Intune will soon require an Azure AD device registration for iOS devices using MAM. If you have Conditional Access policies enabled, your devices should already be registered, and you will not notice any change. For more information see, [Microsoft Entra registered devices - Microsoft Entra | Microsoft Learn](/entra/identity/devices/concept-device-registration).

### Plan for Change: Transition Jamf macOS devices from Conditional Access to Device Compliance

We've been working with Jamf on a migration plan to help customers transition macOS devices from Jamf Pro’s Conditional Access integration to their Device Compliance integration. The Device Compliance integration uses the newer Intune partner compliance management API, which involves a simpler setup than the partner device management API and brings macOS devices onto the same API as iOS devices managed by Jamf Pro. The platform Jamf Pro’s Conditional Access feature is built on will no longer be supported after September 1, 2024.

Note that customers in some environments cannot be transitioned initially, for more details and updates read the blog: [Support tip: Transitioning Jamf macOS devices from Conditional Access to Device Compliance](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-transitioning-jamf-macos-devices-from-conditional/ba-p/3913059).

#### How does this affect you or your users?

If you're using Jamf Pro’s Conditional Access integration for macOS devices, follow Jamf’s documented guidelines to migrate your devices to Device Compliance integration: [Migrating from macOS Conditional Access to macOS Device Compliance – Jamf Pro Documentation](https://learn.jamf.com/bundle/jamf-pro-documentation-current/page/Conditional_Access.html#ariaid-title6).

After the Device Compliance integration is complete, some users might see a one-time prompt to enter their Microsoft credentials.
 
#### How can you prepare?

If applicable, follow the instructions provided by Jamf to migrate your macOS devices. If you need help, contact Jamf Customer Success. For more information and the latest updates, read the blog post: [Support tip: Transitioning Jamf macOS devices from Conditional Access to Device Compliance](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-transitioning-jamf-macos-devices-from-conditional/ba-p/3913059).

### Update to the latest Intune App SDK and Intune App Wrapper for iOS to support iOS/iPadOS 17

To support the upcoming release of iOS/iPadOS 17, update to the latest versions of the Intune App SDK and the App Wrapping Tool for iOS to ensure applications stay secure and run smoothly. Additionally, for organizations using the Conditional Access grant “Require app protection policy”, users should update their apps to the latest version prior to upgrading to iOS 17. You can learn more by reading the blog: [Update Intune App SDK, Wrapper, and iOS apps using MAM policies to support iOS/iPadOS 17](https://techcommunity.microsoft.com/t5/intune-customer-success/update-intune-app-sdk-wrapper-and-ios-apps-using-mam-policies-to/ba-p/3926732).

### Plan for Change: Removal of Microsoft Graph Beta API Android LOB app properties ‘identityVersion’ and ‘identityName’

With Intune’s October (2310) service release, we'll be removing the Android line-of-business (LOB) app properties “identityVersion” and “identityName” from the Microsoft Graph Beta API managedAndroidLobApp resource type. The same data can be found using the Graph API "versionCode” and “versionName” properties.

#### How does this affect you or your users?

If you have automation or reporting using the Android LOB app properties “identityVersion” and “identityName”, you'll need update to the “versionName” and “versionCode” properties for the Graph call to continue working. 

#### How can you prepare?

Update your documentation and reporting as needed.

### Plan for Change: Intune ending support for Android device administrator on devices with GMS access in August 2024

[Google has deprecated](https://blog.google/products/android-enterprise/da-migration/) Android device administrator management, continues to remove management capabilities, and no longer provides fixes or improvements. Due to these changes, Intune will be ending support for Android device administrator management on devices with access to Google Mobile Services (GMS) beginning **August 30, 2024**. Until that time, we will support device administrator management on devices running Android 14 and earlier. For more details, read the blog: [Microsoft Intune ending support for Android device administrator on devices with GMS access in August 2024](https://aka.ms/Intune-Android-DA-blog).

#### How does this affect you or your users?

After Intune ends support for Android device administrator, devices with access to GMS will be impacted in the following ways:   

1. Users won't be able to enroll devices with Android device administrator.  
2. Intune won't make changes or updates to Android device administrator management, such as bug fixes, security fixes, or fixes to address changes in new Android versions.  
3. Intune technical support will no longer support these devices.

#### How can you prepare?

Stop enrolling devices into Android device administrator and migrate impacted devices to other management methods. You can check your Intune reporting to see which devices or users might be affected. Go to **Devices** > **All devices** and filter the OS column to **Android (device administrator)** to see the list of devices. 

Read the blog, [Microsoft Intune ending support for Android device administrator on devices with GMS access in August 2024](https://aka.ms/Intune-Android-DA-blog), for our recommended alternative Android device management methods and information about the impact to devices without access to GMS.

### Plan for Change: Intune is moving to support iOS/iPadOS 15 and later<!--24161619-->

Later this year, we expect iOS 17 to be released by Apple. Microsoft Intune, including the Intune Company Portal and Intune app protection policies (APP, also known as MAM), will require [iOS 15/iPadOS 15 and higher](../fundamentals/supported-devices-browsers.md) shortly after iOS 17’s release.

#### How does this affect you or your users?

If you're managing iOS/iPadOS devices, you might have devices that won't be able to upgrade to the minimum supported version (iOS/iPadOS 15). 

Because Office 365 mobile apps are supported on iOS/iPadOS 15.0 and later, this change might not affect you. You've likely already upgraded your OS or devices. 

To check which devices support iOS 15 or iPadOS 15 (if applicable), see the following Apple documentation:

- [Supported iPhone models](https://support.apple.com/guide/iphone/supported-models-iphe3fa5df43/15.0/ios/15.0)
- [Supported iPad models](https://support.apple.com/guide/ipad/supported-models-ipad213a25b2/15.0/ipados/15.0)

> [!NOTE]
> Userless iOS and iPadOS devices enrolled through Automated Device Enrollment (ADE) have a slightly nuanced support statement due to their shared usage. The minimum supported OS version will change to iOS 15/iPadOS 15 while the allowed OS version will change to iOS 12/iPadOS 12 and later. See [this statement about ADE Userless support](https://aka.ms/ADE_userless_support) for more information.

#### How can you prepare?

Check your Intune reporting to see what devices or users might be affected. For devices with mobile device management (MDM), go to **Devices** > **All devices** and filter by OS. For devices with app protection policies, go to **Apps** > **Monitor** > **App protection status** and use the *Platform* and *Platform version* columns to filter. Note that there's a current known issue where several columns are missing from the App protection status report. We expect a fix soon. 

To manage the supported OS version in your organization, you can use Microsoft Intune controls for both MDM and APP. For more information, see [Manage operating system versions with Intune](../fundamentals/manage-os-versions.md).

### Plan for change: Intune is moving to support macOS 12 and higher later this year<!--24229012-->

Later this year, we expect macOS 14 Sonoma to be released by Apple. Microsoft Intune, the Company Portal app and the Intune mobile device management agent will be moving to support macOS 12 and later. Since the Company Portal app for iOS and macOS are a unified app, this change will occur shortly after the release of iOS/iPadOS 17.

#### How does this affect you or your users?

This change only affects you if you currently manage, or plan to manage, macOS devices with Intune. This change might not affect you because your users have likely already upgraded their macOS devices. For a list of supported devices, see [macOS Monterey is compatible with these computers](https://support.apple.com/HT212551).

> [!NOTE]
> Devices that are currently enrolled on macOS 11.x or earlier will continue to remain enrolled even when those versions are no longer supported. New devices will be unable to enroll if they are running macOS 11.x or earlier.

#### How can you prepare?

Check your Intune reporting to see what devices or users might be affected. Go to **Devices** > **All devices** and filter by macOS. You can add more columns to help identify who in your organization has devices running macOS 11.x or earlier. Ask your users to upgrade their devices to a supported OS version.


### Plan for Change: Ending support for Microsoft Store for Business and Education apps

In April 2023, we'll begin ending support for the Microsoft Store for Business experience in Intune. This occurs in several stages. For more information, see: [Adding your Microsoft Store for Business and Education apps to the Microsoft Store in Intune](https://aka.ms/Intune/MSfB-support)

### How does this affect you or your users?

If you're using Microsoft Store for Business and Education apps:

1. On April 30, 2023, Intune will disconnect Microsoft Store for Business services. Microsoft Store for Business and Education apps won't be able to sync with Intune and the connector page will be removed from the Intune admin center.
2. On June 15, 2023, Intune will stop enforcing online and offline Microsoft Store for Business and Education apps on devices. Downloaded applications remain on the device with limited support. Users might still be able to access the app from their device, but the app won't be managed. Existing synced Intune app objects remain to allow admins to view the apps that had been synced and their assignments. Additionally, you'll not be able to sync apps via the Microsoft Graph API syncMicrosoftStoreForBusinessApps and related API properties will display stale data.
3. On September 15, 2023, Microsoft Store for Business and Education apps will be removed from the Intune admin center. Apps on the device remain until intentionally removed. The Microsoft Graph API microsoftStoreForBusinessApp will no longer be available about a month later.

Note that the retirement of Microsoft Store for Business and Education was [announced in 2021](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/evolving-the-microsoft-store-for-business-and-education/ba-p/2569423). When the Microsoft Store for Business and Education portals are retired, admins will no longer be able to manage the list of Microsoft Store for Business and Education apps that are synced or download offline content from the Microsoft Store for Business and Education portals.

### How can you prepare?

We recommend adding your apps through the new Microsoft Store app experience in Intune. If an app isn't available in the Microsoft Store, you need to retrieve an app package from the vendor and install it as a line-of-business (LOB) app or Win32 app. For instructions read the following articles:

- [Add Microsoft Store apps to Microsoft Intune](../apps/store-apps-microsoft.md)
- [Add a Windows line-of-business app to Microsoft Intune](../apps/lob-apps-windows.md)
- [Add, assign, and monitor a Win32 app in Microsoft Intune](../apps/apps-win32-add.md)

Related information

- [Update to Intune integration with the Microsoft Store on Windows](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/update-to-endpoint-manager-integration-with-the-microsoft-store/ba-p/3585077)
- [Unpacking Endpoint Management: The future of app management in Intune](https://techcommunity.microsoft.com/t5/endpoint-management-events/unpacking-endpoint-management-the-future-of-app-management-in/ev-p/3724878)

### Plan for Change: Ending support for Windows Information Protection

Microsoft Windows [announced](https://go.microsoft.com/fwlink/?linkid=2202124) they're ending support for Windows Information Protection (WIP). The Microsoft Intune family of products will be discontinuing future investments in managing and deploying WIP. In addition to limiting future investments, we removed support for WIP *without enrollment* scenario at the end of calendar year 2022.

### How does this affect you or your users?

If you have enabled WIP policies, you should turn off or disable these policies.

### How can you prepare?

We recommend disabling WIP to ensure users in your organization do not lose access to documents that have been protected by WIP policy. Read the blog [Support tip: End of support guidance for Windows Information Protection](https://aka.ms/Intune-WIP-support) for more details and options for removing WIP from your devices.

### Plan for Change: Ending support for Windows 8.1 <!-- 14740233 -->

Microsoft Intune will be ending support for devices running Windows 8.1 on **October 21, 2022**. Additionally, the sideloading key scenario for line-of-business apps will stop being supported since it's only applicable to Windows 8.1 devices. 

Microsoft strongly recommends that you move to a supported version of Windows 10 or Windows 11, to avoid a scenario where you need service or support that is no longer available.

### How does this affect you or your users?

If you're managing Windows 8.1 devices those devices should be upgraded to a supported version of Windows 10 or Windows 11. There is no impact to existing devices and policies, however, you'll not be able to enroll new devices if they are running Windows 8.1.

### How can you prepare?

Upgrade your Windows 8.1 devices, if applicable. To determine which users’ devices are running Windows 8.1 navigate to [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Windows** > **Windows devices**, and filter by OS.

**Additional information**
- [Manage operating system versions with Intune](../fundamentals/manage-os-versions.md)

### Update your certificate connector for Microsoft Intune

As of June 1, 2022, Intune certificate connectors earlier than version 6.2101.13.0 may no longer work as expected and stop connecting to the Intune service. For more information on the certificate connector lifecycle and support see, [Certificate Connectors for Microsoft Intune](../protect/certificate-connector-overview.md).

#### How does this affect you or your users?

If you're impacted by this change, see MC393815 in the Message center.

#### How can you prepare?

Download, install, and configure the latest certificate connector. For more information see, [Install the Certificate Connector for Microsoft Intune](../protect/certificate-connector-install.md).

To check which version of the certificate connector you are using, follow these steps:

1. On a Windows Server running the Intune Certificate Connector, launch "Add or Remove programs".
2. A list of installed programs and applications will be displayed.
3. Look for an entry related to the Microsoft Intune Certificate Connector. There will be a "Version" associated with the connector. Note that names for older connectors may vary.

### Plan for change: Intune is moving to support Android 8.0 and later in January 2022<!-- 10946003 -->  

Microsoft Intune will be moving to support Android version 8.0 (Oreo) and later for mobile device management (MDM) enrolled devices on or shortly after January 7, 2022.  

#### How does this affect you or your users?

After January 7, 2022, MDM enrolled devices running Android version 7.x or earlier will no longer receive updates to the Android Company Portal or the Intune App. Enrolled devices will continue to have Intune policies applied but are no longer supported for any Intune scenarios. Company Portal and the Intune App will not be available for devices running Android 7.x and lower beginning mid-February; however, these devices won't be blocked from completing enrollment if the requisite app has been installed prior to this change. If you have MDM enrolled devices running Android 7.x or below, update them to Android version 8.0 (Oreo) or higher or replace them with a device on Android version 8.0 or higher.  

> [!NOTE]
> [Microsoft Teams devices](https://www.microsoft.com/en-us/microsoft-teams/across-devices/devices?rtc=2) are not impacted by this announcement and will continue to be supported regardless of their Android OS version.  

#### How can you prepare?  

Notify your helpdesk, if applicable, of this upcoming change in support. You can identify how many devices are currently running Android 7.x or below by navigating to **Devices** > **All devices** > **Filter**. Then filter by OS and sort by OS version. There are two admin options to help inform your users or block enrollment.

Here's how you can warn users:

- Create an app protection policy and configure [conditional launch](../apps/app-protection-policy-settings-android.md#conditional-launch) with a min OS version requirement that warns users.  
- Utilize a device compliance policy for [Android device administrator](../protect/compliance-policy-create-android.md) or [Android Enterprise](../protect/compliance-policy-create-android-for-work.md) and set the action for noncompliance to send an email or push notification to users before marking them noncompliant.  

Here's how you can block devices running on versions earlier than Android 8.0:  

- Create an app protection policy and configure conditional launch with a min OS version requirement that blocks users from app access.  
- Utilize a device compliance policy for Android device administrator or Android Enterprise to make devices running Android 7.x or earlier noncompliant. 
-  Set [enrollment restrictions](../fundamentals/manage-os-versions.md) that prevent devices running Android 7.x or earlier from enrolling.  

> [!NOTE]
> Intune app protection policies are supported on devices running Android 9.0 and later. See MC282986 for more details.  

### Plan for change: Intune APP/MAM is moving to support Android 9 and higher<!-- 10937255 -->

With the upcoming release of Android 12, Intune app protection policies (APP, also known as mobile application management) for Android will move to support Android 9 (Pie) and later on October 1, 2021. This change will align with Office mobile apps for Android support of the last four major versions of Android. 

Based on your feedback, we've updated our support statement. We're doing our best to keep your organization secure and protect your users and devices, while aligning with Microsoft app lifecycles.

> [!NOTE]
> This announcement doesn't affect [Microsoft Teams Android devices](https://www.microsoft.com/microsoft-teams/across-devices/devices?rtc=2). Those devices will continue to be supported regardless of their Android OS version.

#### How does this affect you or your users?

If you're using app protection policies (APP) on any device that's running Android version 8.x or earlier, or you decide to enroll any device that's running Android version 8.x or earlier, these devices will no longer be supported for APP. 

APP policies will continue to be applied to devices running Android 6.x to Android 8.x. But if you have problems with an Office app and APP, support will request that you update to a supported Office version for troubleshooting. To continue to receive support for APP, update your devices to Android version 9 (Pie) or later, or replace them with a device on Android version 9.0 or later before October 1, 2021.

#### How can you prepare?

Notify your helpdesk, if applicable, about this updated support statement. You also have two admin options to warn users:

- Configure a [conditional launch setting for APP](../apps/app-protection-policy-settings-android.md#conditional-launch) with a minimum OS version requirement to warn users.
- Use a device compliance policy for an [Android device administrator](../protect/compliance-policy-create-android.md) or [Android Enterprise](../protect/compliance-policy-create-android-for-work.md). Set the [action for noncompliance](../protect/actions-for-noncompliance.md) to send a message to users before marking them as noncompliant.

### Upgrade to the Microsoft Intune Management Extension<!-- 10102913 -->

We've released an upgrade to the Microsoft Intune Management Extension to improve handling of Transport Layer Security (TLS) errors on Windows 10 devices.

The new version for the Microsoft Intune Management Extension is 1.43.203.0. Intune automatically upgrades all versions of the extension that are earlier than 1.43.203.0 to this latest version. To check the version of the extension on a device, review the version for **Microsoft Intune Management Extension** in the program list under **Apps & features**.

For more information, see the information about security vulnerability CVE-2021-31980 in the [Microsoft Security Response Center](https://msrc.microsoft.com/update-guide/vulnerability/CVE-2021-31980).

#### How does this affect you or your users?

No action is required. As soon as the client connects to the service, it automatically receives a message to upgrade.

### Update to Endpoint Security antivirus Windows 10 profiles<!-- 9741752   -->

We've made a minor change to improve the antivirus profile experience for Windows 10. There's no user effect, because this change affects only what you'll see in the UI.

#### How does this affect you or your users?

Previously, when you configured a [Windows security profile](../protect/antivirus-security-experience-windows-settings.md) for the Endpoint Security antivirus policy, you had two options for most settings: **Yes** and **Not configured**. Those settings now include **Yes**, **Not configured**, and a new option of **No**. 

Previously configured settings that were set to **Not configured** remain as **Not configured**. When you create new profiles or edit an existing profile, you can now explicitly specify **No**.

In addition, the setting **Hide the Virus and threat protection area in the Windows Security app** has a child setting, **Hide the Ransomware data recovery option in the Windows Security app**. If the parent setting is set to **Not configured** and the child setting is set to **Yes**, both the parent and child settings are set to **Not configured**. That change takes effect when you edit the profile.

#### How can you prepare?

No action is needed. However, you might want to notify your helpdesk about this change.

### Plan for change: Intune is ending Company Portal support for unsupported versions of Windows

Intune follows the Windows 10 lifecycle for supported Windows 10 versions. We're now removing support for the associated Windows 10 Company Portals for Windows versions that are out of the Modern Support policy.

#### How does this affect you or your users?

Because Microsoft no longer supports these operating systems, this change might not affect you. You've likely already upgraded your OS or devices. This change only affects you if you're still managing unsupported Windows 10 versions. 

Windows and Company Portal versions that this change affects include:

- Windows 10 version 1507, Company Portal version 10.1.721.0
- Windows 10 version 1511, Company Portal version 10.1.1731.0
- Windows 10 version 1607, Company Portal version 10.3.5601.0
- Windows 10 version 1703, Company Portal version 10.3.5601.0
- Windows 10 version 1709, any Company Portal version

We won't uninstall these Company Portal versions, but we will remove them from the Microsoft Store and stop testing our service releases with them.

If you continue to use an unsupported version of Windows 10, your users won't get the latest security updates, new features, bug fixes, latency improvements, accessibility improvements, and performance investments. You won't be able to co-manage users by using System Center Configuration Manager and Intune.

#### How can you prepare?

In the Microsoft Intune admin center, use the [discovered apps](../apps/app-discovered-apps.md) feature to find apps with these versions. On a user's device, the Company Portal version is shown on the **Settings** page of the Company Portal. Update to a supported Windows and Company Portal version.  
