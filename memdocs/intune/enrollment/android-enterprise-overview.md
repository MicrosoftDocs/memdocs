---
# required metadata

title: Manage Android Enterprise work profile devices in Microsoft Intune
titleSuffix: 
description: Microsoft Intune manages Android Enterprise personally-owned and corporate-owned work profile devices to provide additional management capabilities and privacy when people use their personal Android devices for work.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/20/2021
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 2cc3c960-1fdd-47ca-a693-420d47b403de

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Manage Android personally-owned/corporate-owned work profile devices with Intune

Android Enterprise offers a set of enrollment options that provide users with the most up-to-date and secure features. Enrolling with an Android Enterprise personally-owned/corporate-owned work profile allows a set of features and services that separate personal apps and data from work apps and data. It also provides additional management capabilities and privacy when people use their personal Android devices for work. 

## Supported devices

Android Enterprise management capabilities rely upon features that are part of more recent Android operating systems. For devices that do not support Android Enterprise, conventional Android management remains available. For more information, see [Android Enterprise requirements](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012).

## Onboarding

Before enrolling Android Enterprise work profile devices, you must complete some onboarding steps. These steps establish a connection between your Intune tenant and Managed Google Play. For more information, see [Enable enrollment of Android Enterprise personally-owned work profile devices](android-work-profile-enroll.md) or [Set up Intune enrollment of Android Enterprise corporate-owned devices with work profile](android-corporate-owned-work-profile-enroll.md).

## Work profile management

When you manage an Android Enterprise personally-owned or corporate-owned work profile device with Intune, you don't manage the entire device. Management capabilities only affect the work profile that is created on the device during enrollment. Any apps deployed to the device with Intune get installed in the work profile. App icons in the work profile are differentiated from personal apps on the device. All Android apps and data outside the Android enterprise portion of the device remain personal and under the control of the end user. Users can install any app they choose to the personal side of the device. Administrators can manage and monitor apps and actions scoped to the work profile.

When configuring policies for device configuration or compliance, the broad range of settings enables you to tailor protection to your specific needs. To better understand how to implement specific security configuration scenarios, see the security configuration framework guidance for Android Enterprise device restriction policies.

The security configuration framework is organized into distinct configuration levels that provide guidance for personally owned and supervised devices, with each level building off the previous level. The available levels and settings in each level vary by enrollment mode:

- For Android Enterprise personally-owned work profile devices: [Android personally-owned work profile security settings](../enrollment/android-work-profile-security-settings.md)
- For Android Enterprise fully managed, dedicated, and corporate-owned work profile devices: [Android fully managed-security settings](../enrollment/android-fully-managed-security-settings.md)

Alternatively, you can review the [Device compliance settings for Android Enterprise in Intune](../protect/compliance-policy-create-android-for-work.md) and [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md).

## App publishing and distribution

Managed Google Play is an integral part of Android Enterprise app distribution and management. All apps deployed to Android Enterprise personally-owned and corporate-owned work profile devices in the work profile come from the Managed Google Play service. To manage and deploy apps in the Play Store, you sign in to the Google Play website with your company's administrator credentials for Google management. You can approve apps for Android Enterprise deployment to have them appear in devices' work profiles. These apps then sync to the Microsoft Endpoint Manager admin center where they can then be deployed and managed using Intune. Line of business (LOB) apps developed by your organization must be published to Managed Google Play using Google's Android app publishing console. Line-of-business apps must be configured in the Android app publishing console to restrict access to your organization.

Apps can be installed without user interaction and without requiring that the user allow **Installation from Unknown Sources**. To browse and install optional or available apps, the user can browse the Play for Work store on their device. For more information, see [Assign apps to Android Enterprise work profile devices with Intune](../apps/apps-add-android-for-work.md).

## App configuration

Android Enterprise provides infrastructure for deploying app configuration values to apps that support them. By specifying configuration values for work apps, you ensure they are properly set when users launch the app for the first time. Support for app configuration requires that app developers create their Android apps specifically to support managed configuration values. If they do, then you can use Intune to specify and apply these configuration settings. For more information, see [Add app configuration policies for managed Android devices](../apps/app-configuration-policies-use-android.md).

## Email configuration

Android Enterprise doesn't provide a default email app or native email profile object like those provided by iOS/iPadOS. Instead, email configurations can be set by applying app configuration settings to email apps that support them. Gmail and Nine Work are two Exchange ActiveSync (EAS) client apps in the Play Store that support configuration with Android Enterprise app configuration.

Intune provides configuration templates for Gmail and Nine Work apps when managed as work apps. Other email apps that support app configuration profiles can be configured with mobile app configuration policies.

If you are using Exchange ActiveSync Conditional Access for an Android Enterprise personally-owned or corporate-owned work profile device, consider using either the Gmail or Nine Work email app. The Microsoft Outlook for Android app, or any other email app that uses modern authentication via MSAL, is also supported. For more information, see [How to configure email settings in Microsoft Intune](../configuration/email-settings-configure.md).

   > [!NOTE]
   > Azure Active Directory (Azure AD) Authentication Library (ADAL) will be deprecated, so we recommend updating apps that currently use it to MSAL. For more information, see [Update your applications to use Microsoft Authentication Library (MSAL) and Microsoft Graph API](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363). 


## App protection policies

App protection policies applied are fully supported in the personally-owned/corporate-owned work profile and in the personal profile. You can publish line-of-business apps in the Android app publishing console at https://play.google.com/apps/publish. This console includes an option to make apps private to your organization. For more information, see [Add a device compliance policy for Android Enterprise work profile devices in Intune](../protect/compliance-policy-create-android-for-work.md). For general information about app protection policies, see [What are app protection policies?](../apps/app-protection-policy.md)

## VPN profiles

VPN support is similar to Android VPN profiles. The same VPN providers and basic configuration options are available for Android Enterprise management with two differences:

- **Work profile-scoped VPN** – VPN connections are limited to just the apps deployed to the personally-owned or corporate-owned work profile. Only Android Enterpise-managed apps can use the VPN connection. Personal apps on the device cannot use a managed VPN connection. For more information, see [Android Enterprise VPN settings](../configuration/vpn-settings-android-enterprise.md).

- **App-specific VPN** – App-specific VPN can be configured in Intune if the VPN provider supports:
  - configuration for app-specific VPN
  - the capability to configure per-app VPN via the Android Enterprise app configuration profile.
  For more information, see [Use a Microsoft Intune custom profile to create a per-app VPN profile for Android devices](../configuration/android-pulse-secure-per-app-vpn.md).

## Certificate profiles

The same certificate profile configuration options that are available to Android management are available on Android Enterprise personally-owned and corporate-owned work profile devices. Android Enterprise provides enhanced certificate management APIs. Enhanced certificate management provides the following functionality:

- Ensures that cert deployment is silent and seamless for the user.
- Ensures that deployed certs are removed when a device is retired from Intune and the work profile is removed.
- Provides improved messaging that informs users that the certificate was deployed and configured by their IT department via their management service.

For more information, see [Configure a certificate profile for your devices in Microsoft Intune](../protect/certificates-configure.md).

## Wi-Fi profiles

Wi-Fi profiles managed by Android Enterprise are removed when the device is retired from Intune and the work profile is deleted. For more information, see [How to configure Wi-Fi settings in Microsoft Intune](../configuration/wi-fi-settings-configure.md).

## Next steps
- [Enroll Android devices](android-enroll.md)
- [Assign apps to Android Enterprise work profile devices with Intune](../apps/apps-add-android-for-work.md)
