---
# required metadata

title: Single sign-on (SSO) for iOS/iPadOS and macOS
description: Overview of Microsoft Enterprise SSO plug-in in Microsoft Intune, Jamf Pro and other MDM solution providers. The Enterprise SSO plug-in is available on iOS/iPadOS and macOS devices.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/05/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

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

## Single sign-on (SSO) overview and options for Apple devices in Microsoft Intune

**IN PROGRESS**

Apple devices can use single sign-on (SSO) to access apps and websites. SSO lets users sign in and access multiple apps & websites without entering their credentials each time. This article describes the SSO options available for Apple devices in Microsoft Intune.

Most apps, including Line of Business (LOB) apps, require some level of user authentication to support security. In many cases, the authentication requires users to enter the same credentials repeatedly. To improve the user experience, developers can create apps that use single sign-on (SSO).

SSO provides a better authentication experience for users, and reduces the number of repeated prompts for credentials. On Apple devices, there are features in Intune that provide SSO.

- An app that's coded to look for the user credential store in single sign-on on the device.
- Intune policy

This article applies to:

- iOS/iPadOS
- macOS

::: zone pivot="all,macos"
## Platform SSO

This feature applies to:

- macOS

On macOS devices, users sign in with a local account. Then, they sign into apps and websites with their Microsoft Entra ID.

With platform SSO, users can sign into the device with their Microsoft Entra ID instead of their local account. When they sign into the device with their Microsoft Entra ID, then they get access to device features that use Microsoft Entra ID for authentication.

For more information on platform SSO, go to [Configure platform SSO for macOS devices in Microsoft Intune](platform-sso-macos.md).

You can use platform SSO and the [Microsoft Enterprise SSO plug-in](#microsoft-enterprise-sso-plug---in-for-ios-ipad-and-macos-devices) (in this article) together. Specifically, you:

1. Use platform SSO to sign into the device.
2. Use the SSO app extension to sign into apps and websites.

When combined, users minimize the number of times they need to enter their Entra credentials.

Platform SSO uses the Microsoft Intune [settings catalog](settings-catalog.md) to configure the policy. When the policy is ready, you assign the policy to your users or devices. Microsoft recommends you assign the policy when the device enrolls in Intune. But, it can be assigned at any time, including on existing devices.

### Platform SSO feature summary

The following table summarizes the platform SSO features in Microsoft Intune. Use this information to determine if this SSO option is right for your organization.

| Feature | Details |
| --- | --- |
| **Platform support** | ❌ iOS/iPadOS <br/>✔️ macOS 13.0 and newer|
| **Supported enrollment types** | ✔️ Device enrollment<br/>✔️ Automated Device Enrollment (supervised) <br/>❌ User enrollment <br/>❌ Direct enrollment (Apple Configurator) |
| **Supported authentication types** | ✔️ Microsoft Entra ID <br/> ✔️ Smartcard |
| **Supported app types** | ✔️ Microsoft 365 apps<br/>✔️ Apps, websites or services integrated with Microsoft Entra ID <br/>✔️ Apps, websites or services that support Apple Enterprise SSO and are integrated with on-premises Active Directory |
| **Intune admin center location** | **Devices** > **Configuration** > **Create** > **macOS** for platform > **Settings catalog** for profile type > **Authentication** > **Extensible Single Sign On (SSO)** |
| **Recommendation** | ✔️ Recommended. <br/><br/> You can use platform SSO and the SSO app extension (with the Microsoft Entra SSO plug-in) together. |

::: zone-end

::: zone pivot="all,ios-ipados,macos"
## SSO app extension

This feature applies to:

- iOS/iPadOS
- macOS

In Microsoft Intune, there's an SSO app extension that can use the Microsoft Entra SSO app extension plug-in. This plug-in provides SSO to apps & websites that use Microsoft Entra ID for authentication, including:

- Microsoft 365 apps
- On-premises Active Directory accounts across all apps that support Apple's Enterprise SSO feature

The Microsoft Entra SSO plug-in is a redirect-type SSO app extension. It's available for Microsoft Intune, Jamf Pro, and other MDM solutions. In Intune, the SSO app extension uses a device configuration policy with Microsoft Entra ID as the SSO app extension type.

These settings configure redirect-type and credential-type SSO app extensions:

- The **redirect** type is designed for modern authentication protocols, such as OpenID Connect, OAuth, and SAML2. You can choose between the Microsoft Entra SSO extension ([Microsoft Enterprise SSO plug-in](/azure/active-directory/develop/apple-sso-plugin)) and a generic redirect extension.

- The **credential** type is designed for challenge-and-response authentication flows. You can choose between a Kerberos-specific credential extension provided by Apple, and a generic credential extension.

  The Microsoft Entra macOS SSO app extension should work with any third party or partner MDM. The extension must be deployed as a kerberos SSO extension, or deployed as a custom configuration profile with all the required properties configured.

For more information on the SSO app extension, go to:

- [Use the Microsoft Enterprise SSO plug-in on iOS/iPadOS devices](use-enterprise-sso-plug-in-ios-ipados-with-intune.md)
- [SSO app extension settings list - iOS/iPadOS](ios-device-features-settings.md#single-sign-on-app-extension)
- [Use the Microsoft Enterprise SSO plug-in on macOS devices](use-enterprise-sso-plug-in-macos-with-intune.md)
- [SSO app extension settings list - macOS](macos-device-features-settings.md#single-sign-on-app-extension)

Use this SSO app extension type to enable SSO on Microsoft apps, organization apps, and websites that authenticate using Microsoft Entra ID.

In the Intune policy, you can use a different SSO app extension type. But 

When the policy is ready, you assign the policy to your users. Microsoft recommends you assign the policy when the device enrolls in Intune. But, it can be assigned at any time, including on existing devices.

### SSO app extension feature summary

The following table summarizes the SSO app extension features in Microsoft Intune. Use this information to determine if this SSO option is right for your organization.

| Feature | Details |
| --- | --- |
| **Platform support** | ✔️ iOS/iPadOS 13.0 and newer <br/>✔️ macOS 10.15 and newer|
| **Supported enrollment types** | iOS/iPadOS:<br/>✔️ Device enrollment<br/>✔️ Automated Device Enrollment (supervised) <br/>✔️ User enrollment <br/>✔️ Direct enrollment (Apple Configurator) <br/><br/>macOS: <br/>✔️ User approved device enrollment <br/>✔️ Automated Device Enrollment (supervised)<br/>❌ Direct enrollment (Apple Configurator)|
| **Supported authentication types** | ✔️ Redirect-type SSO app extension, including Microsoft Entra ID <br/> ✔️ Credential app extension <br/> ✔️ Apple's built-in Kerberos extension |
| **Supported app types** | ✔️ Microsoft 365 apps<br/>✔️ Apps, websites or services integrated with Microsoft Entra ID <br/>✔️ Apps, websites or services that support Apple's Enterprise SSO and are integrated with on-premises Active Directory |
| **Intune admin center location** | **Devices** > **Configuration** > **Create** > **iOS/iPadOS** or **macOS** for platform > **Device features** for profile type > **Single sign-on app extension** |
| **Recommendation** | ✔️ Recommended. <br/><br/> On macOS devices, you can use the SSO app extension (with the Enterprise SSO plug-in) and platform SSO together. |

::: zone-end

::: zone pivot="all,ios-ipados"
## Single sign-on

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
| **Platform support** | ✔️ iOS 7.0 and newer<br/>✔️ iPadOS 13.0 and newer <br/> ❌ macOS|
| **Supported enrollment types** | ✔️ Device enrollment<br/>✔️ Automated Device Enrollment (supervised) <br/>❌ User enrollment <br/>❌ Direct enrollment (Apple Configurator)|
| **Supported authentication types** | Can only use Kerberos SSO authentication. <br/> - Enter Kerberos account information for when users access servers or apps. <br/>- Isn't an Apple implementation of Kerberos. <br/>- Handles Kerberos challenges for web pages and apps|
| **Supported app types** | Website and native apps that support Kerberos authentication. App must be coded to look for the user credential store in single sign-on on the device. |
| **Intune admin center location** | **Devices** > **Configuration** > **Create** > **iOS/iPadOS** for platform > **Device features** for profile type > **Single sign-on** |
| **Recommendation** | ❌ Not recommended. Instead, Microsoft recommends using the [SSO app extension](#sso-app-extension) (in this article). |

::: zone-end

## Which option is right for me - in progress

The following table compares the SSO options available for Apple devices in Microsoft Intune. Use this table to help you decide which option is right for you.

| Platform SSO | Single sign-on app extension | Single sign-on |
| --- | --- | --- |
| **Supported platforms**: <br/><br/>- macOS 13.0 and newer | **Supported platforms**:<br/><br/>- iOS/iPadOS 13.0 and newer <br/>- macOS 10.15 and newer | **Supported platforms** <br/><br/>- iOS 7.0 and newer <br/>- iPadOS 13.0 and newer |
| **Supported enrollment types**: <br/><br/>✔️ Device enrollment<br/>✔️ Automated Device Enrollment (supervised) <br/>❌ User enrollment <br/>❌ Direct enrollment (Apple Configurator)| **Supported enrollment types** <br/><br/>**iOS/iPadOS**:<br/>✔️ Device enrollment<br/>✔️ Automated Device Enrollment (supervised) <br/>✔️ User enrollment <br/>✔️ Direct enrollment (Apple Configurator) <br/><br/>**macOS**: <br/>✔️ User approved device enrollment <br/>✔️ Automated Device Enrollment (supervised)<br/>❌ Direct enrollment (Apple Configurator)| **Supported enrollment types** <br/><br/>✔️ Device enrollment<br/>✔️ Automated Device Enrollment (supervised) <br/>❌ User enrollment <br/>❌ Direct enrollment (Apple Configurator)|
| | Define extensions for use by identity providers or organizations to deliver an enterprise SSO experience. | Define Kerberos account information for when users access servers or apps. |
| | Developed by Apple and uses the Apple operating system to authenticate. Can be used to log users into native apps and websites that support Kerberos authentication. | Uses Kerberos to authenticate and isn't an Apple implementation of Kerberos. |
|  | From a development perspective, you can use any type of redirect SSO or credential SSO authentication.  | Can only use Kerberos SSO authentication. |
|  | Handles Kerberos challenges for web pages and apps, supports password changes, and behaves better in enterprise networks | Handles Kerberos challenges for web pages and apps |
| Recommended | Recommended | Not recommended |

## Next steps

- For information about the Microsoft Enterprise SSO plug-in and Microsoft Entra ID, go to [Microsoft Enterprise SSO plug-in for Apple devices](/azure/active-directory/develop/apple-sso-plugin).

- For information from Apple on the single sign-on extension payload, go to [single sign-on extensions payload settings](https://support.apple.com/guide/deployment/single-sign-on-payload-settings-dep7a81f07b/web) (opens Apple's web site).

- For information on troubleshooting the Microsoft Enterprise SSO Extension, go to [Troubleshooting the Microsoft Enterprise SSO Extension plugin on Apple devices](/azure/active-directory/devices/troubleshoot-mac-sso-extension-plugin).
