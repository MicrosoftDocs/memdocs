---
title: include file
description: include file
author: dougeby  
ms.service: microsoft-intune
ms.topic: include
ms.date: 03/13/2024
ms.author: dougeby
manager: dougeby
ms.custom: include file
---

These notices provide important information that can help you prepare for future Intune changes and features.

### Take Action: Enable multifactor authentication for your tenant before October 15, 2024

Starting on or after October 15, 2024, to further increase security, Microsoft will require admins to use multi-factor authentication (MFA) when signing into the Microsoft Azure portal, Microsoft Entra admin center, and Microsoft Intune admin center. To take advantage of the extra layer of protection MFA offers, we recommend enabling MFA as soon as possible. To learn more, review [Planning for mandatory multifactor authentication for Azure and admin portals](https://aka.ms/mfaforazure).

> [!NOTE]
> This requirement also applies to any services accessed through the Intune admin center, such as Windows 365 Cloud PC.

#### How does this affect you or your users?

MFA must be enabled for your tenant to ensure admins are able to sign-in to the Azure portal, Microsoft Entra admin center and Intune admin center after this change.

#### How can you prepare?

- If you haven't already, [set up MFA](https://aka.ms/mfaforazure) before **October 15, 2024**, to ensure your admins can access the Azure portal, Microsoft Entra admin center, and Intune admin center.
- If you're unable to set up MFA before this date, you can [apply to postpone the enforcement date](https://aka.ms/managemfaforazure).
- If MFA hasn't been set up before the enforcement starts, admins will be prompted to register for MFA before they can access the Azure portal, Microsoft Entra admin center, or Intune admin center on their next sign-in.

For more information, refer to: [Planning for mandatory multifactor authentication for Azure and admin portals](https://aka.ms/mfaforazure).

### Plan for Change: Intune is moving to support iOS/iPadOS 16 and later<!--28391935-->

Later this year, we expect iOS 18 and iPadOS 18 to be released by Apple. Microsoft Intune, including the Intune Company Portal and Intune app protection policies (APP, also known as MAM), will require [iOS 16/iPadOS 16 and higher](../fundamentals/supported-devices-browsers.md) shortly after the iOS/iPadOS 18 release. 

#### How does this affect you or your users?

If you're managing iOS/iPadOS devices, you might have devices that won't be able to upgrade to the minimum supported version (iOS 16/iPadOS 16). 

Given that Microsoft 365 mobile apps are supported on iOS 16/iPadOS 16 and higher, this may not affect you. You've likely already upgraded your OS or devices. 

To check which devices support iOS 16 or iPadOS 16 (if applicable), see the following Apple documentation:

- [Supported iPhone models](https://support.apple.com/guide/iphone/supported-models-iphe3fa5df43/16.0/ios/16.0)
- [Supported iPad models](https://support.apple.com/guide/ipad/supported-models-ipad213a25b2/16.0/ipados/16.0)

> [!NOTE]
> Userless iOS and iPadOS devices enrolled through Automated Device Enrollment (ADE) have a slightly nuanced support statement due to their shared usage. The minimum supported OS version will change to iOS 16/iPadOS 16 while the allowed OS version will change to iOS 13/iPadOS 13 and later. See [this statement about ADE Userless support](https://aka.ms/ADE_userless_support) for more information.

#### How can you prepare?

Check your Intune reporting to see what devices or users might be affected. For devices with mobile device management (MDM), go to **Devices** > **All devices** and filter by OS. For devices with app protection policies, go to **Apps** > **Monitor** > **App protection status** and use the *Platform* and *Platform version* columns to filter. 

To manage the supported OS version in your organization, you can use Microsoft Intune controls for both MDM and APP. For more information, see [Manage operating system versions with Intune](../fundamentals/manage-os-versions.md).

### Plan for change: Intune is moving to support macOS 13 and higher later this year<!--28391869-->

Later this year, we expect macOS 15 Sequoia to be released by Apple. Microsoft Intune, the Company Portal app and the Intune mobile device management agent will be moving to support macOS 13 and later. Since the Company Portal app for iOS and macOS are a unified app, this change will occur shortly after the release of macOS 15. This doesn't affect existing enrolled devices.

#### How does this affect you or your users?

This change only affects you if you currently manage, or plan to manage, macOS devices with Intune. This change might not affect you because your users have likely already upgraded their macOS devices. For a list of supported devices, see [macOS Ventura is compatible with these computers](https://support.apple.com/102861).

> [!NOTE]
> Devices that are currently enrolled on macOS 12.x or below will continue to remain enrolled even when those versions are no longer supported. New devices will be unable to enroll if they are running macOS 12.x or below.

#### How can you prepare?

Check your Intune reporting to see what devices or users might be affected. Go to **Devices** > **All devices** and filter by macOS. You can add more columns to help identify who in your organization has devices running macOS 12.x or earlier. Ask your users to upgrade their devices to a supported OS version.

### Plan for Change: Update to Intune endpoint for Remote Help 

Starting on May 30, 2024, or soon after, to improve the experience for Remote Help on Windows, Web, and macOS, we're updating the primary network endpoint for Remote Help from https://remoteassistance.support.services.microsoft.com to https://remotehelp.microsoft.com. 

#### How does this affect you or your users?

If you're using Remote Help and you have firewall rules that don't permit the new endpoint https://remotehelp.microsoft.com, admins and users may experience connectivity issues or disruptions with Remote Help.  

Additionally, the Remote Help app on Windows will need to be updated to the newest version. No action is needed for the Remote Help app for macOS and the Remote Help Web app.

#### How can you prepare?

Update your firewall rules to include the new Remote Help endpoint: https://remotehelp.microsoft.com. For Remote Help on Windows, users will need to update to the [newest version (5.1.124.0)](../fundamentals/remote-help-windows.md#march-13-2024). Most users have opted in for automatic updates and will be updated automatically without any action from the user. To learn more, review [Install and update Remote Help for Windows](../fundamentals/remote-help-windows.md#install-and-update-remote-help).

#### Additional information: 

- [Remote Help on Windows with Microsoft Intune](../fundamentals/remote-help-windows.md)
- [Network endpoints for Microsoft Intune | Microsoft Learn](../fundamentals/intune-endpoints.md#remote-help)

### Update to the latest Company Portal for Android, Intune App SDK for iOS, and Intune App Wrapper for iOS

Starting **June 1, 2024**, we're making updates to improve the Intune mobile application management (MAM) service. This update will require iOS wrapped apps, iOS SDK integrated apps, and the Company Portal for Android to be updated to the latest versions to ensure applications stay secure and run smoothly. 

> [!IMPORTANT]
> If you don't update to the latest versions, users will be blocked from launching your app.
>
> Ahead of this change, for Microsoft apps that need to be updated, when a user opens the app, they'll receive a blocking message to update the app.

Note that the way Android updates, once one Microsoft application with the updated SDK is on the device and the Company Portal is updated to the latest version, Android apps will update. So, this message is focused on iOS SDK/app wrapper updates. We recommend always updating your Android and iOS apps to the latest SDK or app wrapper to ensure that your app continues to run smoothly.  

#### How does this affect you or your users?
If your users haven't updated to the latest Microsoft or third-party app protection supported apps, they'll be blocked from launching their apps. If you have iOS line-of-business (LOB) applications that are using the Intune wrapper or Intune SDK, you must be on Wrapper/SDK version 17.7.0 or later to avoid your users being blocked.

#### How can you prepare?
Plan to make the changes below before **June 1, 2024**:

* Any of your iOS line-of-business (LOB) apps using older versions of the Intune SDK or wrapper must be updated to v17.7.0 or later.
  * For apps using the Intune iOS SDK, use [Release 19.2.0 · msintuneappsdk/ms-intune-app-sdk-ios (github.com)](https://github.com/msintuneappsdk/ms-intune-app-sdk-ios/releases/tag/19.2.0)
  * For apps using the Intune iOS wrapper, use [Release 19.2.0 · msintuneappsdk/intune-app-wrapping-tool-ios (github.com)](https://github.com/msintuneappsdk/intune-app-wrapping-tool-ios/releases/tag/19.2.0)
* For tenants with policies targeted to iOS apps: 
  * Notify your users that they need to upgrade to the latest version of the Microsoft apps. You can find the latest version of the apps in the [App store](https://www.apple.com/app-store/). For example, you can find the latest version of Microsoft Teams [here](https://apps.apple.com/app/microsoft-teams/id1113153706) and Microsoft Outlook [here](https://apps.apple.com/app/microsoft-outlook/id951937596).
  * Additionally, you have the option to enable the following [conditional launch](../apps/app-protection-policy-settings-ios.md#conditional-launch) settings:  
    * The **Min OS version** setting to warn users using iOS 15 or older so that they can download the latest apps. 
    * The **Min SDK version** setting to block users if the app is using Intune SDK for iOS older than 17.7.0. 
    * The **Min app version** setting to warn users on older Microsoft apps. Note that this setting must be in a policy targeted to only the targeted app. 
* For tenants with policies targeted to Android apps: 
  * Notify your users that they need to upgrade to the latest version (v5.0.6198.0) of the [Company Portal](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal) app.
  * Additionally, you have the option to enable the following [conditional launch](../apps/app-protection-policy-settings-ios.md#conditional-launch) device condition setting:  
    * The **Min Company Portal version** setting to warn users using a Company Portal app version older than 5.0.6198.0.

### Plan for Change: Ending support for Intune App SDK Xamarin Bindings in May 2024<!--27143739-->
With the [end of support for Xamarin Bindings](https://dotnet.microsoft.com/platform/support/policy/xamarin), Intune will end support for Xamarin apps and the Intune App SDK Xamarin Bindings beginning on **May 1, 2024**.

#### How does this affect you or your users?

If you you have iOS and/or Android apps built with Xamarin and are using the Intune App SDK Xamarin Bindings to enable app protection policies, upgrade your apps to .NET MAUI.  

#### How can you prepare?

Upgrade your Xamarin based apps to .NET MAUI. Review the following documentation for more information on Xamarin support and upgrading your apps: 

- [Xamarin Support Policy | .NET](https://dotnet.microsoft.com/platform/support/policy/xamarin)
- [Upgrade from Xamarin to .NET | Microsoft Lear](/dotnet/maui/migration/?view=net-maui-8.0)
- [Microsoft Intune App SDK for .NET MAUI – Android | NuGet Gallery](https://www.nuget.org/packages/Microsoft.Intune.Maui.Essentials.android)
- [Microsoft Intune App SDK for .NET MAUI – iOS | NuGet Gallery](https://www.nuget.org/packages/Microsoft.Intune.Maui.Essentials.iOS)

### Plan for Change: Update your PowerShell scripts with a Microsoft Entra ID registered app ID<!--26960016-->

Last year we announced a [new Microsoft Intune GitHub repository](https://aka.ms/Intune/Scripts-blog) based on the Microsoft Graph SDK-based PowerShell module. The legacy Microsoft Intune PowerShell sample scripts GitHub repository is now read-only. Additionally, in **May 2024**, due to updated authentication methods in the Graph SDK-based PowerShell module, the global Microsoft Intune PowerShell application (client) ID based authentication method will be removed.

#### How does this affect you or your users?

If you're using the Intune PowerShell application ID (d1ddf0e4-d672-4dae-b554-9d5bdfd93547), you'll need to update your scripts with a Microsoft Entra ID registered application ID to prevent your scripts from breaking.

#### How can you prepare?

Update your PowerShell scripts by:

1. Creating a new app registration in the Microsoft Entra admin center. For detailed instructions, read: [Quickstart: Register an application with the Microsoft identity platform](/entra/identity-platform/quickstart-register-app).
2. Update scripts containing the Intune application ID (d1ddf0e4-d672-4dae-b554-9d5bdfd93547) with the new application ID created in step 1.

For detailed step-by-step instructions visit [powershell-intune-samples/Updating App Registration (github.com)](https://github.com/microsoftgraph/powershell-intune-samples/blob/master/Updating%20App%20Registration).

### Intune moving to support Android 10 and later for user-based management methods in October 2024<!--14755802-->

In October 2024, Intune will be moving to support Android 10 and later for user-based management methods, which includes:
- Android Enterprise personally-owned work profile
- Android Enterprise corporate owned work profile
- Android Enterprise fully managed
- Android Open Source Project (AOSP) user-based
- Android device administrator
- App protection policies (APP)
- App configuration policies (ACP) for managed apps

Moving forward, we'll end support for one or two versions annually in October until we only support the latest four major versions of Android. You can learn more about this change by reading the blog: [Intune moving to support Android 10 and later for user-based management methods in October 2024](https://aka.ms/Intune/Android-10-support).

> [!NOTE]
> Userless methods of Android device management (Dedicated and AOSP userless) and Microsoft Teams certified Android devices won't be impacted by this change.

#### How does this affect you or your users?

For user-based management methods (as listed above), Android devices running Android 9 or earlier won't be supported. For devices on unsupported Android OS versions:

- Intune technical support won't be provided.
- Intune won't make changes to address bugs or issues.
- New and existing features aren't guaranteed to work. 

While Intune won't prevent enrollment or management of devices on unsupported Android OS versions, functionality isn't guaranteed, and use isn't recommended.

#### How can you prepare?

Notify your helpdesk, if applicable, about this updated support statement. The following admin options are available to help warn or block users:

- Configure a [conditional launch](../apps/app-protection-policy-settings-android.md#conditional-launch) setting for APP with a minimum OS version requirement to warn and/or block users.
- Use a device compliance policy and set the action for noncompliance to send a message to users before marking them as noncompliant.
- Set [enrollment restrictions](../fundamentals/manage-os-versions.md) to prevent enrollment on devices running older versions.

For more information, review: [Manage operating system versions with Microsoft Intune](../fundamentals/manage-os-versions.md).

### Plan for Change: Web based device enrollment will become default method for iOS/iPadOS device enrollment

Today, when creating iOS/iPadOS enrollment profiles, “Device enrollment with Company Portal” is shown as the default method. In an upcoming service release, the default method will change to “Web based device enrollment” during profile creation. Additionally for *new* tenants, if no enrollment profile is created, the user will enroll using web-based device enrollment.
 
> [!NOTE]
> For web enrollment, you will need to deploy the single sign-on (SSO) extension policy to enable just in time (JIT) registration, for more information review: [Set up just in time registration in Microsoft Intune](../enrollment/set-up-just-in-time-registration.md).

#### How does this affect you or your users?

This is an update to the user interface when creating new iOS/iPadOS enrollment profiles to display “Web based device enrollment” as the default method, existing profiles are not impacted. For *new* tenants, if no enrollment profile is created, the user will enroll using web-based device enrollment.

#### How can you prepare?

Update your documentation and user guidance as needed. If you currently use device enrollment with Company Portal, we recommend moving to web based device enrollment and deploying the SSO extension policy to enable JIT registration.

**Additional information:**

- [Set up just in time registration in Microsoft Intune](../enrollment/set-up-just-in-time-registration.md)
- [Set up web based device enrollment for iOS](../enrollment/web-based-device-enrollment-ios.md)

### Wrapped iOS apps and iOS apps using the Intune App SDK will require Azure AD app registration

We're making updates to improve the security of the Intune mobile application management (MAM) service. This update will require iOS wrapped apps and SDK integrated apps to be [registered with Microsoft Entra ID](/entra/identity-platform/quickstart-register-app) (formerly Azure Active Directory (Azure AD)) by March 31, 2024 to continue receiving MAM policy. 

#### How does this affect you or your users?

If you have wrapped apps or SDK integrated apps that aren't registered with Azure AD, these apps will be unable to connect to the MAM service to receive policy and your users won't be able to access apps that aren't registered.

#### How can you prepare?

Prior to this change, you will need to register the apps with Azure AD. See below for detailed instructions.

1. Register your apps with Azure AD by following these instructions: [Register an application with the Microsoft identity platform](/entra/identity-platform/quickstart-register-app).
1. Add the custom redirect URL to your app settings as documented [here](https://github.com/AzureAD/microsoft-authentication-library-for-objc#configuring-msal).
1. Give your app access to the Intune MAM service, for instructions see [here](../developer/app-sdk-get-started.md#give-your-app-access-to-the-intune-mobile-app-management-service).
1. Once the above changes are completed, configure your apps for Microsoft Authentication Library (MSAL):
   1. For wrapped apps: Add the Azure AD application client ID into the command-line parameters with the Intune App Wrapping Tool as outlined in the documentation: [Wrap iOS apps with the Intune App Wrapping Tool | Microsoft Learn](../developer/app-wrapper-prepare-ios.md#command-line-parameters) -ac and -ar are required parameters. Each app will need a unique set of these parameters. -aa is only required for single tenant applications.
   1. For SDK integrated apps see, [Microsoft Intune App SDK for iOS developer guide | Microsoft Learn](../developer/app-sdk-ios-phase2.md#configure-msal-settings-for-the-intune-app-sdk). ADALClientId and ADALRedirectUri/ADALRedirectScheme are now required parameters. ADALAuthority is only required for single tenant applications.
1. Deploy the app.
1. To validate the above steps:
   1. Target "com.microsoft.intune.mam.IntuneMAMOnly.RequireAADRegistration" application configuration policy and set it to Enabled - [Configuration policies for Intune App SDK managed apps - Microsoft Intune | Microsoft Learn](../apps/app-configuration-policies-managed-app.md)
   1. Target App Protection Policy to the application. Enable the ['Work or school account credentials for access' policy](../apps/app-protection-policy-settings-ios.md#access-requirements) and set 'Recheck the access requirements after (minutes of inactivity)' setting to a low number like 1.
1. Then launch the application on a device and verify if the sign-in (which should be required every minute on app launch) happens successfully with the configured parameters.
1. Note that if you only do step #6 and #7 before doing the other steps, you might be blocked on application launch. You will also notice the same behavior if some of the parameters are incorrect.
1. Once you’ve completed the validation steps, you can undo the changes made in step #6.
> [!NOTE]
> Intune will soon require an Azure AD device registration for iOS devices using MAM. If you have Conditional Access policies enabled, your devices should already be registered, and you won't notice any change. For more information see, [Microsoft Entra registered devices - Microsoft Entra | Microsoft Learn](/entra/identity/devices/concept-device-registration).

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

### Plan for Change: Intune ending support for Android device administrator on devices with GMS access in December 2024

[Google has deprecated](https://blog.google/products/android-enterprise/da-migration/) Android device administrator management, continues to remove management capabilities, and no longer provides fixes or improvements. Due to these changes, Intune will be ending support for Android device administrator management on devices with access to Google Mobile Services (GMS) beginning **December 31, 2024**. Until that time, we support device administrator management on devices running Android 14 and earlier. For more details, read the blog: [Microsoft Intune ending support for Android device administrator on devices with GMS access](https://aka.ms/Intune-Android-DA-blog).

#### How does this affect you or your users?

After Intune ends support for Android device administrator, devices with access to GMS will be impacted in the following ways:   

1. Users won't be able to enroll devices with Android device administrator.  
2. Intune won't make changes or updates to Android device administrator management, such as bug fixes, security fixes, or fixes to address changes in new Android versions.  
3. Intune technical support will no longer support these devices.

#### How can you prepare?

Stop enrolling devices into Android device administrator and migrate impacted devices to other management methods. You can check your Intune reporting to see which devices or users might be affected. Go to **Devices** > **All devices** and filter the OS column to **Android (device administrator)** to see the list of devices. 

Read the blog, [Microsoft Intune ending support for Android device administrator on devices with GMS access](https://aka.ms/Intune-Android-DA-blog), for our recommended alternative Android device management methods and information about the impact to devices without access to GMS.

### Plan for Change: Ending support for Microsoft Store for Business and Education apps

In April 2023, we began ending support for the Microsoft Store for Business experience in Intune. This occurs in several stages. For more information, see: [Adding your Microsoft Store for Business and Education apps to the Microsoft Store in Intune](https://aka.ms/Intune/MSfB-support)

### How does this affect you or your users?

If you're using Microsoft Store for Business and Education apps:

1. On April 30, 2023, Intune will disconnect Microsoft Store for Business services. Microsoft Store for Business and Education apps won't be able to sync with Intune and the connector page will be removed from the Intune admin center.
2. On June 15, 2023, Intune will stop enforcing online and offline Microsoft Store for Business and Education apps on devices. Downloaded applications remain on the device with limited support. Users might still be able to access the app from their device, but the app won't be managed. Existing synced Intune app objects remain to allow admins to view the apps that had been synced and their assignments. Additionally, you'll not be able to sync apps via the Microsoft Graph API syncMicrosoftStoreForBusinessApps and related API properties will display stale data.
3. On September 15, 2023, Microsoft Store for Business and Education apps will be removed from the Intune admin center. Apps on the device remain until intentionally removed. The Microsoft Graph API microsoftStoreForBusinessApp will no longer be available about a month later.

The retirement of Microsoft Store for Business and Education was [announced in 2021](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/evolving-the-microsoft-store-for-business-and-education/ba-p/2569423). When the Microsoft Store for Business and Education portals are retired, admins will no longer be able to manage the list of Microsoft Store for Business and Education apps that are synced or download offline content from the Microsoft Store for Business and Education portals.

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
