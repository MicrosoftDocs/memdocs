---
title: Prepare Apps for Mobile Application Management With Microsoft Intune
description: The information in this article helps you decide when you should use the App wrapping tool and the App SDK to enable your custom line-of-business apps to use the mobile app management policies.
ms.date: 12/03/2025
ms.topic: reference
ms.reviewer: jamiesil
ms.collection:
- M365-identity-device-management
---

# Prepare Line-of-Business Apps for App Protection Policies

You can enable your apps to use app protection policies by using either the Intune App Wrapping Tool or the Intune App SDK. Use this information to learn about these two methods and when to use them.

## Intune App Wrapping Tool

The App Wrapping Tool is used primarily for **internal** line-of-business (LOB) apps. The tool is a command-line application that creates a wrapper around the app, which then allows Intune app protection policy to manage the app. When protecting an app provided by an independent software vendor (ISV), it's important to clarify if the ISV supports the wrapped app.

You don't need the source code to use the tool, but you do need valid signing credentials. For more information about the signing requirements, see [Certificate, provisioning profile, and authentication requirements](app-wrapper-prepare-ios.md#certificate-provisioning-profile-and-authentication-requirements). For the App Wrapping Tool documentation, see [Android App Wrapping Tool](app-wrapper-prepare-android.md) and [iOS App Wrapping Tool](app-wrapper-prepare-ios.md).

The App Wrapping Tool does **not** support apps in or available in the Apple App Store or Google Play Store. It also doesn't support certain features that require developer integration (see the following feature comparison table).

For more information about the App Wrapping Tool for app protection policies on devices that aren't enrolled in Intune, see [Protect line-of-business apps and data on devices not enrolled in Microsoft Intune](../apps/apps-add.md).

> [!IMPORTANT]
> Intune regularly releases updates to the Intune App Wrapping Tool. Regularly check the [Intune App Wrapping Tool](https://github.com/msintuneappsdk) repositories for updates and incorporate into your software development release cycle to ensure your apps support the latest App Protection Policy settings.

### Reasons to use the App Wrapping Tool

* Your app doesn't have built-in data protection features
* Your app is deployed internally and the app isn't available in the Apple App Store or Google Play Store
* You don't have access to the app's source code
* You didn't develop the app
* Your app has minimal user authentication experiences

## Intune App SDK

The App SDK is designed mainly for customers who have apps in the Apple App Store or Google Play Store, and want to be able to manage the apps with Intune. However, any app can take advantage of integrating the SDK, even line-of-business apps.

To learn more about the SDK, see the [Overview](app-sdk.md). To get started with the SDK, see [Getting Started With the Microsoft Intune App SDK](app-sdk-get-started.md).

### Reasons to use the SDK

* Your app doesn't have built-in data protection features
* Your app is deployed on a public app store such as Google Play or Apple's App Store
* You're an app developer and have the technical background to use the SDK
* Your app has other SDK integrations
* Your app is frequently updated

## Not using a previously listed app development platform?

The Intune SDK development team actively tests and maintains support for apps built with the native Android and iOS (Obj-C, Swift) platforms. Guidance isn't provided for other platforms, but it's possible to use the native SDK to create your own plug-ins.

## Feature comparison

This table lists the settings that are enabled if an app uses the App SDK or the App Wrapping Tool. Some features require app developers to apply some logic outside of basic integration with the Intune SDK, and as such, aren't enabled if the app uses the App Wrapping Tool.

|Feature|App SDK|App Wrapping Tool|
|-----------|---------------------|-----------|
|Restrict web content to display in a corporate managed browser|X|X|
|Prevent Android, iTunes, or iCloud backups|X|X|
|Allow app to transfer data to other apps|X|X|
|Allow app to receive data from other apps|X|X|
|Restrict cut, copy, and paste with other apps|X|X|
|Specify the number of characters that may be cut or copied from a managed app|X|X|
|Require simple PIN for access|X|X|
|Specify the number of attempts before PIN reset|X|X|
|Allow fingerprint instead of PIN|X|X|
|Allow facial recognition instead of PIN (iOS only)|X|X|
|Require corporate credentials for access|X|X|
|Set a PIN expiry|X|X|
|Block managed apps from running on jailbroken or rooted devices|X|X|
|Encrypt app data|X|X|
|Recheck the access requirements after a specified number of minutes|X|X|
|Specify the offline grace period|X|X|
|Block screen capture (Android only)|X|X|
|Support for MAM without device enrollment|X|X|
|Full Wipe of app data|X|X|
|Selective Wipe of work and school data in Multi-Identity scenarios <br><br>**Note:** For iOS/iPadOS, when the management profile is removed, the app is also removed.|X||
|Prevent "Save as"|X||
|Targeted Application Configuration (or app config through the "MAM channel")|X||
|Support for Multi-Identity|X||
|Customizable Style |X||
|On-demand application VPN connections with Citrix mVPN|X|X|
|Disable contact sync|X|X|
|Disable printing|X|X|
|Require minimum app version|X|X|
|Require minimum operating system|X|X|
|Require minimum Android security patch version (Android only)|X|X|
|Require minimum Intune SDK for iOS (iOS only)|X|X|
|Play integrity verdict (Android only)|X|X|
|Threat scan on apps (Android only)|X|X|
|Require maximum Mobile Threat Defense vendor device risk level|X||
|Configure app notification content for organization accounts|X|X|
|Require use of approved keyboards (Android only)|X|X|
|Require app protection policy (Conditional Access)|X||

## Next steps

For more information about app protection policies and Intune, see:

- [Android app wrapping tool](app-wrapper-prepare-android.md)
- [iOS app wrapping tool](app-wrapper-prepare-ios.md)
- [Use the SDK to enable apps for mobile application management](app-sdk.md)
