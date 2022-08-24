---
# required metadata

title: Manage and secure apps in Endpoint Manager
titleSuffix: Microsoft Endpoint Manager
description: Learn more about the concepts and features you should know when managing apps that access organization resources in Microsoft Intune and Endpoint Manager. You can manage new and existing devices, including BYOD personal devices, check health compliance and view reports, configure device features, and secure devices using mobile threat solutions.
keywords:
author: MandiOhlinger
  
ms.author: mandia
manager: dougeby
ms.date: 08/24/2022
ms.topic: conceptual
ms.service: mem
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 
# optional metadata
 
#audience:
#ms.devlang:
ms.reviewer:
ms.suite: ems
search.appverid:
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
  - M365-identity-device-management
---

# Manage your apps and app data in Microsoft Endpoint Manager

> [!NOTE]
> This is a draft of an idea. It's meant to be 100-level with an introduction to some concepts that decision makers need to be aware.

https://review.docs.microsoft.com/en-us/mem/manage-identities?branch=draft-intune-toc

app protect policies require Azure AD

MDM or MAM or both

This article applies to:

- Android
- iOS/iPadOS
- macOS
- Windows

## Deploy apps your organization uses

Organizations use many different types of apps, including store apps, line-of-business (LOB) apps, web apps, and more. You can add apps to Endpoint Manager and then use its app policy management to deploy these apps to your devices.

The app features in the Endpoint Manager admin center makes it easier to deploy these different kinds of apps. Endpoint Manager supports Android, iOS/iPadOS, macOS, and Windows client devices:

- For **Android** devices, the admin center automatically connects to the public Play Store and gives you the ability to search for apps. You can also sync with your Managed Google Play account.

  If you use [Google Mobile Services (GMS)](https://www.android.com/gms/) (opens Android's web site), you can purchase licenses to GMS, which typically happens when you purchase Android devices. GMS gives users access to the public Play Store and its public apps.

  On Android devices, you can deploy:

  - Public apps from the public Play Store
  - Managed Google Play apps to Android Enterprise devices
  - Web links to web apps
  - Built-in apps, which are apps automatically included and available in the Endpoint Manager admin center
  - Custom line-of-business apps your organization creates
  - Android Enterprise system apps, which are apps that are typically included on Android devices

  If your organization doesn't use [Google Mobile Services (GMS)](https://www.android.com/gms/) (opens Android's web site), then you can also manage devices using the Android Open Source Project (AOSP) platform.

  For more specific information, go to:

  - [How to use Intune in environments without Google Mobile Services](./intune/apps/manage-without-gms.md)
  - [Add Managed Google Play apps to Android Enterprise devices](./intune/apps/apps-add-android-for-work.md)
  - [Manage private Android apps in Google Play](https://support.google.com/a/answer/2494992) (opens Google's web site)
  - [Add built-in apps](./intune/apps/apps-add-built-in.md)

- For **iOS/iPadOS** devices, the admin center automatically connects to the public App Store and gives you the ability to search for apps. You can also sync with your Apple Business Manager or Apple School Manager account. When you sync, the apps your purchase are automatically shown in the admin center.

  On iOS/iPadOS devices, you can deploy:

  - Free apps from the public App Store
  - Paid apps using Apple Business Manager or Apple School Manager
  - Web clips, which are shortcuts to web site links that you can add to the home screen
  - Web links to web apps
  - Built-in apps, which are apps automatically included and available in the Endpoint Manager admin center
  - Custom line-of-business apps your organization creates

  For more specific information, go to:

  - [Add iOS store apps](./intune/apps/store-apps-ios.md)
  - [Manage iOS/iPadOS and macOS apps purchased through Apple Business Manager](./intune/apps/vpp-apps-ios.md)
  - [Add iOS/iPadOS LOB apps](./intune/apps/lob-apps-ios.md)
  - [Add built-in apps](./intune/apps/apps-add-built-in.md)

- For **macOS** devices, the built-in features include apps commonly deployed to macOS, including Microsoft Edge and Microsoft 365 apps. You can also sync with your Apple Business Manager or Apple School Manager account. When you sync, the apps your purchase are automatically shown in the admin center.

  On macOS devices, you can deploy:

  - Paid apps using Apple Business Manager or Apple School Manager
  - Microsoft 365 apps, which includes Word, Excel, PowerPoint, Outlook, OneNote, Teams, and OneDrive
  - Microsoft Edge version 77 and newer, which is the modern chromium version
  - Microsoft Defender for Endpoint, which is cloud service that detects malicious intent and can help remediate security threats
  - Web links to web apps
  - Custom line-of-business apps your organization creates
  - Apple disk image (DMG) apps, which is a disk image file that includes one or more apps that's deployed not using the App Store

  For more specific information, go to:

  - [Manage iOS/iPadOS and macOS apps purchased through Apple Business Manager](./intune/apps/vpp-apps-ios.md)
  - [Assign Microsoft 365 to macOS devices](./intune/apps/apps-add-office365-macOS.md)
  - [Add macOS LOB apps](./intune/apps/lob-apps-macos.md)

- For **Windows** devices, you can use the Endpoint Manager admin center to deploy:

  - Microsoft Store apps
  - Microsoft 365 apps, which includes Word, Excel, PowerPoint, Outlook, OneNote, Teams, and OneDrive
  - Microsoft Edge version 77 and newer, which is the modern chromium version
  - Web links to web apps
  - Custom line-of-business apps your organization creates
  - Win32 apps

  For more specific information, go to:

## Configure apps before they're installed

When an app is deployed to your users and devices, your users may be prompted for configuration information. Users might not know what to enter or you may have organization settings you want.

App configuration policies give you these features. You can create an app configuration policy that automatically configures the app for users. Users don't need to enter any configuration information.

For example, in an app configuration policy, you can enter the app language, add your organization's logo, only allowed organization user accounts, and more.
**TO DO**: Need more real-world examples

Your app configuration policies can be deployed at anytime. If you want to configure apps before users open them the first time, then you can include the app configuration policy when users enroll their devices. During enrollment, your app configuration policies are automatically deployed and the apps include your configuration settings.

**TO DO**: Configure apps on enrolled and not enrolled devices?

For more specific information, go to [App configuration policies in Endpoint Manager](./intune/apps/app-configuration-policies-overview.md).

## Protect apps on organization owned and personal devices

App protection policies are a key part to protecting data in apps that access organization data. If user-owned personal devices are accessing your organization data, then you need app protect policies. You can use these policies to protect email, shared files, access to meetings, and more.

You can use Endpoint Manager to create, configure, and deploy app protection policies to your users and your devices, including personally owned devices and devices managed by another MDM provider. Typically, organization owned devices are managed by your organization. If there are apps on these managed devices that require extra security, then you can also use app protection policies on these devices.

App protection policies also help separate personal data from organization data. For example, you can create policies that block copy-and-paste between apps, require a PIN when opening an app, block backups to personal cloud services, and more.

For more specific information, go to:

- [App protection policies overview and benefits](./intune/apps/app-protection-policy.md)
- [How to create and assign app protection policies](./intune/apps/app-protection-policies.md)

## Update apps to the latest version

Apps are often updated to include bug fixes, feature improvements, security updates, and more. When apps are deployed using Endpoint Manager, most apps are automatically updated when there's an app update available. So, it's recommended to use Endpoint Manager to deploy apps used by your organization.

If users install apps themselves, including from an app store, then these apps will need updated manually. In this situation, you can use app protection policies to enforce a minimum app version, and even wipe organization data on devices that don't meet your standards.

For more information, go to:

- [Add and update apps](./intune/apps/apps-add.md)
- [Wipe corporate data from Intune-managed apps](./intune/apps/apps-selective-wipe.md)
- [Selectively wipe data using app protection policy conditional launch actions](./intune/apps/app-protection-policies-access-actions.md)

## Next steps

- [Manage identities](manage-identities.md)
- [Manage devices](manage-devices.md)
