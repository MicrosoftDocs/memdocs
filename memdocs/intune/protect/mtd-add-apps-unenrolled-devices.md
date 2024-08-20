---
# required metadata

title: Add Mobile Threat Defense apps to unenrolled devices
titleSuffix: Microsoft Intune
description: Add Mobile Threat Defense apps to unenrolled devices by device users.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/20/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: demerson
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection:
- tier2
- M365-identity-device-management
- sub-mtd-apps
---

# Add Mobile Threat Defense apps to unenrolled devices

By default, when using Intune app protection policies with Mobile Threat Defense, Intune does the work to guide the end user on their device to install and sign in to all required apps to enable the connections with the relevant services.

End users need the Microsoft Authenticator (iOS) to register their device, and the Mobile Threat Defense (both Android and iOS) to receive notifications when a threat is identified in their mobile devices, and to receive guidance to remediate the threats.

Optionally, you can use Intune to add and deploy the Microsoft Authenticator, and Mobile Threat Defense (MTD) apps as well.

[!INCLUDE [mtd-mam-note](../../intune/protect/includes/mtd-mam-note.md)]
>
> For unenrolled devices, you **do not need an iOS app configuration policy** that sets up the Mobile Threat Defense for iOS app you use with Intune. This is a key difference compared to Intune enrolled devices.

## Configure Microsoft Authenticator for iOS via Intune (optional)

When using Intune app protection policies with Mobile Threat Defense, Intune guides the end user to install, sign in to, and register their device with the Microsoft Authenticator (iOS).

However, should you wish to make the app available to end users via the Intune Company Portal, see the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [Microsoft Authenticator - iOS App Store URL](https://itunes.apple.com/us/app/microsoft-authenticator/id983156458?mt=8) when completing the **Configure app information** section. Don't forget to [assigning app to groups with Intune](../apps/apps-deploy.md) as the final step.

> [!NOTE]
> For iOS devices, you need the [Microsoft Authenticator](/azure/multi-factor-authentication/end-user/microsoft-authenticator-app-how-to) so users can have their identities checked by Microsoft Entra. The Intune Company Portal works as the broker on Android devices so users can have their identities checked by Microsoft Entra.

## Making Mobile Threat Defense apps available via Intune (optional)

When you use Intune app protection policies with Mobile Threat Defense, Intune guides the end user to install and sign in to the required Mobile Threat Defense client app.

However, should you wish to make the app available to end users via the Intune Company Portal, you can follow the steps provided in the following sections. Make sure you're familiar with the process of:

- [Adding an app into Intune](../apps/apps-add.md)
- [Assigning an app with Intune](../apps/apps-deploy.md)

### Making Better Mobile available to end users

- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md).

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [ActiveShield - App Store URL](https://itunes.apple.com/us/app/activeshield/id980234260?mt=8&uo=4) when completing the **Configure app information** section.

### Making CylancePROTECT available to end users

- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [CylancePROTECT - Play Store URL](https://play.google.com/store/apps/details?id=com.blackberry.protect) when completing the **Configure app information** section.

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [CylancePROTECT - App Store URL](https://apps.apple.com/us/app/cylanceprotect/id1511209199) when completing the **Configure app information** section.

### Making Check Point Harmony Mobile Protect available to end users

- **Android**  
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [Harmony Mobile Protect - Play Store URL](https://play.google.com/store/apps/details?id=com.lacoon.security.fox) when completing the **Configure app information** section. 

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [Harmony Mobile Protect - App Store URL](https://apps.apple.com/us/app/sandblast-mobile-protect/id1006390797) when completing the **Configure app information** section.

### Making Jamf available to end users

- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [Jamf Trust - Play Store URL](https://play.google.com/store/apps/details?id=com.wandera.android) when completing the **Configure app information** section.

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [Jamf Trust - App Store URL](https://apps.apple.com/us/app/jamf-trust/id1608041266) when completing the **Configure app information** section.

### Making Lookout for Work available to end users

- **Android**  
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [Lookout for Work - Play Store URL](https://play.google.com/store/apps/details?id=com.lookout.enterprise) when completing the **Configure app information** section.

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [Lookout for Work - iOS App Store URL](https://itunes.apple.com/us/app/lookout-for-work/id997193468?mt=8) when completing the **Configure app information** section.

### Making SentinelOne available to end users

- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [SentinelOne - Play Store URL](https://play.google.com/store/apps/details?id=com.sentinelone.mobile) when completing the **Configure app information** section.
- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [SentinelOne - App Store URL](https://apps.apple.com/us/app/sentinelone-mobile/id1567458126) when completing the **Configure app information** section.

### Making Symantec Endpoint Protection Mobile available to end users

- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). When completing the **Configure app information** section, use this [SEP Mobile app store URL](https://play.google.com/store/apps/details?id=com.skycure.skycure). For **Minimum operating system**, select **Android 4.0 (Ice Cream Sandwich)**.

- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [SEP Mobile - App Store URL](https://itunes.apple.com/us/app/skycure/id695620821?mt=8) when completing the **Configure app information** section.

### Making Trellix Mobile Security available to end users

- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [Trellix Mobile Security - Play Store URL](https://play.google.com/store/apps/details?id=com.mcafee.mvision&hl=en_CA&gl=US) when completing the **Configure app information** section.
- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [Trellix Mobile Security - App Store URL](https://apps.apple.com/us/app/mcafee-mvision-mobile/id1435156022) when completing the **Configure app information** section.

### Making Zimperium available to end users

- **Android**
  - See the instructions for [adding Android store apps to Microsoft Intune](../apps/store-apps-android.md). Use this [Zimperium - Play Store URL](https://play.google.com/store/apps/details?id=com.zimperium.zips&hl=en) when completing the **Configure app information** section.
- **iOS**
  - See the instructions for [adding iOS store apps to Microsoft Intune](../apps/store-apps-ios.md). Use this [Zimperium - App Store URL](https://itunes.apple.com/us/app/zimperium-zips/id1030924459?mt=8) when completing the **Configure app information** section.

## Next steps

- [Enable the Mobile Threat Defense connector in Intune for unenrolled devices](mtd-enable-unenrolled-devices.md)
