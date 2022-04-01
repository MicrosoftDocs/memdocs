---
# required metadata

title: Prepare apps for mobile application management with Microsoft Intune 
description: The information in this topic helps you decide when you should use the App wrapping tool and the App SDK to enable your custom line-of-business apps to use the mobile app management policies.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/01/2021
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology:
ms.assetid: 29e22121-8268-48b5-a671-f940a6be1d24

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: jamiesil
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: seodec18
ms.collection: M365-identity-device-management
---

# Prepare line-of-business apps for app protection policies

You can enable your apps to use app protection policies by using either the Intune App Wrapping Tool or the Intune App SDK. Use this information to learn about these two methods and when to use them.

## Intune App Wrapping Tool

The App Wrapping Tool is used primarily for **internal** line-of-business (LOB) apps. The tool is a command-line application that creates a wrapper around the app, which then allows the app to be managed by an Intune app protection policy. When protecting an app provided by an independent software vendor (ISV) it's important to clarify if the ISV will still support the wrapped app.

You don't need the source code to use the tool, but you do need signing credentials. For more about signing credentials, see the [Intune blog](https://blogs.technet.microsoft.com/enterprisemobility/2015/02/25/how-to-obtain-the-prerequisites-for-the-intune-app-wrapping-tool-for-ios/). For the App Wrapping Tool documentation, see [Android App Wrapping Tool](app-wrapper-prepare-android.md) and [iOS App Wrapping Tool](app-wrapper-prepare-ios.md).

The App Wrapping Tool does **not** support apps in or available in the Apple App Store or Google Play Store. It also doesn't support certain features that require developer integration (see the following feature comparison table).

For more information about the App Wrapping Tool for app protection policies on devices that are not enrolled in Intune, see [Protect line-of-business apps and data on devices not enrolled in Microsoft Intune](../apps/apps-add.md).

> [!IMPORTANT]
> Intune regularly releases updates to the Intune App Wrapping Tool. Regularly check the [Intune App Wrapping Tool](https://github.com/msintuneappsdk) repositories for updates and incorporate into your software development release cycle to ensure your apps support the latest App Protection Policy settings.

### Reasons to use the App Wrapping Tool

* Your app does not have built-in data protection features
* Your app is deployed internally and the app is not available in the Apple App Store or Google Play Store
* You don't have access to the app's source code
* You didn't develop the app
* Your app has minimal user authentication experiences

### Supported app development platforms

|**App Wrapping Tool** | **Xamarin** |**Cordova** |
|------|----|----|
|**iOS** |Yes|Yes|
|**Android**|No - use the [Intune App SDK Xamarin Bindings](app-sdk-xamarin.md).|Yes|

## Intune App SDK

The App SDK is designed mainly for customers who have apps in the Apple App Store or Google Play Store, and want to be able to manage the apps with Intune. However, any app can take advantage of integrating the SDK, even line-of-business apps.

To learn more about the SDK, see the [Overview](app-sdk.md). To get started with the SDK, see [Getting Started With the Microsoft Intune App SDK](app-sdk-get-started.md).

### Reasons to use the SDK

* Your app does not have built-in data protection features
* Your app is deployed on a public app store such as Google Play or Apple's App Store
* You are an app developer and have the technical background to use the SDK
* Your app has other SDK integrations
* Your app is frequently updated

### Supported app development platforms

|**Intune App SDK** |**Xamarin** |**Cordova**
|------|----|----|
|**iOS**|Yes – use the [Intune App SDK Xamarin Bindings](app-sdk-xamarin.md).|No|
|**Android**| Yes - use the [Intune App SDK Xamarin Bindings](app-sdk-xamarin.md).|No|

## Not using an app development platform listed above?

The Intune SDK development team actively tests and maintains support for apps built with the native Android, iOS (Obj-C, Swift), Xamarin, and Xamarin.Forms platforms. Guidance is not provided for other platforms, but it is possible to use the native SDK to create your own plug-ins.

## Feature comparison

This table lists the settings that are enabled if an app uses the App SDK or the App Wrapping Tool. Some features require app developers to apply some logic outside of basic integration with the Intune SDK, and as such, are not enabled if the app uses the App Wrapping Tool. 

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
|Targeted Application Configuration (or app config through the "MAM channel")|X|X|
|Support for Multi-Identity|X||
|Customizable Style |X||
|On-demand application VPN connections with Citrix mVPN|X|X| 
|Disable contact sync|X|X|
|Disable printing|X|X|
|Require minimum app version|X|X|
|Require minimum operating system|X|X|
|Require minimum Android security patch version (Android only)|X|X|
|Require minimum Intune SDK for iOS (iOS only)|X|X|
|SafetyNet device attestation (Android only)|X|X|
|Threat scan on apps (Android only)|X|X|
|Require maximum Mobile Threat Defense vendor device risk level|X||
|Configure app notification content for organization accounts|X|X|
|Require use of approved keyboards (Android only)|X|X|
|Require app protection policy (Conditional Access)|X||

## Next steps

To learn more about app protection policies and Intune, see the following topics:

- [Android app wrapping tool](app-wrapper-prepare-android.md)<br>
- [iOS app wrapping tool](app-wrapper-prepare-ios.md)<br>
- [Use the SDK to enable apps for mobile application management](app-sdk.md)
