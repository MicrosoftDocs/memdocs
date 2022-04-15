---
title: include file
description: include file
author: ErikjeMS  
ms.service: microsoft-intune
ms.topic: include
ms.date: 04/15/2022
ms.author: erikje
ms.custom: include file
---

These notices provide important information that can help you prepare for future Intune changes and features.  

### Plan for Change: iOS/iPadOS notifications will require minimum version of the Company Portal<!-- 14131757 -->

We will be making service side updates to iOS/iPadOS notifications in Microsoft Intune's April (2205) service release that will require users to have updated to at least version 5.2202.0 of the iOS/iPadOS Company Portal (released in March 2022).

#### How does this affect you or your users?

There is no change in functionality for push notifications, however, users will need to update to the latest Company Portal version. Scenarios that send push notifications to the Company Portal include:

- [Custom notifications](../remote-actions/custom-notifications.md)
- [Push notifications for noncompliance](../protect/actions-for-noncompliance.md#available-actions-for-noncompliance)
- [Device ownership change push notifications](../apps/company-portal-app.md#device-ownership-notification)
- [Delivery of S/MIME certificates for iOS to access Outlook](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/smime-outlook-for-ios-and-android)
- [Derived credential enrollment](../protect/derived-credentials.md)

If users do not update the Company Portal app to version 5.2203.0 prior to this change, they will not receive messages sent by your organization and will instead receive a notification telling them to update their app. Once they update their app, push notifications will resume.

#### How can you prepare?  

The required version of the Company Portal has been released, so most users have likely [updated the app](../user-help/install-a-new-version-of-the-company-portal-app.md) and will not be impacted. However, you may want to notify users of this change to ensure all users continue to receive push notifications sent by your organization.

### Plan for change: Intune is moving to support Android 8.0 and later in January 2022<!-- 10946003 -->  

Microsoft Intune will be moving to support Android version 8.0 (Oreo) and later for mobile device management (MDM) enrolled devices on or shortly after January 7, 2022.  

#### How does this affect you or your users?

After January 7, 2022, MDM enrolled devices running Android version 7.x or earlier will no longer receive updates to the Android Company Portal or the Intune App. Enrolled devices will continue to have Intune policies applied but are no longer supported for any Intune scenarios. Company Portal and the Intune App will not be available for devices running Android 7.x and lower beginning mid-February; however, these devices will not be blocked from completing enrollment if the requisite app has been installed prior to this change. If you have MDM enrolled devices running Android 7.x or below, update them to Android version 8.0 (Oreo) or higher or replace them with a device on Android version 8.0 or higher.  

> [!NOTE]
> [Microsoft Teams devices](https://www.microsoft.com/en-us/microsoft-teams/across-devices/devices?rtc=2) are not impacted by this announcement and will continue to be supported regardless of their Android OS version.  

#### How can you prepare?  

Notify your helpdesk, if applicable, of this upcoming change in support. You can identify how many devices are currently running Android 7.x or below by navigating to **Devices** > **All devices** > **Filter**. Then filter by OS and sort by OS version. There are two admin options to help inform your users or block enrollment.

Here's how you can warn users:

- Create an app protection policy and configure [conditional launch](../apps/app-protection-policy-settings-android.md#conditional-launch) with a min OS version requirement that warns users.  
- Utilize a device compliance policy for [Android device administrator](../protect/compliance-policy-create-android.md) or [Android Enterprise](../protect/compliance-policy-create-android-for-work.md) and set the action for non-compliance to send an email or push notification to users before marking them noncompliant.  

Here's how you can block devices running on versions earlier than Android 8.0:  

- Create an app protection policy and configure conditional launch with a min OS version requirement that blocks users from app access.  
- Utilize a device compliance policy for Android device administrator or Android Enterprise to make devices running Android 7.x or earlier non-compliant. 
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

### Plan for change: Enrollment restrictions will no longer be included in policy sets<!--1067033 -->

With the Microsoft Intune service release (2109), you'll no longer be able to configure enrollment restrictions in policy sets. Instead, you'll need to go to **Devices** > **Policy** section > **Enrollment restrictions** to create and manage all enrollment restrictions.  

#### How does this affect you or your users?

If our service telemetry indicates that your existing policy sets include enrollment restrictions, we'll migrate your policies when the new restrictions are in place. To create and manage enrollment restrictions going forward, go to **Devices** > **Policy** section > **Enrollment restrictions**.

#### How can you prepare?

Update your documentation. Be sure to configure all new enrollment restrictions in the **Enrollment restrictions** section of Intune. We'll start migrating existing policies with the 2109 service release.

### Take action: Update to the latest version of the Android Company Portal app<!--10488117-->

Starting with the October (2110) service release, Intune will no longer support new Android device administrator enrollments that use Company Portal version 5.04993.0 or earlier. The reason is a change in the integration of Intune with Samsung devices.

#### How does this affect you or your users?

Users who need to enroll Samsung devices in an Android device administrator by using an older version of the Company Portal app (any version earlier than 5.04993.0) will no longer be successful. They'll need to update the Company Portal app to successfully enroll.

#### How can you prepare?

Update any older version of the Company Portal staged in your environment to support Android device administrator enrollments before the Intune October (2110) service release. Inform your users that they'll need to update to the latest version of the Android Company Portal to enroll their Samsung device. 

If applicable, inform your helpdesk in case users don't update the app before enrolling. We also recommend that you keep the Company Portal app updated to ensure that the latest fixes are available on your devices.

#### More information

- [How to update the Company Portal app](../user-help/install-a-new-version-of-the-company-portal-app.md)
- [Download the Microsoft Intune Company Portal for Android from the official Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=49140)

### Plan for change: Safe boot and debugging features in Android Enterprise device restrictions will be replaced

[Google announced](https://developers.google.com/android/management/release-notes#march-2021) that it has deprecated several settings in the Android Management API and will stop supporting the settings for Intune on November 1, 2021. This change affects the **Safe boot** and **Debugging features** configuration settings for Android Enterprise device restrictions. These settings will not be available after support ends. To prepare for this change, we'll add a new setting called **Developer settings** in September's (2109) service release.

#### How does this affect you or your users?

With the Intune October (2110) service release, **Safe boot** and **Debugging features** will be removed from the admin center UI. Those features will then be removed shortly after from Microsoft Graph API on October 31, 2021. If applicable, you should use the new setting, **Developer settings**.

**Developer settings** will be available for new and existing profiles in the September (2109) service release. By default, it's set as **Not configured**. If you choose to set this to **Allow**, users will be able to access developer settings. Developer settings might include the ability to enable debugging features and/or reboot the device in **Safe boot** mode.

> [!NOTE]
> If **Developer settings** is set to **Allow**, it will override both the **Safe boot** and **Debugging features** settings.

#### How can you prepare?

Review the configuration settings for your Android Enterprise device restrictions. If you want users to have access to developer settings after **Safe boot** and **Debugging features** are removed, you'll need to set **Developer settings** to **Allow**. Otherwise, it will remain as **Not configured**, and users won't have access to any developer settings.

### Plan for change: Announcing end of support for the existing Use Locations (network fence) feature in Intune<!-- 9492223  -->

Intune is announcing end of support for the [network fence feature](../protect/create-compliance-policy.md) for use only in devices enrolled through an Android device administrator. Google has reduced support for devices enrolled through a device administrator. Intune customers provided feedback that led to a re-envisioning of location-based fencing to better meet customer needs across multiple Android enrollment options.

#### How does this affect you or your users?

This change will affect you only if you currently use a location-based (network fence) compliance policy, on either your trial account or your paid account. In 90 days from the date of this feature end-of-support announcement (on or around October 7, 2021 unless otherwise updated), any network location-based compliance policies targeted to devices enrolled through an Android device administrator will no longer work to provide a network fence.

#### How can you prepare?

No action is needed at this time. Review our [In Development](../fundamentals/in-development.md) page for advanced notice of upcoming new features. We'll follow up with more information about re-envisioned location-based services when that information is available.

### Plan for change: Intune is moving to support iOS/iPadOS 13 and later<!--10144130-->

Apple has released iOS 15. Microsoft Intune, including Intune Company Portal and Intune app protection policies (APP, also known as mobile application management), now requires iOS/iPadOS 13 and later.

#### How does this affect you or your users?

If you're managing iOS/iPadOS devices, you might have devices that won't be able to upgrade to the minimum supported version (iOS/iPadOS 13). 

Because Office 365 mobile apps are supported on iOS/iPadOS 13.0 and later, this change might not affect you. You've likely already upgraded your OS or devices. 

To check which devices support iOS 13 or iPadOS 13 (if applicable), see the following Apple documentation:

- [Supported iPhone models](https://support.apple.com/guide/iphone/supported-iphone-models-iphe3fa5df43/13.0/ios/13.0)
- [Supported iPad models](https://support.apple.com/guide/ipad/supported-models-ipad213a25b2/13.0/ipados/13.0)
- [Supported iPod models](https://support.apple.com/guide/ipod-touch/your-ipod-touch-iphdd4353af4/13.0/ios/13.0)

#### How can you prepare?

Check your Intune reporting to see what devices or users might be affected. For devices with mobile device management, go to **Devices** > **All devices** and filter by OS. For devices with app protection policies, go to **Apps** > **Monitor** > **App protection status** > **App Protection report: iOS, Android**.

To manage the supported OS version in your organization, you can use Microsoft Endpoint Manager controls for both mobile device management and APP. For more information, see [Manage operating system versions with Intune](../fundamentals/manage-os-versions.md).

### Plan for change: Intune is moving to support macOS 10.15 and later with the release of macOS 12<!--10154527-->

Apple is expected to release macOS 12 Monterey in the fall of 2021. Shortly after the release, Microsoft Intune, the Company Portal app, and the Intune mobile device management agent will move to support macOS 10.15 (Catalina) and later.

#### How does this affect you or your users?

This change will affect you only if you currently manage, or plan to manage, macOS devices by using Intune. This change might not affect you because your users have likely already upgraded their macOS devices. For a list of supported devices, see [macOS Catalina is compatible with these computers](https://support.apple.com/en-us/HT210222).

> [!NOTE]
> Devices that are currently enrolled on macOS 10.13.x and 10.14 will remain enrolled after those versions are no longer supported. New devices will be unable to enroll if they're running macOS 10.14 or earlier.

#### How can you prepare?

Check your Intune reporting to see what devices or users might be affected. Go to **Devices** > **All devices** and filter by macOS. You can add more columns to help identify who in your organization has devices running macOS 10.14 or earlier. Ask your users to upgrade their devices to a supported OS version before the release of macOS 12.

### Plan for change: Intune is ending support for standalone client apps on Microsoft Tunnel<!-- 9370486   -->

Beginning on June 14, 2021, the Microsoft Defender for Endpoint app on Android supports Microsoft Tunnel functionality and is the official tunnel client app for Android Enterprise customers. With the release of Microsoft Defender for Endpoint as the Microsoft Tunnel client app, the standalone Microsoft Tunnel app for Android is deprecated. Support will end after January 31, 2022. When support ends, the standalone tunnel app will be removed from the Google Play store.

#### How does this affect you or your users?

If you use the standalone tunnel app for Android, you'll need to move to the Microsoft Defender for Endpoint app before January 31, 2022. This move will ensure that users can still access the Tunnel Gateway configuration.

#### How can you prepare?

For your devices that run Android Enterprise and currently use the standalone tunnel app, plan to [replace the standalone tunnel app with the Defender for Endpoint app](../protect/microsoft-tunnel-migrate-app.md). New devices should use Microsoft Defender for Endpoint as the tunnel client app.

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

In addition, the setting **Hide the Virus and threat protection area in the Windows Security app** has a child setting, **Hide the Ransomware data recovery option in the Windows Security app**. If the parent setting is set to **Not configured** and the child setting is set to **Yes**, both the parent and child settings will be set to **Not configured**. That change will take effect when you edit the profile.

#### How can you prepare?

No action is needed. However, you might want to notify your helpdesk about this change.

### Plan for change: Intune is ending Company Portal support for unsupported versions of Windows

Intune follows the Windows 10 lifecycle for supported Windows 10 versions. We're now removing support for the associated Windows 10 Company Portals for Windows versions that are out of the Modern Support policy.

#### How does this affect you or your users?

Because Microsoft no longer supports these operating systems, this change might not affect you. You've likely already upgraded your OS or devices. This change will affect you only if you're still managing unsupported Windows 10 versions. 

Windows and Company Portal versions that this change affects include:

- Windows 10 version 1507, Company Portal version 10.1.721.0
- Windows 10 version 1511, Company Portal version 10.1.1731.0
- Windows 10 version 1607, Company Portal version 10.3.5601.0
- Windows 10 version 1703, Company Portal version 10.3.5601.0
- Windows 10 version 1709, any Company Portal version

We won't uninstall these Company Portal versions, but we will remove them from the Microsoft Store and stop testing our service releases with them.

If you continue to use an unsupported version of Windows 10, your users won't get the latest security updates, new features, bug fixes, latency improvements, accessibility improvements, and performance investments. You won't be able to co-manage users by using System Center Configuration Manager and Intune.

#### How can you prepare?

In the Microsoft Endpoint Manager admin center, use the [discovered apps](../apps/app-discovered-apps.md) feature to find apps with these versions. On a user's device, the Company Portal version is shown on the **Settings** page of the Company Portal. Update to a supported Windows and Company Portal version.  
