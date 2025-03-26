---
# required metadata

title: Overview of Android work profile management in Microsoft Intune  
titleSuffix: 
description: Learn more about Android Enterprise work profile management, a device management option for personal and corporate-owned devices enrolling in Microsoft Intune.  
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/05/2024
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
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

# Android Enterprise work profile management overview  

Microsoft Intune supports work profile management, an Android Enterprise management option that enables platform-level separation of work apps and data on enrolled devices. When an employee or student enrolls their device in Intune, they enable the creation of a *work profile*. The work profile creates a separate partition on the device for the user's work account, so that the user can switch between their personal apps and work apps easily and securely. When they leave the work profile, they return to the personal side of their device, where their personal apps and data are unaffected by Intune policies.  

Device users enrolling personal devices must enroll through the Intune Company Portal app, while users on corporate-owned devices must enroll through the Microsoft Intune app.  

This article provides an overview of the Android Enterprise work profile management options supported by Microsoft Intune, which include:  

- Work profiles for corporate-owned devices.  
- Work profiles for personal devices.  

## You need to know    

Android Enterprise isn't available everywhere. Before you create an enrollment profile in the Microsoft Intune admin center, make sure Android Enterprise is available in your region. For more information about availability and requirements for Android Enterprise, see [Android Enterprise requirements](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012) (opens Android Enterprise Help).  

In places where Android Enterprise isn't supported, there are other Intune-supported Android management options to choose from, including: 

* Android open source platform (AOSP) management 
* Android device administrator management  
* Mobile application management  

## Managed Google Play account       

To enable device and app management for Android Enterprise devices in Intune, you must [connect your Microsoft Intune tenant to a Managed Google Play account](connect-intune-android-enterprise.md).  

## Managing the work profile  

Microsoft Intune policies and settings only apply to the work profile. As an Intune administrator, you can manage the work parts of the enrolled device.  

* All apps you deploy in Intune get installed in the work profile. Administrators can manage and monitor apps and actions scoped to the work profile. 
* All Android apps and data outside of the work profile remain personal and under the control of the device user. Users can install any app they choose on the personal side of the device.  

There are unique app icons in the work profile to help users differentiate between the work apps and personal apps on their device.  

The settings available in Intune, ranging from enrollment to device configuration to compliance, allow you to tailor the level of protection to your organization's needs. For more information about applicable settings, see:  

* [Device compliance settings for Android Enterprise in Intune](../protect/compliance-policy-create-android-for-work.md)
* [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md)  

<!-- Removing section until linked files are updated.
When configuring policies for device configuration or compliance, the broad range of settings enables you to tailor protection to your specific needs. To better understand how to implement specific security configuration scenarios, see the security configuration framework guidance for Android Enterprise device restriction policies. The security configuration framework is organized into distinct configuration levels that provide guidance for personally owned and supervised devices, with each level building off the previous level. The available levels and settings in each level vary by enrollment mode:

- For Android Enterprise personally owned work profile devices: [Android personally owned work profile security settings](../enrollment/android-work-profile-security-settings.md)
- For Android Enterprise fully managed, dedicated, and corporate-owned work profile devices: [Android fully managed-security settings](../enrollment/android-fully-managed-security-settings.md)

Alternatively, you can review the [Device compliance settings for Android Enterprise in Intune](../protect/compliance-policy-create-android-for-work.md) and [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md). -->

## App publishing and distribution

Managed Google Play is an integral part of Android Enterprise app distribution and management. All apps deployed to the work profile on personal and corporate-owned devices come from the Managed Google Play service. 

To manage and deploy apps in the Play Store, sign in to the Google Play website with your administrator credentials for Google management. From here, you can approve apps for deployment. Approved apps sync with Microsoft Intune and appear in the admin center where you can deploy and manage them. Line of business (LOB) apps developed by your organization must be published to Managed Google Play using the Google Play managed publishing console. 

Apps can be installed without user interaction and without requiring the user to allow app installations from unknown sources. To browse and install optional or available apps, the user can browse the Managed Google Play store on their device. For more information, see [Assign apps to Android Enterprise work profile devices with Intune](../apps/apps-add-android-for-work.md).  

## App configuration  

Android Enterprise provides infrastructure for deploying app configuration values to apps that support them. By specifying the values for work apps, you ensure they're properly configured when users launch the app for the first time. Support for app configuration requires that app developers create Android apps specifically to support managed configuration values. If they do, then you can use Intune to specify and apply these configuration settings. For more information, see [Add app configuration policies for managed Android devices](../apps/app-configuration-policies-use-android.md).  

## Email configuration

Android Enterprise doesn't provide a default email app or native email profile object like those provided by iOS/iPadOS. Instead, you can configure email settings for supported email apps via Intune app configuration settings. 

Gmail and Nine Work are two Exchange ActiveSync (EAS) client apps in the Play Store that support Android Enterprise app configuration. Intune provides configuration templates for Gmail and Nine Work apps so you can manage them as work apps. You can configure other email apps that support app configuration profiles in an app configuration policy.   

If you're using Exchange ActiveSync Conditional Access for a personal or corporate-owned device, consider using the Gmail or Nine Work email app. The Microsoft Outlook for Android app, and any other email app that uses modern authentication via MSAL, is also supported. For more information, see [How to configure email settings in Microsoft Intune](../configuration/email-settings-configure.md). 

   > [!TIP]
   > Azure AD Authentication Library (ADAL) has been deprecated, so we recommend updating apps that currently use ADAL to MSAL. For more information, see [Update your applications to use Microsoft Authentication Library (MSAL) and Microsoft Graph API](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363). 


## App protection policies  

Microsoft Intune supports app protection policies applied to apps in the work profile and on the personal side of devices. You can publish line-of-business apps in the [Google Play publishing console](https://play.google.com/apps/publish), and you can make apps private to your organization.  

For more information about app protection policies for the work profile, see the following articles:  

* [Overview of app protection policies](../apps/app-protection-policy.md)  

* [Add a device compliance policy for work profile devices in Intune](../protect/compliance-policy-create-android-for-work.md)  

## VPN profiles  

VPN support is similar to Android VPN profiles. The same VPN providers and basic configuration options are available for Android Enterprise management, with two differences:

- **Work profile-scoped VPN** – VPN connections are limited to the apps deployed to the work profile on personal and corporate-owned devices, so only managed apps can use the VPN connection. Personal apps on the device can't use a managed VPN connection. For more information, see [Android Enterprise VPN settings](../configuration/vpn-settings-android-enterprise.md).  

- **App-specific VPN** – You can configure an app-specific VPN in Intune if the VPN provider supports:  

  - The configuration of an app-specific VPN.  

  - The capability to configure per-app VPN via the Android Enterprise app configuration profile.  

  For more information, see [Use a Microsoft Intune custom profile to create a per-app VPN profile for Android devices](../configuration/android-pulse-secure-per-app-vpn.md).  

## Certificate profiles

The same certificate profile configurations that are available to Android management are available for the work profile on personal and corporate-owned devices. Android Enterprise provides enhanced certificate management APIs.  

Enhanced certificate management:   

- Ensures that certificate deployment is silent and seamless for the user.  

- Ensures that deployed certificates are removed when a device retires from Intune and the work profile is removed.  

- Informs device users that the certificate was deployed and configured by their IT support person via Microsoft Intune.  

For more information, see [Configure a certificate profile for your devices in Microsoft Intune](../protect/certificates-configure.md).  

## Wi-Fi profiles

Wi-Fi profiles are removed when the device retires from Intune and the work profile is deleted. For more information, see [How to configure Wi-Fi settings in Microsoft Intune](../configuration/wi-fi-settings-configure.md).  

## Next steps  

- [Enrollment deployment guide for Android](../fundamentals/deployment-guide-enrollment-android.md)  

- [Assign apps to Android Enterprise work profile devices with Intune](../apps/apps-add-android-for-work.md)  
