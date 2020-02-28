---
# required metadata

title: App protection policies and work profiles in Microsoft Intune - Azure | Microsoft Docs
description: See the differences and pros and cons when deciding to use app protection policies or work profiles for personal or BYOD Android Enterprise devices in Microsoft Intune. Compare the differences and features you get with app protection policies without enrollment (APP-WE) and Android Enterprise work profiles.
keywords:

author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/13/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology:
ms.reviewer: chrisbal

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure

---

# Application protection policies and work profiles on Android Enterprise devices in Intune

In many organizations, administrators are challenged to protect resources and data on different devices. One challenge is protecting resources for users with personal Android Enterprise devices, also known as bring-your-own-device (BYOD). Microsoft Intune supports two Android deployment scenarios for bring-your-own-device (BYOD):

- App protection policies without enrollment (APP-WE)
- Android Enterprise work profiles

The APP-WE and the Android work profile deployment scenarios include the following key features important for BYOD environments:

1. **Protection and segregation of organization-managed data**: Both solutions protect organization data by enforcing data loss prevention (DLP) controls on organization-managed data. These protections prevent accidental leaks of protected data, such as an end user accidentally sharing it to a personal app or account. They also serve to ensure that a device accessing the data is healthy and not compromised.

2. **End-user privacy**: APP-WE and Android Enterprise work profiles separate end users content on the device, and data managed by the mobile device management (MDM) administrator. In both scenarios, IT admins enforce policies, such as PIN-only authentication on organization-managed apps or identities. IT admins are unable to read, access, or erase data that's owned or controlled by end users.

Whether you choose APP-WE or Android Enterprise work profiles for your BYOD deployment depends on your requirements and business needs. The goal of this article is to provide guidance to help you decide.

## About Intune app protection policies

Intune app protection policies (APP) are data protection policies targeted to users. The policies apply data loss protection at the application level. Intune APP requires app developers enable APP features on the apps they create.

Individual Android apps are enabled for APP in a few ways:

1. **Natively integrated into Microsoft first-party apps**: Microsoft Office apps for Android, and a selection of other Microsoft apps, come with Intune APP built-in. These Office apps, such as Word, OneDrive, Outlook, and so on, don't need any more customization to apply policies. These apps can be installed by end users directly from Google Play Store.

2. **Integrated into app builds by developers using the Intune SDK**: App developers can integrate the Intune SDK into their source code and recompile their apps to support Intune APP policy features.

3. **Wrapped using the Intune app wrapping tool**: Some customers compile Android apps (.APK file) without access to source code. Without the source code, the developer can't integrate with the Intune SDK. Without the SDK, they can't enable their app for APP policies. The developer must modify or recode the app to support APP policies.

    To help, Intune includes the **App Wrapping Tool** tool for existing Android apps (APKs), and creates an app that recognizes APP policies.

    For more information on this tool, see [prepare line-of-business apps for app protection policies](../developer/apps-prepare-mobile-application-management.md).

To see a list of apps enabled with APP, see [managed apps with a rich set of mobile application protection policies](https://www.microsoft.com/cloud-platform/microsoft-intune-apps).

## Deployment scenarios

This section describes the important characteristics of the APP-WE and Android Enterprise work profile deployment scenarios.

### APP-WE

An APP-WE (app protection policies without enrollment) deployment defines policies on apps, not devices. In this scenario, devices typically aren't enrolled or managed by an MDM authority, such as Intune. To protect apps and access to organizational data, administrators use APP-manageable apps, and apply data protection policies to these apps.

This feature applies to:

- Android 4.4 and later

> [!TIP]
> For more information, see [What are app protection policies?](app-protection-policy.md).

APP-WE scenarios are for end users who want a small organizational footprint on their devices, and don't want to enroll in MDM. As an administrator, you still need to protect your data. These devices aren't managed. So common MDM tasks and features, such as WiFi, device VPN, and certificate management, aren't part of this deployment scenario.

### Android Enterprise work profiles

Work profiles are the core Android Enterprise deployment scenario and the only scenario targeted at BYOD use cases. The work profile is a separate partition created at the Android OS level that can be managed by Intune.

This feature applies to:

- Android 5.0 and later devices with Google Mobile Services

A work profile includes the following features:

- **Traditional MDM functionality**: Key MDM capabilities, such as app lifecycle management using managed Google Play, is available in any Android Enterprise scenario. Managed Google Play provides a robust experience to install and update apps without any user intervention. IT can also push app configuration settings to organizational apps. It also doesn't require end users to allow installations from unknown sources. Other common MDM activities, such as deploying certificates, configuring WiFi/VPNs, and setting device passcodes are available with work profiles.

- **DLP on the work profile boundary**: Like APP-WE, IT can enforce data protection policies. With a work profile, DLP policies are enforced at the work profile level, not the app level. For example, copy/paste protection is enforced by the APP settings applied to an app, or enforced by the work profile. When the app is deployed into a work profile, administrators can pause copy/paste protection to the work profile by turning off this policy at the APP level.

## Tips to optimize the work profile experience

### When to use APP within work profiles

Intune APP and work profiles are complementary technologies that can be used together or separately. Architecturally, both solutions enforce policies at different layers – APP at the individual app layer, and work profile at the profile layer. Deploying apps managed with an APP policy to an app in a work profile is a valid and supported scenario. To use APP, work profiles, or a combination depends on your DLP requirements.

Work profiles and APP complement each other’s settings by providing additional coverage if one profile doesn't meet your organization's data protection requirements. For example, work profiles don't natively provide controls to restrict an app from saving to an untrusted cloud storage location. APP includes this feature. You may decide that DLP provided solely by the work profile is sufficient, and choose not to use APP. Or you may require the protections from a combination of the two.

### Suppress APP policy for work profiles

You may need to support individual users who have multiple devices - unmanaged devices in an APP-WE scenario, and managed devices with work profiles.

For example, you require end users to enter a PIN when opening a work app. Depending on the device, the PIN features are handled by APP or by the work profile. For the APP-WE devices, the PIN-to-launch behavior is enforced by APP. For work profile devices, you can use a device or work profile PIN enforced by the OS. To accomplish this scenario, configure APP settings so that they don't apply *when* an app is deployed into a work profile. If you don’t configure it this way, the end user gets prompted for a PIN by the device, and again at the APP layer.

### Control multi-identity behavior in work profiles

Office applications, such as Outlook and OneDrive, have “multi-identity” behavior. Within one instance of the application, the end user can add connections to multiple distinct accounts or cloud storage locations. Within the application, the data retrieved from these locations can be separate or merged. And, the user can context switch between personal identities (user@outlook.com) and organization identities (user@contoso.com).

When using work profiles, you may want to disable this multi-identity behavior. When you disable it, badged instances of the app in the work profile can only be configured with an organization identity. Use the Allowed Accounts app configuration setting for supporting Office Android apps.

For more information, see [deploy Outlook for iOS/iPadOS and Android app configuration settings](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune).

## When to use Intune APP

There are several enterprise mobility scenarios where using Intune APP is the best recommendation.

### Older devices running Android 4.4-5.1 are being used

Officially, any Android device 5.0 or above with Google Mobile Services supports work profiles, and is eligible to be managed in that way. However, some Android 5.0 and 5.1 devices from some OEMs don't support work profiles.

If using versions that don't support work profiles, and to ensure DLP for organization data on devices, you must use Intune APP features.

### No MDM, no enrollment, Google services are unavailable

Some customers don't want any form of device management, including work profile management, for different reasons:

- Legal and liability reasons
- For consistency of user experience
- The Android device environment is highly heterogeneous
- There isn't any connectivity to Google services, which is required for work profile management.

For example, customers in or have users in China can't use Android device management since Google services are blocked. In this case, use Intune APP for DLP.

## Summary

Using Intune, both APP-WE and Android Enterprise work profiles are available for your Android BYOD program. To choose APP-WE or work profiles depends upon your business and usage requirements. In summary, use work profiles if you need MDM activities on managed devices, such as certificate deployment, app push, and so on. Use APP-WE if you don’t want or can’t manage devices, and are using only Intune APP-enabled apps.

## Next steps

[Start using app protection policies](app-protection-policy.md), or [enroll your devices](../enrollment/android-enroll.md).
