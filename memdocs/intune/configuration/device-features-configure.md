---
# required metadata

title: Create iOS/iPadOS or macOS device profile with Microsoft Intune
description: Add or create an iOS, iPadOS, or macOS device profile. Configure settings for AirPrint, layout of the home screen, app notifications, shared device, single sign-on, and web content filter settings in Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/17/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
# optional metadata

#ROBOTS:
#audience:

ms.reviewer: beflamm, arnab
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Add iOS, iPadOS, or macOS device feature settings in Intune

Intune includes many features and settings that help administrators control iOS, iPadOS, and macOS devices. For example, administrators can:

- Allow users access to AirPrint printers in your network
- Add apps and folders to the home screen, including adding new pages
- Choose if and how app notifications are shown
- Configure the lock screen to show a message or the asset tag, especially for shared devices
- Give users a secure single sign-on experience to share credentials between apps
- Filter web sites that use adult language and allow or block specific web sites

Intune uses "configuration profiles" to create and customize these settings for your organization's needs. After you add these features in a profile, you then push or deploy the profile to iOS/iPadOS and macOS devices in your organization.

This feature applies to:

- iOS/iPadOS
- macOS

This article describes the different features you can configure, and shows you how to create a device configuration profile. You can also see all the available settings for [iOS/iPadOS](ios-device-features-settings.md) and [macOS](macos-device-features-settings.md) devices.

## Create the profile

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy**.
3. Enter the following properties:

    - **Platform**: Select your platform:

        - **iOS/iPadOS**
        - **macOS**

    - **Profile type**: Select **Templates** > **Device features**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, a good policy name is **macOS: Configures login screen**.
    - **Description**: Enter a description for the policy. This setting is optional, but recommended.

6. Select **Next**.

7. In **Configuration settings**, depending on the platform you chose, the settings you can configure are different. Choose your platform for detailed settings:

    - [iOS/iPadOS](ios-device-features-settings.md)
    - [macOS](macos-device-features-settings.md)

8. Select **Next**.
9. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, go to [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

10. In **Assignments**, select the users or groups that will receive your profile. For more information on assigning profiles, go to [Assign user and device profiles](device-profile-assign.md).

    Select **Next**.

11. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

## Airprint

Airprint is an Apple feature that allows devices to print to files over a wireless network. In Intune, you can add AirPrint information to devices.

For a list of the settings you can configure in Intune, go to [AirPrint on iOS/iPadOS](ios-device-features-settings.md#airprint) and [AirPrint on macOS](macos-device-features-settings.md#airprint).

For more information on AirPrint, go to [About AirPrint](https://support.apple.com/HT201311) on Apple's web site.

Applies to:

- iOS 7.0 and newer
- iPadOS 13.0 and newer
- macOS 10.10 and newer

## App notifications

Choose how apps on your iOS and iPadOS devices receive notifications. For example, send app notifications so they show in the notification center, show on the lock screen, or play a sound.

For a list of the settings you can configure in Intune, go to [App notifications on iOS/iPadOS](ios-device-features-settings.md#app-notifications).

For more information on this feature, go to [Notifications](https://developer.apple.com/notifications/) on Apple's web site.

Applies to:

- iOS 9.3 and newer
- iPadOS 13.0 and newer

## Associated domains

Associated domains allow you to create a relationship between your domains, such as `contoso.com`, and your apps. This feature allows you to:

- Share data and sign in credentials between apps and websites in your organization.
- Use app features that are based on your website, such as single sign-on app extension, universal links, and password autofill.

  For example, create an associated domain to allow password autofill to recommend credentials, such as a password, for websites associated with your app.

For a list of the settings you can configure in Intune, go to [Associated domains on macOS](macos-device-features-settings.md#associated-domains).

For more information on this feature, go to [Setting Up an App's Associated Domains](https://developer.apple.com/documentation/security/password_autofill/setting_up_an_app_s_associated_domains) on Apple's web site.

Applies to:

- macOS 10.15 and newer

## Home screen layout

These settings configure the app layout and folders on the home screen and dock. You can also see in real time how most apps and their icons look. Specifically:

- Use the **Home screen** settings to add apps and folders to the home screen on devices.
- Use the **Dock** settings to add apps or folders to the dock on the screen. For example, show Safari and the Mail app on the device dock.

For a list of the settings you can configure in Intune, go to [Home screen layout on iOS/iPadOS](ios-device-features-settings.md#home-screen-layout).

Applies to:

- iOS 9.3 and newer
- iPadOS 13.0 and newer

## Lock screen message

Use these settings to show a custom message or text on the sign in window and lock screen. For example, you can enter an "If lost, return to ..." message, and show asset tag information.

For a list of the settings you can configure in Intune, go to [Lock screen message settings on iOS/iPadOS](ios-device-features-settings.md#lock-screen-message).

For more information on Lock Screen Message, go to [LockScreenMessage](https://developer.apple.com/documentation/devicemanagement/lockscreenmessage) on Apple's web site.

Applies to:

- iOS 9.3 and newer
- iPadOS 13.0 and newer

## Login items

Use this feature to choose the apps, custom apps, files, and folders that open when users sign in to the devices.

For a list of the settings you can configure in Intune, go to [Login items on macOS](macos-device-features-settings.md#login-items).

Applies to:

- macOS 10.13 and newer

## Login window

Control the appearance of the sign in screen and functions available to users before they sign in. For example, add a banner with a custom message, choose if the sleep button is shown, and more.

For a list of the settings you can configure in Intune, go to [Login window on macOS](macos-device-features-settings.md#login-window).

Applies to:

- macOS 10.7 and newer

## Single sign-on (SSO)

Microsoft Intune has different types of single sign-on (SSO) options for iOS/iPadOS and macOS devices. Specifically:

- **Platform SSO** (recommended)

  Applies to:

  - macOS 13.0 and newer

  This feature is part of the [Microsoft Enterprise SSO plug-in](/entra/identity-platform/apple-sso-plugin) in Microsoft Entra ID. It enables single sign-on (SSO) using passwordless authentication, Microsoft Entra user accounts, and smart cards. Users can also manually sign into their macOS devices using their Microsoft Entra account, instead of a local account.

  In Intune, you create an Intune settings catalog policy and configure the Platform SSO settings.

  For more information on Platform SSO, go to:

  - [Configure Platform SSO for macOS devices in Microsoft Intune](platform-sso-macos.md)
  - [Single sign-on (SSO) overview and options for Apple devices in Microsoft Intune](use-enterprise-sso-plug-in-ios-ipados-macos.md)

- **SSO app extension** (recommended)

  Applies to:

  - iOS 13.0 and newer
  - iPadOS 13.0 and newer
  - macOS 10.15 and newer

  This feature is part of the [Microsoft Enterprise SSO plug-in](/entra/identity-platform/apple-sso-plugin) in Microsoft Entra ID. It allows iOS/iPadOS and macOS users to sign into apps and websites using Microsoft Entra ID.

  In Intune, you create an Intune device features configuration policy and configure the SSO app extension settings.

  For more information, go to:

  - [Single sign-on (SSO) overview and options for Apple devices in Microsoft Intune](use-enterprise-sso-plug-in-ios-ipados-macos.md)
  - [SSO app extension on iOS/iPadOS devices](use-enterprise-sso-plug-in-ios-ipados-with-intune.md)
  - [SSO app extension on macOS devices](use-enterprise-sso-plug-in-macos-with-intune.md)

  For more information on developing an SSO app extension, watch [Extensible Enterprise SSO](https://developer.apple.com/videos/play/tech-talks/301) on Apple's web site. To read Apple's description of the feature, go to [single sign-on extensions payload settings](https://support.apple.com/guide/deployment/single-sign-on-payload-settings-dep7a81f07b/web).

- **Single sign-on**

  Applies to:

  - iOS 7.0 and newer
  - iPadOS 13.0 and newer

  > [!NOTE]
  > Instead of these SSO settings, Apple recommends you use the SSO app extension.

  Restricted to only Kerberos authentication. Kerberos is a network authentication protocol that uses secret key cryptography to authenticate client-server applications. In an Intune policy, you enter the Kerberos account information that accesses servers or specific apps, like the Microsoft Entra username attribute.

  To use single sign-on, your app must be coded to look for the user credential store in single sign-on on the device.

  For a list of the settings you can configure in Intune, go to [Single sign-on on iOS/iPadOS](ios-device-features-settings.md#single-sign-on).

## Wallpaper

Add a custom .png, .jpg, or .jpeg image to your supervised iOS/iPadOS devices. For example, use Intune to add a company logo to the lock screen on your devices.

For a list of the settings you can configure in Intune, go to [Wallpaper on iOS/iPadOS](ios-device-features-settings.md#wallpaper).

Applies to:

- iOS
- iPadOS 13.0 and newer

## Web content filter

These settings use Apple's built-in AutoFilter algorithm to evaluate web pages, and block adult content and adult language. You can also create a list of allowed web links and restricted web links. For example, you can allow only `contoso` web sites to open.

For a list of the settings you can configure in Intune, go to [Web content filter on iOS/iPadOS](ios-device-features-settings.md#web-content-filter).

Applies to:

- iOS 7.0 and newer
- iPadOS 13.0 and newer

## Related content

- [Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).
- View all the device feature settings for [iOS/iPadOS](ios-device-features-settings.md) and [macOS](macos-device-features-settings.md) devices.
