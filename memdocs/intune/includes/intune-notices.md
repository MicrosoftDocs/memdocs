---
title: include file
description: include file
author: ErikjeMS  
ms.service: microsoft-intune
ms.topic: include
ms.date: 06/14/2021
ms.author: erikje
ms.custom: include file
---

These notices provide important information that can help you prepare for future Intune changes and features.

### Plan for Change: Intune moving to support iOS/iPadOS 13 and higher later this year<!--10144130-->

Later this year, we expect iOS 15 to be released by Apple. Microsoft Intune, including the Intune Company Portal and Intune app protection policies (APP, also known as MAM), will require  iOS/iPadOS 13 and higher shortly after iOS 15’s release.

#### How does this affect me?

If you are managing iOS/iPadOS devices, you might have devices that will not be able to upgrade to the minimum supported version (iOS/iPadOS 13). Provided that Office 365 mobile apps are supported on iOS/iPadOS 13.0 and higher, this may not affect you; you’ve likely already upgraded your OS or devices. See the following Apple documentation for devices to check which devices support iOS 13 or iPadOS 13 (if applicable).

- [Supported iPhone models](https://support.apple.com/guide/iphone/supported-iphone-models-iphe3fa5df43/13.0/ios/13.0)
- [Supported iPad models](https://support.apple.com/guide/ipad/supported-models-ipad213a25b2/13.0/ipados/13.0)
- [Supported iPod models](https://support.apple.com/guide/ipod-touch/your-ipod-touch-iphdd4353af4/13.0/ios/13.0)

For instructions on how to check in the Microsoft Endpoint Manager admin center which devices or users may be affected, read below.

#### What do I need to do to prepare for this change?

Check your Intune reporting to see what devices or users may be affected. For devices with mobile device management (MDM) go to **Devices** > **All devices** and filter by OS. For devices with app protection policies  go to **Apps** > **Monitor** > **App protection status** > **App Protection report: iOS, Android**.

To manage the supported OS version in your organization, you can use Microsoft Endpoint Manager controls for both MDM and APP.  For more information, please review: [Manage operating system versions with Intune - Microsoft Intune](../fundamentals/manage-os-versions.md).

### Plan for Change: Intune moving to support macOS 10.15 and later with the release of macOS 12<!--10154527-->

With Apple's expected release of macOS 12 Monterey in the fall of 2021, Microsoft Intune, the Company Portal app and the Intune MDM agent will be moving to support macOS 10.15 (Catalina) and higher shortly after the release.

#### How does this affect me?

This will only affect you if you currently manage, or plan to manage macOS devices with Intune. This may not impact you because your users have likely already upgraded their macOS devices. See [macOS Catalina is compatible with these computers](https://support.apple.com/en-us/HT210222) for a list of devices that are supported.

> [!NOTE]
> Devices that are currently enrolled on macOS 10.13.x and 10.14 will continue to remain enrolled even when those versions are no longer supported. New devices will be unable to enroll if running macOS 10.14 or below.

#### What do I need to do to prepare for this change?

Check your Intune reporting to see what devices or users may be affected. Go to Devices > All devices and filter by macOS. You can add in additional columns to help identify who in your organization has devices running macOS 10.14 or below. Request that your users upgrade their devices to a supported OS version before the release of macOS 12.

### Update your iOS Company Portal minimum version to v4.16.0<!-- 9964998 -->
We have recently released an updated Company Portal for iOS to the Apple Store that is a required app update. The minimum supported version of the iOS Company Portal is now v4.16.0.

#### What action do I need to take?
If you have enabled the **[Block installing apps using App Store](../configuration/device-restrictions-ios.md#settings-apply-to-automated-device-enrollment-supervised)** device restriction setting, you will likely need to push an update to the related devices. Otherwise, no action is needed, but if you have a helpdesk, you may want to make them aware of the prompt to update the Company Portal app.

#### How does this affect me?
User impact - Most users have app updates set to automatic, so they receive the updated Company Portal app without taking any action. Users that have an earlier app version will be prompted to update to the latest Company Portal app.

> [!NOTE]
> If you have enabled the **[Block installing apps using App Store](../configuration/device-restrictions-ios.md#settings-apply-to-automated-device-enrollment-supervised)** device restriction setting, you may need to manually push an update to the related devices.

### Plan for Change: Intune ending support for standalone client apps on Microsoft Tunnel<!-- 9370486   -->

Beginning on June 14, 2021, the Microsoft Defender for Endpoint app on Android supports Microsoft Tunnel functionality and is the official tunnel client app for Android Enterprise customers. With the release of Microsoft Defender for Endpoint as the Microsoft Tunnel client app, the standalone Microsoft Tunnel app for Android is deprecated with support ending in 60 days, after August 14, 2021. When support ends, the standalone tunnel app will be removed from the Google Play store.

#### How this change will affect your organization

If you use the standalone tunnel app for Android, you'll need to move to the Microsoft Defender for Endpoint app before August 14 2021 to ensure users can still access the Tunnel Gateway configuration.

#### What you need to do to prepare

For your devices that run Android Enterprise and currently use the standalone tunnel app, plan to [replace the standalone tunnel app with the Defender for Endpoint app](../protect/microsoft-tunnel-migrate-app.md). New devices should use Microsoft Defender for Endpoint as the tunnel client app.
### Upgrade to the Microsoft Intune Management Extension<!-- 10102913 -->

We’ve released an upgrade to the Microsoft Intune Management Extension to improve handling of Transport Layer Security (TLS) errors on Windows 10 devices. 

The new version for the Microsoft Intune Management Extension is **1.43.203.0**. Intune automatically upgrades all versions of the extension that are less than **1.43.203.0** to this latest version. To check the version of the extension on a device, review the version for *Microsoft Intune Management Extension* in the program list under **Apps & features**.

For more information, see **CVE-2021-31980** at [https://msrc.microsoft.com/update-guide/vulnerability/CVE-2021-31980](https://msrc.microsoft.com/update-guide/vulnerability/CVE-2021-31980).

#### What action do I need to take?

No action is required. As soon as the client connects to the service, it automatically receives a message to upgrade.

### Update to Endpoint Security Antivirus Windows 10 Profiles<!-- 9741752   -->

We've made a minor change to improve the Antivirus profile experience for Windows 10. There’s no end-user effect as this is a change only in what you’ll see in the UI.

#### How does this affect me?

Previously, when you configured a [Windows security profile](../protect/antivirus-security-experience-windows-settings.md) for Endpoint security Antivirus policy, you had two options for most settings: *Yes* and *Not configured*. Moving forward, those same settings now include *Yes*, *Not configured*, and a new option of *No*. Previously configured settings that were set to *Not configured* remain as *Not configured*.  When you create new profiles or edit an existing profile, you now have the option to explicitly specify *No*.

In addition, the setting *Hide the Virus and threat protection area in the Windows Security app* has a child setting, *Hide the Ransomware data recovery option in the Windows Security app*. If the parent setting (Hide the Virus and threat protection area) was set to *Not configured* and the child setting was set to *Yes*, both the parent and child settings will be set to *Not configured*, which will take effect when you edit the profile.

#### What action do I need to take?

No action is needed. However, you might want to notify your helpdesk about this change.

### Plan for Change: Intune ending company portal support for unsupported versions of Windows

Intune follows Windows 10 lifecycle for supported Windows 10 versions. We’re now removing support for the associated Windows 10 Company Portals for those Windows versions that are out of the Modern Support policy.

#### How does this affect me?

Given that Microsoft no longer supports these OSs, this may not affect you; you have likely already upgraded your OS or devices. This will only affect you if you are still managing unsupported Windows 10 versions. Windows and Company portal versions this affects include:

- Windows 10, Version 1507, Company portal version 10.1.721.0
- Windows 10, Version 1511, Company portal version 10.1.1731.0
- Windows 10, Version 1607, Company portal version 10.3.5601.0
- Windows 10, Version 1703, Company portal version 10.3.5601.0
- Windows 10, Version 1709, any Company portal version

We will not uninstall these Company portal versions mentioned above, but we will remove them from the Microsoft Store and stop testing our service releases with them.

**User Impact:** If you continue to use an unsupported version of Window 10, your users won't get the latest security updates, new features, bug fixes, latency improvements, accessibility improvements, and performance investments. The user will not be able to be co-managed with System Center Configuration Manager and Intune.

#### What do I need to do?

In the Microsoft Endpoint Manager admin center, use the [Discovered apps](../apps/app-discovered-apps.md) feature to find apps with these versions. On a user’s device, the Company Portal version is shown in the **Settings** page of the company portal. Update to a supported Windows/Company Portal version.

### Plan for Change: Intune moving to support Android 6.0 and higher in April 2021

As mentioned in MC234534, Intune will be moving to support Android 6.0 (Marshmallow) and higher in the April (2104) service release.

#### How this change will affect your organization

Given that the Office mobile apps for Android ended support for Android 5.x (Lollipop) on June 30, 2019 (MC181101) this change may not affect you; you have likely already upgraded your OS or devices. However, if you have any device that is still running Android version 5.x, or decide to enroll any device that is running Android version 5.x, please note that these devices will no longer be supported. Either update them to Android version 6.0 (Marshmallow) or higher or replace them with a device on Android version 6.0 or higher.

> [!NOTE]
> Teams Android devices are not impacted by this announcement and will continue to be supported regardless of their Android OS version.

#### What you need to do to prepare

Notify your helpdesk, if applicable, of this upcoming change in support. You also have two admin options to help inform your end users or block enrollment.

1. Here’s how you can warn end users:
    - Utilize a device compliance policy for Android device administrator or Android Enterprise and set the action for non-compliance to send a message to users before marking them noncompliant.
    - Configure an app protection policy Conditional launch setting with a Min OS version requirement to warn users.
2. Here’s how you can block devices on versions below Android 6.0:
    - Set enrollment restrictions to prevent devices on Android 5.x from enrolling
    - Utilize a device compliance policy for Android device administrator or Android Enterprise to make devices on Android 5.x non-compliant.
    - Configure an app protection policy Conditional launch setting with a Min OS version requirement to block users from app access.