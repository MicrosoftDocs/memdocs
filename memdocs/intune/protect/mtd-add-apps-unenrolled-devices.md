---
# required metadata

title: Add Mobile Threat Defense apps to unenrolled devices
titleSuffix: Microsoft Intune
description: Add Mobile Threat Defense apps to unenrolled devices by device users.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/19/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection: M365-identity-device-management
---

# Add Mobile Threat Defense apps to unenrolled devices

By default, when using Intune app protection policies with Mobile Threat Defense, Intune does the work to guide the end user on their device to install and sign in to all required apps to enable the connections with the relevant services.

End users need the Microsoft Authenticator (iOS) to register their device, and the Mobile Threat Defense (both Android and iOS) to receive notifications when a threat is identified in their mobile devices, and to receive guidance to remediate the threats.

Optionally, you can use Intune to add and deploy the Microsoft Authenticator, and Mobile Threat Defense (MTD) apps as well.

> [!NOTE]
> This article applies to all Mobile Threat Defense partners that support app protection policies:
>
> - Microsoft Defender for Endpoint (Android,iOS/iPadOS)
> - Better Mobile (Android,iOS/iPadOS)
> - Check Point Harmony Mobile (Android, iOS/iPadOS)
> - Lookout for Work (Android, iOS/iPadOS)
> - MVISION Mobile (Android,iOS/iPadOS)
> - Symantec Endpoint Security (Android, iOS/iPadOS)
> - Wandera (Android,iOS/iPadOS)
> - Zimperium (Android,iOS/iPadOS)
>
> For unenrolled devices, you **do not need an iOS app configuration policy** that sets up the Mobile Threat Defense for iOS app you use with Intune. This is a key difference compared to Intune enrolled devices.

## Configure Microsoft Authenticator for iOS via Intune (optional)

When using Intune app protection policies with Mobile Threat Defense, Intune will guide the end user to install, sign in to, and register their device with the Microsoft Authenticator (iOS).

However, should you wish to make the app available to end users via the Intune Company Portal, see the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [Microsoft Authenticator - iOS App Store URL](https://itunes.apple.com/us/app/microsoft-authenticator/id983156458?mt=8) when completing the **Configure app information** section. Don't forget to [assigning app to groups with Intune](../apps/apps-deploy.md) as the final step.

> [!NOTE]
> For iOS devices, you need the [Microsoft Authenticator](/azure/multi-factor-authentication/end-user/microsoft-authenticator-app-how-to) so users can have their identities checked by Azure AD. The Intune Company Portal works as the broker on Android devices so users can have their identities checked by Azure AD.

## Making Mobile Threat Defense apps available via Intune (optional)

When you use Intune app protection policies with Mobile Threat Defense, Intune guides the end user to install and sign in to the required Mobile Threat Defense client app.

However, should you wish to make the app available to end users via the Intune Company Portal, you can follow the steps provided in the following sections. Make sure you're familiar with the process of:

- [Adding an app into Intune](../apps/apps-add.md)
- [Assigning an app with Intune](../apps/apps-deploy.md)

### Making Better Mobile available to end users

- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [Active Shield - Play Store URL](https://play.google.com/store/apps/details?id=com.better.active.shield.enterprise) when completing the **Configure app information** section.

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [ActiveShield - App Store URL](https://itunes.apple.com/us/app/activeshield/id980234260?mt=8&uo=4) when completing the **Configure app information** section.

### Making Check Point Harmony Mobile Protect available to end users

- **Android**  
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [Harmony Mobile Protect - Play Store URL](https://play.google.com/store/apps/details?id=com.lacoon.security.fox) when completing the **Configure app information** section. 

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [Harmony Mobile Protect - App Store URL](https://apps.apple.com/us/app/sandblast-mobile-protect/id1006390797) when completing the **Configure app information** section.

### Making Lookout for Work available to end users

- **Android**  
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [Lookout for Work - Play Store URL](https://play.google.com/store/apps/details?id=com.lookout.enterprise) when completing the **Configure app information** section.

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [Lookout for Work - iOS App Store URL](https://itunes.apple.com/us/app/lookout-for-work/id997193468?mt=8) when completing the **Configure app information** section.

### Making MVISION Mobile available to end users

- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [MVISION Mobile - Play Store URL](https://play.google.com/store/apps/details?id=com.mcafee.mvision&hl=en_CA&gl=US) when completing the **Configure app information** section.
- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [MVISION Mobile - App Store URL](https://apps.apple.com/us/app/mcafee-mvision-mobile/id1435156022) when completing the **Configure app information** section.

### Making Symantec Endpoint Protection Mobile available to end users

- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). When completing the **Configure app information** section, use this [SEP Mobile app store URL](https://play.google.com/store/apps/details?id=com.skycure.skycure). For **Minimum operating system**, select **Android 4.0 (Ice Cream Sandwich)**.

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [SEP Mobile - App Store URL](https://itunes.apple.com/us/app/skycure/id695620821?mt=8) when completing the **Configure app information** section.

### Making Wandera available to end users

- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [Wandera Mobile - Play Store URL](https://play.google.com/store/apps/details?id=com.wandera.android) when completing the **Configure app information** section.

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [Wandera Mobile - App Store URL](https://itunes.apple.com/app/wandera/id605469330) when completing the **Configure app information** section.

### Making Zimperium available to end users

- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [Zimperium - Play Store URL](https://play.google.com/store/apps/details?id=com.zimperium.zips&hl=en) when completing the **Configure app information** section.
- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [Zimperium - App Store URL](https://itunes.apple.com/us/app/zimperium-zips/id1030924459?mt=8) when completing the **Configure app information** section.

<!-- ### Making Pradeo available to end users
- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [Pradeo - Play Store URL](https://play.google.com/store/apps/details?id=net.pradeo.service&hl=en_US) when completing the **Configure app information** section.

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [Pradeo - App Store URL](https://itunes.apple.com/us/app/pradeo-agent/id547979360?mt=8) when completing the **Configure app information** section. -->


<!-- ### Making Sophos available to end users
- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [Sophos - Play Store URL](https://play.google.com/store/apps/details?id=com.sophos.smsec) when completing the **Configure app information** section.

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [ActiveShield - App Store URL](https://itunes.apple.com/us/app/sophos-mobile-security/id1086924662?mt=8) when completing the **Configure app information** section.  -->

## Next steps

- [Enable the Mobile Threat Defense connector in Intune for unenrolled devices](mtd-enable-unenrolled-devices.md)
