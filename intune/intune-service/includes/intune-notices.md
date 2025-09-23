---
title: include file
description: include file
author: dougeby  
ms.service: microsoft-intune
ms.topic: include
ms.date: 4/8/2025
ms.author: dougeby
manager: dougeby
ms.custom: include file
---

These notices provide important information that can help you prepare for future Intune changes and features.

### Update firewall configurations to include new Intune network endpoints

As part of Microsoft’s ongoing [Secure Future Initiative (SFI)](https://www.microsoft.com/trust-center/security/secure-future-initiative), starting on or shortly after **December 2, 2025**, the network service endpoints for Microsoft Intune  will also use the Azure Front Door IP addresses. This improvement supports better alignment with modern security practices and over time will make it easier for organizations using multiple Microsoft products to manage and maintain their firewall configurations. As a result, customers may be required to add these network (firewall) configurations in third-party applications to enable proper function of Intune device and app management. This change will affect customers using a firewall allowlist that allows outbound traffic based on IP addresses or Azure service tags.

Don't remove any existing network endpoints required for Microsoft Intune. Additional network endpoints are documented as part of the Azure Front Door and service tags information referenced in the files linked below:

- Public clouds: Download Azure IP Ranges and Service Tags – [Public Cloud from Official Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=56519)
- Government clouds: Download Azure IP Ranges and Service Tags – [US Government Cloud from Official Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=57063)

The additional ranges are those listed in the JSON files linked above and can be found by searching for “AzureFrontDoor.MicrosoftSecurity”.

#### How does this change affect you or your users?

If you've configured an outbound traffic policy for Intune IP address ranges or Azure service tags for your firewalls, routers, proxy servers, client-based firewalls, VPN or network security groups, you'll need to update them to include the new Azure Front Door ranges with the “AzureFrontDoor.MicrosoftSecurity” tag. 

Intune requires internet access for devices under Intune management, whether for mobile device management or mobile application management. If your outbound traffic policy doesn’t include the new Azure Front Door IP address ranges, users may face login issues, devices might lose connectivity with Intune, and access to apps like the Intune Company Portal or those protected by app protection policies could be disrupted.

#### How can you prepare?

Ensure that your firewall rules are updated and added to your firewall’s allowlist with the additional IP addresses documented under Azure Front Door by **December 2, 2025**. 

Alternatively, you may add the service tag “AzureFrontDoor.MicrosoftSecurity” to your firewall rules to allow outbound traffic on port 443 for the addresses in the tag. 

If you aren't the IT admin who can make this change, notify your networking team. If you're responsible for configuring internet traffic, refer to the following documentation for more details:

- [Azure Front Door](/azure/frontdoor/origin-security?tabs=app-service-functions&pivots=front-door-classic)
- [Azure service tags](/azure/virtual-network/service-tags-overview)
- [Intune network endpoints](../fundamentals/intune-endpoints.md#intune-core-service)
- [US government network endpoints for Intune](../fundamentals/intune-us-government-endpoints.md)

If you have a helpdesk, inform them about this upcoming change.

### Update to support statement for Windows 10 in Intune

Windows 10 will reach end of support on **October 14, 2025**. After this date, Windows 10 will no longer receive quality or feature updates. Security updates will only be available to commercial customers who have enrolled devices into the Extended Security Updates (ESU) program. For more details, review the additional information shared below.

#### How does this change affect you or your users?

After Windows 10 reaches the end of support, Microsoft Intune will continue to maintain core management functionality for Windows 10. This ensures:

- Continuity of device management.
- Support for updates and migration workflows to Windows 11.
- Ability for ESU customers to deploy Windows security updates and maintain secure patch levels.

Following Windows 10 end of support, the final release of Windows 10 (version 22H2) will be designated as an “allowed” version in Intune. While updates and new features are not available, devices running this version can still enroll in Intune and use eligible features, but functionality is not guaranteed and may vary.

#### How can you prepare?
Use the **All devices** report in the Intune admin center to identify devices still running Windows 10 and upgrade eligible devices to Windows 11.

If devices cannot be upgraded in time, consider enrolling eligible devices in the Windows 10 ESU program to continue receiving critical security updates.


#### Additional information:

- [Stay secure with Windows 11, Copilot+ PCs and Windows 365 before support ends for Windows 10](https://blogs.windows.com/windowsexperience/2025/06/24/stay-secure-with-windows-11-copilot-pcs-and-windows-365-before-support-ends-for-windows-10/)
- [Windows 10 reaching end of support](/lifecycle/announcements/windows-10-end-of-support)
- [Enable Extended Security Updates (ESU)](/windows/whats-new/enable-extended-security-updates)
- [Windows 10 release information](/windows/release-health/release-information)
- [Windows 11 release information](/windows/release-health/windows11-release-information)
- [Lifecycle FAQ - Windows](/lifecycle/faq/windows)

### Update to the latest Intune App SDK and Intune App Wrapping Tool  for iOS and register your app with Microsoft Entra

To support the upcoming release of iOS/iPadOS 26 and ensure continued app protection policy (APP, also known as MAM) enforcement, update to the latest versions of the Intune App SDK and the Intune App Wrapping Tool to ensure applications stay secure and run smoothly. **Important:** If you don't update to the latest versions, some app protection policies may not apply to your app in certain scenarios.

> [!NOTE]
> Updating to SDK v21.0.0 or later requires your app to be registered with Microsoft Entra. Review the following GitHub announcements for more details on the specific impact:
> - SDK for iOS: [App Registration Requirement Will be Enforced in Version 21.0.0+ | microsoftconnect/ms-intune-app-sdk-ios - Discussion #569](https://github.com/microsoftconnect/ms-intune-app-sdk-ios/discussions/569)
> - Wrapper for iOS: [-ac and -ar parameters will become required in version 21.0.0 | microsoftconnect/intune-app-wrapping-tool-ios - Discussion #136](https://github.com/microsoftconnect/intune-app-wrapping-tool-ios/discussions/136)
> 
> If you have questions or concerns, file an issue in the GitHub repository or reply directly to the GitHub announcement. 

As a best practice, always update your iOS/iPadOS apps to the latest App SDK or App Wrapping Tool to ensure that your app continues to run smoothly.

#### How does this change affect you or your users?

If you have applications using the Intune App SDK or Intune App Wrapping Tool, update to the latest version to support iOS/iPadOS 26. Updating to v21.0.0 or later requires that apps must be registered with Microsoft Entra. While it was previously possible for apps to enable Intune MAM without full Microsoft Entra configuration, this won't be supported starting with SDK 21.0.0. Apps that aren't properly registered may fail to function or receive app protection policies. 

#### How can you prepare?

- For apps running on iOS 26, update to the new version of the Intune App SDK for iOS: [Releases - microsoftconnect/ms-intune-app-sdk-ios](https://github.com/microsoftconnect/ms-intune-app-sdk-ios/releases)
    - For apps built with XCode 16 use the latest v20.x release.
    - For apps built with XCode 26 use v21.0.0 or later, which is expected to release in September 2025.
- For apps running on iOS 26, update to the new version of the Intune App Wrapping Tool for iOS: [Releases - microsoftconnect/intune-app-wrapping-tool-ios](https://github.com/microsoftconnect/intune-app-wrapping-tool-ios/releases)
    - For apps built with XCode 16 use the latest v20.x release.
    - For apps built with XCode 26 use v21.0.0 or later which is expected to release in September 2025.
- Ensure your apps are registered in Microsoft Entra. For more details refer to: [How to register an app in Microsoft Entra ID](/entra/identity-platform/quickstart-register-app)

Notify your users as applicable, to ensure they upgrade their apps to the latest version prior to upgrading to iOS 26. You can review the Intune App SDK version in use by your users in the Microsoft Intune admin center by navigating to **Apps** > **Monitor** > **App protection status**, then review “Platform version” and “iOS SDK version”.  

### Plan for Change: Intune is moving to support iOS/iPadOS 17 and later

Later in calendar year 2025, we expect iOS 26 and iPadOS 26 to be released by Apple. Microsoft Intune, including the Intune Company Portal and Intune app protection policies (APP, also known as MAM), requires [iOS 17/iPadOS 17 and higher](../fundamentals/supported-devices-browsers.md) shortly after the iOS/iPadOS 26 release.

#### How does this change affect you or your users?

If you're managing iOS/iPadOS devices, you might have devices that won't be able to upgrade to the minimum supported version (iOS 17/iPadOS 17).

Given that Microsoft 365 mobile apps are supported on iOS 17/iPadOS 17 and higher, this change may not affect you. You likely already upgraded your OS or devices.

To check which devices support iOS 17 or iPadOS 17 (if applicable), see the following Apple documentation:

- [Supported iPhone models](https://support.apple.com/guide/iphone/iphone-models-compatible-with-ios-17-iphe3fa5df43/17.0/ios/17.0)
- [Supported iPad models](https://support.apple.com/guide/ipad/ipad-models-compatible-with-ipados-17-ipad213a25b2/17.0/ipados/17.0)

> [!NOTE]
> Userless iOS and iPadOS devices enrolled through Automated Device Enrollment (ADE) have a slightly nuanced support statement due to their shared usage. The minimum supported OS version changes to iOS 17/iPadOS 17 while the allowed OS version changes to iOS 14/iPadOS 14 and later. See [this statement about ADE Userless support](https://aka.ms/ADE_userless_support) for more information.

#### How can you prepare?

Check your Intune reporting to see what devices or users might be affected. For devices with mobile device management (MDM), go to **Devices** > **All devices** and filter by OS. For devices with app protection policies, go to **Apps** > **Monitor** > **App protection status** and use the *Platform* and *Platform version* columns to filter.

To manage the supported OS version in your organization, you can use Microsoft Intune controls for both MDM and APP. For more information, refer to [Manage operating system versions with Intune](../fundamentals/manage-os-versions.md).

### Plan for change: Intune is moving to support macOS 14 and higher later this year

Later in calendar year 2025, we expect macOS Tahoe 26 to be released by Apple. Microsoft Intune, the Company Portal app, and the Intune mobile device management agent support macOS 14 and later. Since the Company Portal app for iOS and macOS are a unified app, this change will occur shortly after the release of macOS 26. This doesn't affect existing enrolled devices.

#### How does this change affect you or your users?

This change only affects you if you currently manage, or plan to manage, macOS devices with Intune. This change might not affect you because your users have likely already upgraded their macOS devices. For a list of supported devices, refer to [macOS Sonoma is compatible with these computers](https://support.apple.com/105113).

> [!NOTE]
> Devices that are currently enrolled on macOS 13.x or below will continue to remain enrolled even when those versions are no longer supported. New devices are unable to enroll if they're running macOS 13.x or below.

#### How can you prepare?

Check your Intune reporting to see what devices or users might be affected. Go to **Devices** > **All devices** and filter by macOS. You can add more columns to help identify who in your organization has devices running macOS 13.x or earlier. Ask your users to upgrade their devices to a supported OS version.

### Plan for Change: Google Play strong integrity definition update for Android 13 or above

Google recently updated the definition of "Strong Integrity" for devices running Android 13 or above, requiring hardware-backed security signals and recent security updates. For more information refer to the [Android Developers Blog: Making the Play Integrity API faster, more resilient, and more private](https://android-developers.googleblog.com/2024/12/making-play-integrity-api-faster-resilient-private.html). Microsoft Intune will enforce this change by **September 30, 2025**. Until then we've adjusted app protection policy and compliance policy behavior to align with Google’s recommended backward compatibility guidance to minimize disruption as detailed in [Improved verdicts in Android 13 and later devices | Google Play | Android Developers](https://developer.android.com/google/play/integrity/improvements#how_can_i_use_the_old_meets-strong-integrity_label_definition_across_all_android_sdk_versions).

#### How does this change affect you or your users?

If you have targeted users with app protection policies and/or compliance policies that are using devices running Android 13 or above without a security update in the past 12 months, these devices will no longer meet the "Strong Integrity" standard. 

**User Impact:** For users running devices on Android 13 or above after this change:
- Devices without the latest security updates may be downgraded from "Strong Integrity" to "Device Integrity" which could result in conditional launch blocks for affected devices.
- Devices without the latest security updates may see their devices become noncompliant in the Intune Company Portal app and could lose access to company resources based on your organization's Conditional Access policies.

Note that devices running Android versions 12 or below aren't affected by this change. 

#### How can you prepare?

Before September 30, 2025, review and update your policies as needed. Ensure users with devices running Android 13 or above are receiving timely security updates. You can use the [app protection status report](../apps/app-protection-policies-monitor.md#view-the-app-protection-status-report) to monitor the date of the last Android Security Patch received by the device and notify users to update as needed. The following admin options are available to help warn or block users:

- For app protection policies configure the **Min OS version** and **Min patch version** conditional launch settings. For more details, review [Android app protection policy settings in Microsoft Intune | Microsoft Learn](../apps/app-protection-policy-settings-android.md#conditional-launch)
- For compliance policies configure the **Minimum security patch level** compliance setting. For more details, review: [Device compliance settings for Android Enterprise in Intune](../protect/compliance-policy-create-android-for-work.md)

### Plan for Change: New Intune connector for deploying Microsoft Entra hybrid joined devices using Windows Autopilot

As part of Microsoft’s Secure Future Initiative, we recently released an update to the Intune Connector for Active Directory to use a Managed Service Account instead of a local SYSTEM account for deploying Microsoft Entra hybrid joined devices with Windows Autopilot. The new connector aims to enhance security by reducing unnecessary privileges and permissions associated with the local SYSTEM account.
 
> [!IMPORTANT]
> At the end of June 2025, we'll remove the old connector which uses the local SYSTEM account. At that point, we will stop accepting enrollments from the old connector. For more details, refer to the blog: [Microsoft Intune Connector for Active Directory security update](https://aka.ms/Intune-connector-blog)

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

In an upcoming release, Intune app protection policies have new standalone settings for blocking screen capture, Genmojis, and Writing tools. These standalone settings are supported by apps that have updated to version 19.7.12 or later for Xcode 15 and 20.4.0 or later for Xcode 16 of the Intune App SDK and App Wrapping Tool.

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

In late May 2025 (previously March), a select number of old Microsoft Graph Beta API [windowsAutopilotDeploymentProfile](/graph/api/resources/intune-shared-windowsautopilotdeploymentprofile) properties used for Windows Autopilot self-deploying mode and pre-provisioning are removed and stop working. The same data can be found using newer Graph API properties.

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

### Intune moving to support Android 10 and later for user-based management methods in October 2024<!--14755802-->

In October 2024, Intune supports Android 10 and later for user-based management methods, which includes:

- Android Enterprise personally owned work profile
- Android Enterprise corporate owned work profile
- Android Enterprise fully managed
- Android Open Source Project (AOSP) user-based
- Android device administrator
- App protection policies
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
