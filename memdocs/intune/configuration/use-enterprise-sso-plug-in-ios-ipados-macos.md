---
# required metadata

title: Single sign-on (SSO) for iOS/iPadOS and macOS
description: Overview of Microsoft Enterprise SSO plug-in in Microsoft Intune, Jamf Pro, and other MDM solution providers. The Enterprise SSO plug-in is available on iOS/iPadOS and macOS devices.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/11/2024
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
zone_pivot_groups: apple-enterprise-sso
---

# Single sign-on (SSO) overview and options for Apple devices in Microsoft Intune

> [!IMPORTANT]
> This article is a final draft and ready for PM review. It will go live when Platform SSO goes live. **Delete this note before publishing**.

Apple devices can use single sign-on (SSO) to access devices, apps, and websites using their Microsoft Entra ID. SSO lets users sign in and get access without entering their credentials each time.

This article applies to:

- iOS/iPadOS
- macOS

To support security, devices and most apps, including Line of Business (LOB) apps, require some level of user authentication. In many cases, the authentication requires users to enter the same credentials repeatedly. To improve the end user experience, admins can deploy SSO policies and developers can create apps that use single sign-on (SSO).

There are three SSO options available for Apple devices in Microsoft Intune:

- **[Platform SSO](#platform-sso)** (macOS only) - Part of the [Microsoft Enterprise SSO plug-in](/entra/identity-platform/apple-sso-plugin) in Microsoft Entra ID
- **[SSO app extension](#sso-app-extension)** (iOS/iPadOS, macOS) - Part of the [Microsoft Enterprise SSO plug-in](/entra/identity-platform/apple-sso-plugin) in Microsoft Entra ID
- **[Single sign-on template](#single-sign-on-template)** (iOS/iPadOS only) - A template in Intune

SSO provides a better authentication experience for users, and reduces the number of repeated prompts for credentials. This article describes the SSO options available for Apple devices in Microsoft Intune.

::: zone pivot="all,macos"
## Platform SSO

This feature applies to:

- macOS

The [Microsoft Enterprise SSO plug-in](/entra/identity-platform/apple-sso-plugin) includes two SSO features - **Platform SSO** and the **SSO app extension**. This section focuses on **Platform SSO**.

On macOS devices, users normally sign in with a local account. Then, they sign into apps and websites with their Microsoft Entra ID.

With Platform SSO:

- End users get a better and more security experience by using Microsoft Entra ID integration with the Microsoft Enterprise SSO plug-in.
- Organization choose the authentication method that meets their business need, including passwordless authentication, Microsoft Entra user account sync, or smart card authentication.
- End users get a single sign-on experience with the SSO app extension by allowing the use of Touch ID and passkeys with Microsoft Entra ID. 

For more information on Platform SSO, go to [Configure Platform SSO for macOS devices in Microsoft Intune](platform-sso-macos.md).

You use Platform SSO and the [SSO app extension](#sso-app-extension) (in this article) together. Specifically, you:

1. Use the SSO app extension to sign into apps and websites with Microsoft Entra ID.
2. Use Platform SSO to enhance the SSO capabilities with different authentication methods. 

With these features, users can sign in with their Microsoft Entra credentials and minimize the number of times they need to enter their Microsoft Entra credentials.

### Platform SSO feature summary

The following table summarizes the Platform SSO features in Microsoft Intune. Use this information to determine if Platform SSO is right for your organization.

| Feature | Details |
| --- | --- |
| **Platform support** | ❌ iOS/iPadOS <br/>✅ macOS 13.0 and newer|
| **Supported enrollment types** | ✅ Device enrollment<br/>✅ Automated Device Enrollment (supervised) <br/>❌ User enrollment <br/>✅ Direct enrollment (Apple Configurator) |
| **Supported authentication types** | ✅ Passwordless <br/> ✅ Microsoft Entra ID <br/> ✅ Smartcard |
| **Supported app types** | ✅ Microsoft 365 apps<br/>✅ Apps, websites or services integrated with Microsoft Entra ID <br/>✅ Apps, websites or services that support Apple Enterprise SSO and are integrated with on-premises Active Directory |
| **Intune admin center location** | **Devices** > **Configuration** > **Create** > **macOS** for platform > **Settings catalog** for profile type > **Authentication** > **Extensible Single Sign On (SSO)** |
| **Recommendation** | ✅ Recommended. <br/><br/> You use Platform SSO and the SSO app extension together. You can use the SSO app extension on its own. To use Platform SSO, you must use only Platform SSO as it includes the SSO app extension settings. |

::: zone-end

::: zone pivot="all,ios-ipados,macos"
## SSO app extension

This feature applies to:

- iOS/iPadOS
- macOS

The [Microsoft Enterprise SSO plug-in](/entra/identity-platform/apple-sso-plugin) includes two SSO features - **Platform SSO** and the **SSO app extension**. This section focuses on the **SSO app extension**.

The SSO app extension provides SSO to apps and websites that use Microsoft Entra ID for authentication, including:

- Microsoft 365 apps
- On-premises Active Directory accounts across all apps that support Apple's Enterprise SSO feature
- An app that's coded to look for the user credential store in single sign-on on the device

The SSO app extension is a redirect-type SSO app extension. It's available for Microsoft Intune, Jamf Pro, and other MDM solutions. In Intune, the SSO app extension uses a device configuration policy with Microsoft Entra ID as the SSO app extension type.

These settings configure redirect-type and credential-type SSO app extensions. Specifically:

- The **redirect** type is designed for modern authentication protocols, such as OpenID Connect, OAuth, and SAML2. You can choose between the Microsoft Entra SSO extension ([Microsoft Enterprise SSO plug-in](/azure/active-directory/develop/apple-sso-plugin)) and a generic redirect extension.

- The **credential** type is designed for challenge-and-response authentication flows. You can choose between a Kerberos-specific credential extension provided by Apple, and a generic credential extension.

  The SSO app extension should work with any non-Microsoft or partner MDM. The extension must be deployed as a kerberos SSO extension, or deployed as a custom configuration profile with all the required properties configured.

For more information on the SSO app extension, go to:

- [Use the Microsoft Enterprise SSO plug-in on iOS/iPadOS devices in Intune](use-enterprise-sso-plug-in-ios-ipados-with-intune.md)
- [SSO app extension settings list - iOS/iPadOS in Intune](ios-device-features-settings.md#single-sign-on-app-extension)
- [Use the Microsoft Enterprise SSO plug-in on macOS devices in Intune](use-enterprise-sso-plug-in-macos-with-intune.md)
- [SSO app extension settings list - macOS in Intune](macos-device-features-settings.md#single-sign-on-app-extension)

### SSO app extension feature summary

The following table summarizes the SSO app extension features in Microsoft Intune. Use this information to determine if this SSO option is right for your organization.

| Feature | Details |
| --- | --- |
| **Platform support** | ✅ iOS/iPadOS 13.0 and newer <br/>✅ macOS 10.15 and newer|
| **Supported enrollment types** | iOS/iPadOS:<br/>✅ Device enrollment<br/>✅ Automated Device Enrollment (supervised) <br/>✅ User enrollment <br/>✅ Direct enrollment (Apple Configurator) <br/><br/>macOS: <br/>✅ User approved device enrollment <br/>✅ Automated Device Enrollment (supervised)<br/>✅ Direct enrollment (Apple Configurator)|
| **Supported authentication types** | ✅ Redirect-type SSO app extension, including Microsoft Entra ID <br/> ✅ Credential app extension <br/> ✅ Apple's built-in Kerberos extension |
| **Supported app types** | ✅ Microsoft 365 apps<br/>✅ Apps, websites or services integrated with Microsoft Entra ID <br/>✅ Apps, websites or services that support Apple's Enterprise SSO and are integrated with on-premises Active Directory |
| **Intune admin center location** | **Devices** > **Configuration** > **Create** > **iOS/iPadOS** or **macOS** for platform > **Device features** for profile type > **Single sign-on app extension** |
| **Recommendation** | ✅ Recommended. <br/><br/> On macOS devices, you can use the SSO app extension by itself. If you're also using Platform SSO for macOS, then you don't need the SSO app extension since it is included in the Platform SSO configuration. |

::: zone-end

::: zone pivot="all,ios-ipados"
## Single sign-on template

> [!NOTE]
> Instead of these SSO settings, Apple recommends you use the [SSO app extension](#sso-app-extension) (in this article).

Applies to:

- iOS 7.0 and newer
- iPadOS 13.0 and newer

This single sign-on policy is based on Kerberos. Kerberos is a network authentication protocol that uses secret key cryptography to authenticate client-server applications. The Intune policy settings define Kerberos account information when accessing servers or specific apps, and handle Kerberos challenges for web pages and native apps.

For a list of the settings you can configure in Intune, go to [Single sign-on on iOS/iPadOS](ios-device-features-settings.md#single-sign-on).

To use single sign-on, be sure you have:

- An app that's coded to look for the user credential store in single sign-on on the device.
- Intune configured for iOS/iPadOS device single sign-on.

### Single sign-on feature summary

The following table summarizes the Single sign-on features in Microsoft Intune. Use this information to determine if this SSO option is right for your organization.

| Feature | Details |
| --- | --- |
| **Platform support** | ✅ iOS 7.0 and newer<br/>✅ iPadOS 13.0 and newer <br/> ❌ macOS|
| **Supported enrollment types** | ✅ Device enrollment<br/>✅ Automated Device Enrollment (supervised) <br/>❌ User enrollment <br/>❌ Direct enrollment (Apple Configurator)|
| **Supported authentication types** | Can only use Kerberos SSO authentication. <br/> - Enter Kerberos account information for when users access servers or apps. <br/>- Isn't an Apple implementation of Kerberos. <br/>- Handles Kerberos challenges for web pages and apps|
| **Supported app types** | Website and native apps that support Kerberos authentication. App must be coded to look for the user credential store in single sign-on on the device. |
| **Intune admin center location** | **Devices** > **Configuration** > **Create** > **iOS/iPadOS** for platform > **Device features** for profile type > **Single sign-on** |
| **Recommendation** | ❌ Not recommended. Instead, Microsoft recommends using the [SSO app extension](#sso-app-extension) (in this article). |

::: zone-end

## SSO app extension vs SSO template

The **Single sign-on app extension** feature is different than the **Single sign-on** feature. Use the following table to compare.

| | Single sign-on app extension | Single sign-on |
| --- | --- | --- |
| **Supported platforms** | ✅ iOS/iPadOS 13.0 and newer <br/>✅ macOS 10.15 and newer | ✅ iOS 7.0 and newer <br/>✅ iPadOS 13.0 and newer <br/>❌ macOS |
| **Description** | Define extensions for use by identity providers or organizations to deliver a seamless enterprise sign-on experience. It uses the Apple operating system to authenticate. | Define Kerberos account information for when users access servers or apps. |
| **Authentication** | From an app development perspective, can use any type of redirect SSO or credential SSO authentication. | From an app development perspective, can only use Kerberos SSO authentication. |
| **Apple implementation** | Developed by Apple and built into the iOS/iPadOS 13.0+ and macOS 10.15+ platforms. The built-in Kerberos extension can be used to log users into native apps and websites that support Kerberos authentication. | Not an Apple implementation of Kerberos. |
| **Recommendation** | Recommended. <br/><br/>Provides an improved end-user experience. It handles Kerberos challenges for web pages, supports password changes, and behaves better in enterprise networks. <br/><br/> When deciding to use Kerberos in the **SSO app extension** or **Single sign-on** template, we recommend using the SSO app extension due to improved performance and capabilities.| Not recommended. <br/><br/>It handles Kerberos challenges for web pages. |

## Related articles

- For information about the Microsoft Enterprise SSO plug-in and Microsoft Entra ID, go to [Microsoft Enterprise SSO plug-in for Apple devices](/azure/active-directory/develop/apple-sso-plugin).

- For information from Apple on the single sign-on extension payload, go to [single sign-on extensions payload settings](https://support.apple.com/guide/deployment/single-sign-on-payload-settings-dep7a81f07b/web) (opens Apple's web site).

- For information on troubleshooting the Microsoft Enterprise SSO Extension, go to [Troubleshooting the Microsoft Enterprise SSO Extension plugin on Apple devices](/azure/active-directory/devices/troubleshoot-mac-sso-extension-plugin).
