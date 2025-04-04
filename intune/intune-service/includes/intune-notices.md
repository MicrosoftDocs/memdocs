---
title: include file
description: include file
author: dougeby  
ms.service: microsoft-intune
ms.topic: include
ms.date: 4/1/2025
ms.author: dougeby
manager: dougeby
ms.custom: include file
---

These notices provide important information that can help you prepare for future Intune changes and features.

### Plan for Change: New Intune connector for deploying Microsoft Entra hybrid joined devices using Windows Autopilot

As part of Microsoft’s Secure Future Initiative, we recently released an update to the Intune Connector for Active Directory to use a Managed Service Account instead of a local SYSTEM account for deploying Microsoft Entra hybrid joined devices with Windows Autopilot. The new connector aims to enhance security by reducing unnecessary privileges and permissions associated with the local SYSTEM account.
 
> [!IMPORTANT]
> In late May 2025, we'll remove the old connector which uses the local SYSTEM account. At that point, we will stop accepting enrollments from the old connector. For more details, refer to the blog: [Microsoft Intune Connector for Active Directory security update](https://aka.ms/Intune-connector-blog)

#### How does this change affect you or your users?

If you have Microsoft Entra hybrid joined devices using Windows Autopilot, you need to transition to the new connector to continue deploying and managing devices effectively. If you don't update to the new connector, you won't be able to enroll new devices using the old connector.

#### How can you prepare?

Update your environment to the new connector by following these steps:

1. Download and install the new connector in the Intune admin center.
2. Sign in to set up the Managed Service Account (MSA).
3. Update the ODJConnectorEnrollmentWizard.exe.config file to include the required Organizational Units (OUs) for domain join.

For more detailed instructions, review: [Microsoft Intune Connector for Active Directory security update](https://aka.ms/Intune-connector-blog) and [Deploy Microsoft Entra hybrid joined devices by using Intune and Windows Autopilot](../../autopilot/windows-autopilot-hybrid.md).

### Update network endpoints for Windows, Mac and Android AOSP managed devices
Intune has updated the required CDN endpoints for Windows, Mac and Android Open Source Project (AOSP). If you have configured your firewall to allow *.manage.microsoft.com then no action is required, otherwise, we recommend you review and update your proxy settings by **April 30, 2025**.

#### How does this change affect you or your users?

If you're using Intune to deploy applications and scripts, you'll need to grant access to the updated endpoints for your location. If access to the new endpoints is not granted, users won't be able to install applications or scripts, and certain functionalities may fail. The CDN endpoints are used in the following scenarios:

- Windows: The CDN is used for delivering updates to the Intune management extension which enables scenarios such as Win32 app deployment, PowerShell scripts, Endpoint analytics, and more.
- Co-managed devices: The CDN providers the official Configuration Manager binaries, including the main technical preview and official releases, hotfixes, push notifications, and more.
- Mac: The CDN is used for delivering updates to the Intune management agent which is used to deploy macOS PKG apps, DMG apps, shell scripts, and custom attributes.
- Android AOSP: The CDN is used for delivering applications during device provisioning, such as the Intune Company Portal app, and feature updates.

#### How can you prepare?

Update your firewall rules to include the new CDN endpoints. For the best experience, we recommend using the *.manage.microsoft.com domain. If your proxy or firewall doesn't allow you to create a firewall rule using a domain, update the address as listed: 

- Windows CDN requirements: [Network requirements for PowerShell scripts and Win32 apps](../fundamentals/intune-endpoints.md#network-requirements-for-powershell-scripts-and-win32-apps)
- Configuration Manager co-managed devices CDN requirements: [Updates and servicing](../../configmgr/core/plan-design/network/internet-endpoints.md#updates-and-servicing)
- Mac CDN requirements: [Network requirements for macOS app and script deployments](../fundamentals/intune-endpoints.md#network-requirements-for-macos-app-and-script-deployments)
- Android AOSP CDN requirements: [Android AOSP dependencies](../fundamentals/intune-endpoints.md#android-aosp-dependencies)

### Plan for Change: New settings for Apple AI features; Genmojis, Writing tools, Screen capture

Today, the Apple AI features for Genmojis, Writing tools, and screen capture are blocked when the app protection policy (APP) "Send Org data to other apps" setting is configured to a value other than "All apps". For more details on the current configuration, app requirements, and the list of current Apple AI controls review the blog: [Microsoft Intune support for Apple Intelligence](https://techcommunity.microsoft.com/blog/intunecustomersuccess/microsoft-intune-support-for-apple-intelligence/4254037)

Expected with Intune’s April (2504) service release, Intune app protection policies have new standalone settings for blocking screen capture, Genmojis, and Writing tools. These standalone settings are supported by apps that have updated to version 19.7.12 or later for Xcode 15 and 20.4.0 or later for Xcode 16 of the Intune App SDK and App Wrapping Tool.

#### How does this change affect you or your users?

If you configured the APP "Send Org data to other apps" setting to a value other than "All apps", then the new "Genmoji", "Writing Tools" and "Screen capture" settings are set to **Block** in your app protection policy to prevent changes to your current user experience.

> [!NOTE]
> If you configured an app configuration policy (ACP) to allow for screen capture, it overrides the APP setting. We recommend updating the new APP setting to **Allow** and removing the ACP setting. For more information about the screen capture control, review [iOS/iPadOS app protection policy settings | Microsoft Learn](../apps/app-protection-policy-settings-ios.md#data-protection).
#### How can you prepare?

Review and update your app protection policies if you'd like more granular controls for blocking or allowing specific AI features. (**Apps** > **Protection** > *select a policy* > **Properties** > **Basics** > **Apps** > **Data protection**)

### Plan for change: User alerts on iOS for when screen capture actions are blocked

In an upcoming version (20.3.0) of the Intune App SDK and Intune App Wrapping Tool for iOS, support is added to alert users when a screen capture action (including recording and mirroring) is detected in a managed app. The alert is only visible to users if you have configured an app protection policy (APP) to block screen capture.

#### How does this change affect you or your users?

If APP has been configured to block screen capturing, users see an alert indicating that screen capture actions are blocked by their organization when they attempt to screenshot, screen record, or screen mirror.

For apps that have updated to the latest Intune App SDK or Intune App Wrapping Tool versions, screen capture is blocked if you configured "Send Org data to other apps" to a value other than "All apps". To allow screen capture for your iOS/iPadOS devices, configure the Managed apps app configuration policy setting "com.microsoft.intune.mam.screencapturecontrol" to **Disabled**.

#### How can you prepare?

Update your IT admin documentation and notify your helpdesk or users as needed. You can learn more about blocking screen capture in the blog: [New block screen capture for iOS/iPadOS MAM protected apps](https://aka.ms/Intune/iOS-screen-capture)

### Move to new Microsoft Graph Beta API properties for Windows Autopilot self-deploying mode and pre-provisioning

In late February 2025, a select number of old Microsoft Graph Beta API [windowsAutopilotDeploymentProfile](/graph/api/resources/intune-shared-windowsautopilotdeploymentprofile) properties used for Windows Autopilot self-deploying mode and pre-provisioning are removed and stop working. The same data can be found using newer Graph API properties.

#### How does this change affect you or your users?

If you have automation or scripts using the following Windows Autopilot properties, you must update to the new properties to prevent them from breaking.

| Old | New |
| -------- | ------- |
| enableWhiteglove | preprovisioningAllowed |
| extractHardwareHash | hardwareHashExtractionEnabled |
| language | Locale |
| outOfBoxExperienceSettings | outOfBoxExperienceSetting |
| outOfBoxExperienceSettings.HidePrivacySettings | outOfBoxExperienceSetting.PrivacySettingsHidden |
| outOfBoxExperienceSettings.HideEULA | outOfBoxExperienceSetting.EULAHidden |
| outOfBoxExperienceSettings.SkipKeyboardSelectionPage | outOfBoxExperienceSettings.KeyboardSelectionPageSkipped |
| outOfBoxExperienceSettings.HideEscapeLink | outOfBoxExperienceSettings.EscapeLinkHidden |

#### How can you prepare?

Update your automation or scripts to use the new Graph API properties to avoid deployment issues.

**Additional information:**

- [windowsAutopilotDeploymentProfile resource type - Microsoft Graph Beta | Microsoft Learn](/graph/api/resources/intune-shared-windowsautopilotdeploymentprofile)
- [azureADWindowsAutopilotDeploymentProfile resource type - Microsoft Graph Beta | Microsoft Learn](/graph/api/resources/intune-enrollment-azureadwindowsautopilotdeploymentprofile)
- [outOfBoxExperienceSettings resource type - Microsoft Graph Beta | Microsoft Learn](/graph/api/resources/intune-enrollment-outofboxexperiencesettings)

### Plan for Change: Blocking screen capture in the latest Intune App SDK for iOS and Intune App Wrapping Tool for iOS 

We recently released updated versions of the Intune App SDK and the Intune App Wrapping Tool. Included in these releases (v19.7.5+ for Xcode 15 and v20.2.0+ for Xcode 16) is the support for blocking screen capture, Genmojis, and writing tools in response to the new AI features in iOS/iPadOS 18.2.

#### How does this change affect you or your users?

For apps that have updated to the latest Intune App SDK or Intune App Wrapping Tool versions screen capture will be blocked if you configured "Send Org data to other apps" to a value other than "All apps". To allow screen capture for your iOS/iPadOS devices, configure the [Managed apps app configuration policy](../apps/app-configuration-policies-managed-app.md) setting "com.microsoft.intune.mam.screencapturecontrol" to **Disabled**.

#### How can you prepare?

Review your app protection policies and if needed, create a [Managed apps app configuration policy](../apps/app-configuration-policies-managed-app.md) to allow screen capture by configuring the above setting *(Apps > App configuration policies > Create > Managed apps > Step 3 ‘Settings’ under General configuration)*. For more information review, [iOS app protection policy settings – Data protection](../apps/app-protection-policy-settings-ios.md#data-protection) and [App configuration policies - Managed apps](../apps/app-configuration-policies-overview.md#managed-apps).

### Take Action: Update to the latest Intune App SDK for iOS and Intune App Wrapping Tool for iOS

To support the upcoming release of iOS/iPadOS 18.2, update to the latest versions of the Intune App SDK and the Intune App Wrapping Tool to ensure applications stay secure and run smoothly. **Important:** If you don't update to the latest versions, some app protection policies may not apply to your app in certain scenarios. Review the following GitHub announcements for more details on the specific impact:

- SDK for iOS: [Update recommended prior to iOS 18.2 general availability - microsoftconnect/ms-intune-app-sdk-ios - Discussion #495](https://github.com/microsoftconnect/ms-intune-app-sdk-ios/discussions/495) 
- Wrapper for iOS: [Update recommended prior to iOS 18.2 general availability - microsoftconnect/intune-app-wrapping-tool-ios - Discussion #128](https://github.com/microsoftconnect/intune-app-wrapping-tool-ios/discussions/128)

As a best practice, always update your iOS apps to the latest App SDK or App Wrapping Tool to ensure that your app continues to run smoothly.

#### How does this change affect you or your users?

If you have applications using the Intune App SDK or Intune App Wrapping Tool, you'll need to update to the latest version to support iOS 18.2.

#### How can you prepare?

For apps running on iOS 18.2, you must update to the new version of the Intune App SDK for iOS:
- [For apps built with XCode 15 use v19.7.6 - Release 19.7.6 - microsoftconnect/ms-intune-app-sdk-ios - GitHub](https://github.com/microsoftconnect/ms-intune-app-sdk-ios/releases/tag/19.7.6)
- [For apps built with XCode 16 use v20.2.1 - Release 20.2.1 - microsoftconnect/ms-intune-app-sdk-ios - GitHub](https://github.com/microsoftconnect/ms-intune-app-sdk-ios/releases/tag/20.2.1)

For apps running on iOS 18.2, you must update to the new version of the Intune App Wrapping Tool for iOS:
- [For apps built with XCode 15 use v19.7.6 - Release 19.7.6 - microsoftconnect/intune-app-wrapping-tool-ios - GitHub](https://github.com/microsoftconnect/intune-app-wrapping-tool-ios/releases/tag/19.7.6)
- [For apps built with XCode 16 use v20.2.1 - Release 20.2.1 - microsoftconnect/intune-app-wrapping-tool-ios - GitHub](https://github.com/microsoftconnect/intune-app-wrapping-tool-ios/releases/tag/20.2.1)

> [!IMPORTANT]
>
> The listed SDK releases support blocking screen capture, Genmojis, and writing tools in response to new AI features in iOS 18.2. For apps that have updated to these SDK versions, screen capture block is applied if you have configured *Send Org data to other apps* to a value other than *All apps*. See [iOS/iPadOS app protection policy settings](../apps/app-protection-policy-settings-ios.md#data-protection) for more info. You can configure app configuration policy setting **com.microsoft.intune.mam.screencapturecontrol = Disabled** if you wish to allow screen capture for your iOS devices. See [App configuration policies for Microsoft Intune](../apps/app-configuration-policies-overview.md#managed-apps) for more info. Intune will be providing more granular controls for blocking specific AI features in the future. Follow [What's new in Microsoft Intune](../fundamentals/whats-new.md) to stay up to date.
>
> Notify your users as applicable, to ensure they upgrade their apps to the latest version prior to upgrading to iOS 18.2. You can review the Intune App SDK version in use by your users in the Microsoft Intune admin center by navigating to **Apps** > **Monitor** > **App protection status**, then review *Platform version* and *iOS SDK version*.
>
> If you have questions, leave a comment on the applicable GitHub announcement. Additionally, if you haven't already, navigate to the applicable GitHub repository and subscribe to *Releases* and *Discussions* (Watch > Custom > select Releases, Discussions) to ensure you stay up-to-date with the latest SDK releases, updates, and other important announcements.

### Plan for Change: Specific app configuration values will be automatically sent to specific apps

Starting with Intune's September (2409) service release, the **IntuneMAMUPN**, **IntuneMAMOID**, and **IntuneMAMDeviceID** app configuration values will be automatically sent to managed applications on Intune enrolled iOS devices for the following apps: Microsoft Excel, Microsoft Outlook, Microsoft PowerPoint, Microsoft Teams and Microsoft Word. Intune will continue to expand this list to include additional managed apps.

#### How does this change affect you or your users?

If these values aren't configured correctly for iOS devices, there's a possibility of either the policy not getting delivered to the app or the wrong policy is delivered. For more information, see [Support tip: Intune MAM users on iOS/iPadOS userless devices may be blocked in rare cases](https://techcommunity.microsoft.com/blog/intunecustomersuccess/support-tip-intune-mam-users-on-iosipados-userless-devices-may-be-blocked-in-rar/4254335).

#### How can you prepare?

No additional action is needed.

### Plan for Change: Implement strong mapping for SCEP and PKCS certificates

With the May 10, 2022, Windows update ([KB5014754](https://support.microsoft.com/topic/kb5014754-certificate-based-authentication-changes-on-windows-domain-controllers-ad2c23b0-15d8-4340-a468-4d4f3b188f16)), changes were made to the Active Directory Kerberos Key Distribution (KDC) behavior in Windows Server 2008 and later versions to mitigate elevation of privilege vulnerabilities associated with certificate spoofing. Windows enforces these changes on **February 11, 2025**.
 
To prepare for this change, Intune has released the ability to include the security identifier to strongly map SCEP and PKCS certificates. For more information, review the blog: [Support tip: Implementing strong mapping in Microsoft Intune certificates](https://techcommunity.microsoft.com/blog/intunecustomersuccess/support-tip-implementing-strong-mapping-in-microsoft-intune-certificates/4053376).

#### How does this change affect you or your users?

These changes will impact SCEP and PKCS certificates delivered by Intune for Microsoft Entra hybrid joined users or devices. If a certificate can't be strongly mapped, authentication will be denied. To enable strong mapping:

- SCEP certificates: Add the security identifier to your SCEP profile. We strongly recommend testing with a small group of devices and then slowly rollout updated certificates to minimize disruptions to your users.
- PKCS certificates: Update to the latest version of the Certificate Connector, change the registry key to enable the security identifier, and then restart the connector service. **Important:** Before you modify the registry key, review how to change the registry key and how to back up and restore the registry.

For detailed steps and additional guidance, review the blog: [Support tip: Implementing strong mapping in Microsoft Intune certificates](https://techcommunity.microsoft.com/blog/intunecustomersuccess/support-tip-implementing-strong-mapping-in-microsoft-intune-certificates/4053376)

#### How can you prepare?

If you use SCEP or PKCS certificates for Microsoft Entra Hybrid joined users or devices, you'll need to take action before February 11, 2025 to either:

- **(Recommended)** Enable strong mapping by reviewing the steps described in the blog: [Support tip: Implementing strong mapping in Microsoft Intune certificates](https://techcommunity.microsoft.com/blog/intunecustomersuccess/support-tip-implementing-strong-mapping-in-microsoft-intune-certificates/4053376)
- Alternatively, if all certificates can't be renewed before February 11, 2025, with the SID included, enable Compatibility mode by adjusting the registry settings as described in [KB5014754](https://support.microsoft.com/topic/kb5014754-certificate-based-authentication-changes-on-windows-domain-controllers-ad2c23b0-15d8-4340-a468-4d4f3b188f16). Compatibility mode is valid until September 2025.

### Update to the latest Intune App SDK and Intune App Wrapper for Android 15 support

We've recently released new versions of the Intune App SDK and Intune App Wrapping Tool for Android to support Android 15. We recommend upgrading your app to the latest SDK or wrapper versions to ensure applications stay secure and run smoothly.
 
#### How does this change affect you or your users?

If you have applications using the Intune App SDK or Intune App Wrapping Tool for Android, it's recommended that you update your app to the latest version to support Android 15.
 
#### How can you prepare?

If you choose to build apps targeting Android API 35, you need to adopt the new version of the Intune App SDK for Android (v11.0.0). If you wrapped your app and are targeting API 35 you need to use the new version of the App wrapper (v1.0.4549.6).

> [!NOTE]
> As a reminder, while apps must update to the latest SDK if targeting Android 15, apps don't need to update the SDK to run on Android 15.

You should also plan to update your documentation or developer guidance if applicable to include this change in support for the SDK.

Here are the public repositories:
- [Intune App SDK for Android](https://github.com/microsoftconnect/ms-intune-app-sdk-android)
- [Intune App Wrapping Tool for Android](https://github.com/microsoftconnect/intune-app-wrapping-tool-android)

### Plan for Change: Intune is moving to support iOS/iPadOS 16 and later<!--28391935-->

Later in calendar year 2024, we expect iOS 18 and iPadOS 18 to be released by Apple. Microsoft Intune, including the Intune Company Portal and Intune app protection policies (APP, also known as MAM), requires [iOS 16/iPadOS 16 and higher](../fundamentals/supported-devices-browsers.md) shortly after the iOS/iPadOS 18 release.

#### How does this change affect you or your users?

If you're managing iOS/iPadOS devices, you might have devices that won't be able to upgrade to the minimum supported version (iOS 16/iPadOS 16).

Given that Microsoft 365 mobile apps are supported on iOS 16/iPadOS 16 and higher, this change may not affect you. You likely already upgraded your OS or devices.

To check which devices support iOS 16 or iPadOS 16 (if applicable), see the following Apple documentation:

- [Supported iPhone models](https://support.apple.com/guide/iphone/supported-models-iphe3fa5df43/16.0/ios/16.0)
- [Supported iPad models](https://support.apple.com/guide/ipad/supported-models-ipad213a25b2/16.0/ipados/16.0)

> [!NOTE]
> Userless iOS and iPadOS devices enrolled through Automated Device Enrollment (ADE) have a slightly nuanced support statement due to their shared usage. The minimum supported OS version changes to iOS 16/iPadOS 16 while the allowed OS version changes to iOS 13/iPadOS 13 and later. See [this statement about ADE Userless support](https://aka.ms/ADE_userless_support) for more information.

#### How can you prepare?

Check your Intune reporting to see what devices or users might be affected. For devices with mobile device management (MDM), go to **Devices** > **All devices** and filter by OS. For devices with app protection policies, go to **Apps** > **Monitor** > **App protection status** and use the *Platform* and *Platform version* columns to filter.

To manage the supported OS version in your organization, you can use Microsoft Intune controls for both MDM and APP. For more information, see [Manage operating system versions with Intune](../fundamentals/manage-os-versions.md).

### Plan for change: Intune is moving to support macOS 13 and higher later this year<!--28391869-->

Later in calendar year 2024, we expect macOS 15 Sequoia to be released by Apple. Microsoft Intune, the Company Portal app, and the Intune mobile device management agent support macOS 13 and later. Since the Company Portal app for iOS and macOS are a unified app, this change will occur shortly after the release of macOS 15. This doesn't affect existing enrolled devices.

#### How does this change affect you or your users?

This change only affects you if you currently manage, or plan to manage, macOS devices with Intune. This change might not affect you because your users have likely already upgraded their macOS devices. For a list of supported devices, see [macOS Ventura is compatible with these computers](https://support.apple.com/102861).

> [!NOTE]
> Devices that are currently enrolled on macOS 12.x or below will continue to remain enrolled even when those versions are no longer supported. New devices are unable to enroll if they're running macOS 12.x or below.

#### How can you prepare?

Check your Intune reporting to see what devices or users might be affected. Go to **Devices** > **All devices** and filter by macOS. You can add more columns to help identify who in your organization has devices running macOS 12.x or earlier. Ask your users to upgrade their devices to a supported OS version.

### Intune moving to support Android 10 and later for user-based management methods in October 2024<!--14755802-->

In October 2024, Intune supports Android 10 and later for user-based management methods, which includes:

- Android Enterprise personally owned work profile
- Android Enterprise corporate owned work profile
- Android Enterprise fully managed
- Android Open Source Project (AOSP) user-based
- Android device administrator
- App protection policies (APP)
- App configuration policies (ACP) for managed apps

Moving forward, we'll end support for one or two versions annually in October until we only support the latest four major versions of Android. You can learn more about this change by reading the blog: [Intune moving to support Android 10 and later for user-based management methods in October 2024](https://aka.ms/Intune/Android-10-support).

> [!NOTE]
> Userless methods of Android device management (Dedicated and AOSP userless) and Microsoft Teams certified Android devices won't be impacted by this change.

#### How does this change affect you or your users?

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

Today, when creating iOS/iPadOS enrollment profiles, "Device enrollment with Company Portal" is shown as the default method. In an upcoming service release, the default method will change to "Web based device enrollment" during profile creation. Additionally for *new* tenants, if no enrollment profile is created, the user will enroll using web-based device enrollment.

> [!NOTE]
> For web enrollment, you need to deploy the single sign-on (SSO) extension policy to enable just in time (JIT) registration, for more information review: [Set up just in time registration in Microsoft Intune](../enrollment/set-up-just-in-time-registration.md).

#### How does this change affect you or your users?

This is an update to the user interface when creating new iOS/iPadOS enrollment profiles to display "Web based device enrollment" as the default method, existing profiles aren't impacted. For *new* tenants, if no enrollment profile is created, the user will enroll using web-based device enrollment.

#### How can you prepare?

Update your documentation and user guidance as needed. If you currently use device enrollment with Company Portal, we recommend moving to web based device enrollment and deploying the SSO extension policy to enable JIT registration.

**Additional information:**

- [Set up just in time registration in Microsoft Intune](../enrollment/set-up-just-in-time-registration.md)
- [Set up web based device enrollment for iOS](../enrollment/web-based-device-enrollment-ios.md)

### Plan for Change: Intune ending support for Android device administrator on devices with GMS access in December 2024

[Google has deprecated](https://blog.google/products/android-enterprise/da-migration/) Android device administrator management, continues to remove management capabilities, and no longer provides fixes or improvements. Due to these changes, Intune will be ending support for Android device administrator management on devices with access to Google Mobile Services (GMS) beginning **December 31, 2024**. Until that time, we support device administrator management on devices running Android 14 and earlier. For more details, read the blog: [Microsoft Intune ending support for Android device administrator on devices with GMS access](https://aka.ms/Intune-Android-DA-blog).

#### How does this change affect you or your users?

After Intune ends support for Android device administrator, devices with access to GMS will be impacted in the following ways:

1. Intune won't make changes or updates to Android device administrator management, such as bug fixes, security fixes, or fixes to address changes in new Android versions.
2. Intune technical support will no longer support these devices.

#### How can you prepare?

Stop enrolling devices into Android device administrator and migrate impacted devices to other management methods. You can check your Intune reporting to see which devices or users might be affected. Go to **Devices** > **All devices** and filter the OS column to **Android (device administrator)** to see the list of devices.

Read the blog, [Microsoft Intune ending support for Android device administrator on devices with GMS access](https://aka.ms/Intune-Android-DA-blog), for our recommended alternative Android device management methods and information about the impact to devices without access to GMS.
