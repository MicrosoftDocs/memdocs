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
ms.service: 
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

[!INCLUDE [Apple SSO Boilerplate](../includes/apple-enterprise-sso-boilerplate.md)]

## Prerequisites

To use the Microsoft Enterprise SSO plug-in for Apple devices:

- The device must be managed (MDM)
- The MDM solution must support configuring [Single Sign-on MDM payload settings for Apple devices](https://support.apple.com/guide/deployment/extensible-single-sign-on-payload-settings-depfd9cdf845/web) with a device policy
- The device must support the plug-in:
  - iOS/iPadOS 13.0 and newer

- Microsoft Authenticator app installed on the device.

The Microsoft Authenticator app can be installed manually by users, or deployed with an MDM.

> [!NOTE]
> On iOS and iPadOS devices, Apple requires that the SSO app extension and the Microsoft Authenticator app be installed. Users don't need to use or configure the Microsoft Authenticator app, it just needs to be installed on the device.

## Microsoft Enterprise SSO plug-in vs. Kerberos SSO extension

When you use the SSO app extension, you use the **SSO** or **Kerberos** Payload Type for authentication. The SSO app extension is designed to improve the sign-in experience for apps and websites that use these authentication methods.

The Microsoft Enterprise SSO plug-in uses the **SSO** Payload Type with **Redirect** authentication. The SSO Redirect and Kerberos extension types can both be used on a device at the same time. Be sure to create separate device profiles for each extension type you plan to use on your devices.

To determine the correct SSO extension type for your scenario, use the following table:

---
| Microsoft Enterprise SSO plug-in for Apple Devices | Single sign-on app extension with Kerberos |
| --- | --- |
| Uses the **Microsoft Azure AD** SSO app extension type | Uses the **Kerberos** SSO app extension type |
| Supports the following apps: <br/> - Microsoft 365 <br/> - Apps, websites or services integrated with Azure AD | Supports the following apps: <br/><br/> - Apps, websites or services integrated with AD <br/> |

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

5. Optionally you could configure other  properties like

      | Key | Type | Value |
      | --- | --- | --- |
      | **AppPrefixAllowList** | String | Enter a list of prefixes for apps that don't support MSAL **and** are allowed to use SSO. For example, enter `com.microsoft.,com.apple.` to allow all Microsoft and Apple apps.<br/><br/>Be sure these apps [meet the allowlist requirements](/azure/active-directory/develop/apple-sso-plugin#enable-sso-for-apps-that-dont-use-a-microsoft-identity-platform-library).|
      | **browser_sso_interaction_enabled** | Integer | When set to `1`, users can sign in from Safari browser, and from apps that don't support MSAL. Enabling this setting allows users to bootstrap the extension from Safari or other apps.|
      | **disable_explicit_app_prompt** | Integer | Some apps might incorrectly enforce end-user prompts at the protocol layer. If you see this problem, users are prompted to sign in, even though the Microsoft Enterprise SSO plug-in works for other apps. <br/><br/>When set to `1` (one), you reduce these   prompts. |

    > [!TIP]
    > For more information on these properties, and other properties you can configure, see [Microsoft Enterprise SSO plug-in for Apple devices (preview)](/azure/active-directory/develop/apple-sso-plugin#more-configuration-options).

6. Assign the new policy to the devices that should be targeted to receive the SSO Extension MDM profile.

When the device checks in with the MDM service, it receives this profile.

## End user experience

:::image type="content" source="./media/apple-enterprise-sso-plug-in/flow-chart-end-user-iOSiPadOS.png" alt-text="End user flow chart when installing SSO app app extension on iOS/iPadOS devices.":::

- If you're not deploying the Microsoft Authenticator using an app policy, then users must install it manually. Users don't need to use the Authenticator app, it just needs to be installed on the device.

- Users sign in to any supported app or website to bootstrap the extension. Bootstrap is the process of signing in for the first time, which sets up the extension.  

- After users sign in successfully, the extension is automatically used to sign in to any other supported app or website.

You can test Single Sign on by opening Safari in [Private mode](https://support.apple.com/guide/ipad/browse-the-web-privately-ipad8ea0fc1a/ipados) (opens Apple's web site) and opening the site https://portal.office.com, no username and password will be required.
:::image type="content" source="./media/apple-enterprise-sso-plug-in/ipad-sso-animated.gif" alt-text="Animation showing SSO experience on iPadOS":::


## Next steps

- For information about the Microsoft Enterprise SSO plug-in, see [Microsoft Enterprise SSO plug-in for Apple devices (preview)](/azure/active-directory/develop/apple-sso-plugin).

- For information from Apple on the single sign-on extension payload, see [Single Sign-On Extensions payload settings](https://support.apple.com/guide/mdm/single-sign-on-extensions-mdmfd9cdf845/web) (opens Apple's web site).
