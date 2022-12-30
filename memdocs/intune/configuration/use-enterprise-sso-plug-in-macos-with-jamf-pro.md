---
# required metadata

title: Use the Microsoft Enterprise SSO plug-in on macOS devices in Jamf Pro
description: Add or create an macOS device profile using the Microsoft Enterprise SSO plug-in in Microsoft Intune. 
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

# Use the Microsoft Enterprise SSO plug-in on macOS devices in Jamf Pro

The Microsoft Enterprise SSO plug-in (preview) provides single sign-on (SSO) to apps and websites that use Microsoft Azure Active Directory (Azure AD) for authentication, including Microsoft 365. This plug-in uses the Apple single sign-on app extension framework. It reduces the number of authentication prompts users get when using devices managed by Mobile Device Management (MDM), including Jamf Pro.

Once set up, apps that support the Microsoft Authentication Library (MSAL) automatically take advantage of the Microsoft Enterprise SSO plug-in (preview). Apps that don't support MSAL can be allowed to use the extension. Just add the application bundle ID or prefix to the extension configuration.  

For example, to allow a Microsoft app that doesn't support MSAL, add `com.microsoft.` to the **AppPrefixAllowList** property. Be careful with the apps you allow. They can bypass interactive sign-in prompts for the signed in user.

For more information, see [Microsoft Enterprise SSO plug-in for Apple devices - apps that don't use MSAL](/azure/active-directory/develop/apple-sso-plugin#applications-that-dont-use-msal).  

This feature applies to:

- macOS

This article explains how to deploy the Microsoft Enterprise SSO plug-in (preview) for macOS Devices with Jamf Pro.

> [!IMPORTANT]
> The Microsoft Enterprise SSO plug-in for Apple Devices is in public preview. This preview version is provided without a service level agreement (SLA). It's not recommended to use in production. Certain features might not be supported or might have restricted behavior. For more information, see:
>
> - [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)

## Prerequisites

To use the Microsoft Enterprise SSO plug-in for Apple devices:

- The device must be managed via Jamf Pro
- The device must support the plug-in:
  - macOS 10.15 and newer

- Company Portal app installed on the device.

  The Company Portal app can be installed manually by users, or by deploying the app through Jamf Pro. For a list of options on how to install the Company Portal app, see [Jamf Pro's documentation](https://docs.jamf.com/10.24.1/jamf-pro/administrator-guide/Managing_macOS_Installers.html).

> [!NOTE]
> On macOS devices, Apple requires that the Company Portal app be installed. Users don't need to use the Company Portal, the app just need to be installed on the device.
>
> **[Jamf Pro and Intune integration for device compliance](../protect/conditional-access-integrate-jamf.md) is not required to use the SSO app extension.**

## Microsoft Enterprise SSO plug-in vs. Kerberos SSO extension

In Jamf Pro, when you use the SSO app extension, you use the **SSO** or **Kerberos** Payload Type for authentication. The SSO app extension is designed to improve the sign-in experience for apps and websites that use these authentication methods.

The Microsoft Enterprise SSO plug-in uses the **SSO** Payload Type with **Redirect** authentication. The SSO Redirect and Kerberos extension types can both be used on a device at the same time. Be sure to create separate device profiles for each extension type you plan to use on your devices.

To determine the correct SSO extension type for your scenario, use the following table:

---
| Microsoft Enterprise SSO plug-in for Apple Devices | Single sign-on app extension with Kerberos |
| --- | --- |
| Uses the **Microsoft Azure AD** SSO app extension type | Uses the **Kerberos** SSO app extension type |
| Supports the following apps: <br/> - Microsoft 365 <br/> - Apps, websites or services integrated with Azure AD | Supports the following apps: <br/><br/> - Apps, websites or services integrated with AD <br/> |

---

For more information on the single sign-on extension, see [Single sign-on app extension](device-features-configure.md#single-sign-on-app-extension).

## Create a single sign-on app extension configuration profile in Jamf Pro

In the Jamf Pro portal, you create a Computer configuration profile. This profile includes the settings to configure the SSO app extension on devices.

1. Sign in to the Jamf Pro portal.
2. To create a macOS, select **Computers** > **Configuration profiles** > **New**.

    :::image type="content" source="./media/apple-enterprise-sso-plug-in/jamf-pro-configuration-profiles.png" alt-text="In the Jamf Pro portal, create a configuration profile for macOS devices.":::

3. **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, a good policy name is: **Microsoft Enterprise SSO plug-in**.

4. In the **Options** column, scroll down and select **Single Sign-On Extensions** > **Add**.

    :::image type="content" source="./media/apple-enterprise-sso-plug-in/sso-extension-creation.png" alt-text="In the Jamf Pro portal, select the configuration profiles SSO option, and select add.":::

4. Enter the following properties:

    - **Payload Type**: SSO
    - **Extension Identifier**:
      - com.microsoft.CompanyPortalMac.ssoextension
    - **Team Identifier**:
      - UBF8T346G9
    - **Sign-On Type**: Redirect
    - **URLs** (add one by one):
      - `https://login.microsoftonline.com`
      - `https://login.microsoft.com`
      - `https://sts.windows.net`
      - `https://login.partner.microsoftonline.cn`
      - `https://login.chinacloudapi.cn`
      - `https://login.microsoftonline.us`
      - `https://login.usgovcloudapi.net`
      - `https://login-us.microsoftonline.com`

    :::image type="content" source="./media/apple-enterprise-sso-plug-in/sso-extension-basic-settings-1.png" alt-text="In the Jamf Pro portal, see the basic configuration settings part 1.":::

    :::image type="content" source="./media/apple-enterprise-sso-plug-in/sso-extension-basic-settings-2.png" alt-text="In the Jamf Pro portal, see the basic configuration settings part 2.":::

5. In **Custom Configuration**, you'll define other required properties. Jamf Pro requires that these properties are configured using an uploaded PLIST file. To see the full list of configurable properties, go to [Azure AD Apple SSO Extension documentation](/azure/active-directory/develop/apple-sso-plugin#manual-configuration-for-other-mdm-services).

    The following example is a recommended PLIST file that meets the needs of most organizations:

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <plist version="1.0">
    <dict>
        <key>AppPrefixAllowList</key>
        <string>com.microsoft.,com.apple.,com.jamf.,com.jamfsoftware.</string>
        <key>browser_sso_interaction_enabled</key>
        <integer>1</integer>
        <key>disable_explicit_app_prompt</key>
        <integer>1</integer>
    </dict>
    </plist>
    ```

    :::image type="content" source="./media/apple-enterprise-sso-plug-in/sso-extension-custom-configuration-plist.png" alt-text="See a sample custom configuration with a PLIST file for Jamf Pro.":::

    - These PLIST settings configure the following SSO Extension options:

      | Key | Type | Value |
      | --- | --- | --- |
      | **AppPrefixAllowList** | String | Enter a list of prefixes for apps that don't support MSAL **and** are allowed to use SSO. For example, enter `com.microsoft.` to allow all Microsoft apps.<br/><br/>Be sure these apps [meet the allowlist requirements](/azure/active-directory/develop/apple-sso-plugin#enable-sso-for-apps-that-dont-use-a-microsoft-identity-platform-library).|
      | **browser_sso_interaction_enabled** | Integer | When set to `1`, users can sign in from Safari browser, and from apps that don't support MSAL. Enabling this setting allows users to bootstrap the extension from Safari or other apps.|
      | **disable_explicit_app_prompt** | Integer | Some apps might incorrectly enforce end-user prompts at the protocol layer. If you see this problem, users are prompted to sign in, even though the Microsoft Enterprise SSO plug-in works for other apps. <br/><br/>When set to `1` (one), you reduce these   prompts. |

    > [!TIP]
    > For more information on these properties, and other properties you can configure, see [Microsoft Enterprise SSO plug-in for Apple devices (preview)](/azure/active-directory/develop/apple-sso-plugin#more-configuration-options).

6. Select the **Scope** tab. Enter the computers or devices that should be targeted to receive the SSO Extension MDM profile.
7. Select **Save**.

When the device checks in with the Jamf Pro service, it receives this profile.

## End user experience

:::image type="content" source="./media/apple-enterprise-sso-plug-in/flow-chart-end-user-macOS.png" alt-text="End user flow chart when installing SSO app app extension on macOS devices in Microsoft Intune.":::

- If you're not deploying the Company Portal using an app policy, then users must install it manually. Users don't need to use the Company Portal app, it just needs to be installed on the device.

- Users sign in to any supported app or website to bootstrap the extension. Bootstrap is the process of signing in for the first time, which sets up the extension.  

:::image type="content" source="./media/apple-enterprise-sso-plug-in/user-signs-in.png" alt-text="Users signs in to app or website to bootstrap the SSO app extension on macOS devices.":::

- After users sign in successfully, the extension is automatically used to sign in to any other supported app or website.

You can test Single Sign on by opening [Safari in Private mode](https://support.apple.com/guide/safari/browse-privately-ibrw1069/mac) (opens Apple's web site) and opening the site https://portal.office.com, no username and password will be required.
:::image type="content" source="./media/apple-enterprise-sso-plug-in/macos-sso-animated.gif" alt-text="Users signs in to app or website to bootstrap the SSO app extension on iOS/iPadOS and macOS devices in Microsoft Intune.":::

On macOS, users are prompted to opt in or out of SSO when they sign in to a work or school app. They can select **Don’t ask me again** to opt out of SSO and block future requests.

Users can also manage their SSO preferences in the Company Portal app for macOS. To edit preferences, go to the Company Portal menu bar > **Company Portal** > **Settings**. They can select or deselect **Don’t ask me to sign in with single sign-on for this device**.
:::image type="content" source="./media/apple-enterprise-sso-plug-in/macOS-5.png" alt-text="Don’t ask me to sign in with single sign-on for this device.":::

## Next steps

- For information about the Microsoft Enterprise SSO plug-in, see [Microsoft Enterprise SSO plug-in for Apple devices (preview)](/azure/active-directory/develop/apple-sso-plugin).

- For information from Apple on the single sign-on extension payload, see [Single Sign-On Extensions payload settings](https://support.apple.com/guide/mdm/single-sign-on-extensions-mdmfd9cdf845/web) (opens Apple's web site).
