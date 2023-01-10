---
# required metadata

title: Configure the Microsoft Enterprise SSO plug-in on iOS/iPadOS devices with an MDM
description: Add or create an iOS or iPadOS device profile using the Microsoft Enterprise SSO plug-in in an MDM. 
keywords:
author: TBC
ms.author: alessanc
manager: ianfarr
ms.date: 12/12/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection: M365-identity-device-management
---

# Configure the Microsoft Enterprise SSO plug-in on iOS/iPadOS devices with a Mobile Device Management solution (MDM)

[!INCLUDE [Apple SSO Boilerplate](../includes/apple-enterprise-sso-intro-boilerplate.md)]

This feature applies to:

- iOS/iPadOS

This article explains how to deploy the Microsoft Enterprise SSO plug-in (preview) for iOS/iPadOS Devices with a generic MDM solution.

[!INCLUDE [Apple SSO Disclaimer Boilerplate](../includes/apple-enterprise-sso-disclaimer-boilerplate.md)]

## Prerequisites

To use the Microsoft Enterprise SSO plug-in for Apple devices:

- The device must be managed (MDM)
- The MDM solution must support configuring [Single Sign-on MDM payload settings for Apple devices](https://support.apple.com/guide/deployment/extensible-single-sign-on-payload-settings-depfd9cdf845/web) with a device policy
- The device must support the plug-in:
  - iOS/iPadOS 13.0 and newer
- Microsoft Authenticator app installed on the device.
  - The Microsoft Authenticator app can be installed manually by users, or deployed with an MDM.

> [!NOTE]
> On iOS and iPadOS devices, Apple requires that the SSO app extension and the Microsoft Authenticator app be installed. Users don't need to use or configure the Microsoft Authenticator app, it just needs to be installed on the device.

[!INCLUDE [Apple Kerberos Extension Boilerplate](../includes/apple-enterprise-sso-kerberos-boilerplate.md)]

---

For more information on the single sign-on extension, see [Single sign-on app extension](device-features-configure.md#single-sign-on-app-extension).

## Create a single sign-on app extension device configuration profile

In the MDM portal, you will create a Device Configuration profile. This profile includes the settings to configure the SSO app extension on devices.

1. Sign in to the MDM portal.
2. Create a new Device Configuration profile
3. Select an option called **Single Sign-On Extensions** or **SSO extension**. The name may vary depending on your MDM of choice.
4. Enter the following properties:

    | **Key** | **Value** |
    | --- | --- |
    | Payload Type | SSO |
    | Extension Identifier | com.microsoft.azureauthenticator.ssoextension |
    | Sign-On Type | **Redirect** |
    | URLs | - `https://login.microsoftonline.com` <br/> - `https://login.microsoft.com` <br/> - `https://sts.windows.net` <br/> - `https://login.partner.microsoftonline.cn` <br/> - `https://login.chinacloudapi.cn` <br/> - `https://login.microsoftonline.us` <br/> - `https://login.usgovcloudapi.net` <br/> - `https://login-us.microsoftonline.com` |

5. Optionally you can configure other properties. The properties below reflect the defaults used by the SSO Extension, but they may be customized to suit your needs:

    [!INCLUDE [Apple SSO Recommended Settings Table Boilerplate](../includes/apple-enterprise-sso-recommended-settings-intune-and-generic-mdm-boilerplate.md)]

6. Assign the new policy to the devices that should be targeted to receive the SSO Extension MDM profile.

When the device checks in with the MDM service, it receives this profile.

[!INCLUDE [Apple iOS End User Experience Boilerplate](../includes/apple-enterprise-sso-ios-end-user-experience-boilerplate.md)]

## Next steps

- For information about the Microsoft Enterprise SSO plug-in, see [Microsoft Enterprise SSO plug-in for Apple devices (preview)](/azure/active-directory/develop/apple-sso-plugin).

- For information from Apple on the single sign-on extension payload, see [Single Sign-On Extensions payload settings](https://support.apple.com/guide/mdm/single-sign-on-extensions-mdmfd9cdf845/web) (opens Apple's web site).
