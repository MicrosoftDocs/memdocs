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

[!INCLUDE [Apple SSO Boilerplate](../includes/apple-enterprise-sso-intro-boilerplate.md)]

This feature applies to:

- macOS

This article explains how to deploy the Microsoft Enterprise SSO plug-in (preview) for macOS Devices with Jamf Pro.

[!INCLUDE [Apple SSO Disclaimer Boilerplate](../includes/apple-enterprise-sso-disclaimer-boilerplate.md)]

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

[!INCLUDE [Apple Kerberos Extension Boilerplate](../includes/apple-enterprise-sso-kerberos-boilerplate.md)]

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

[!INCLUDE [Apple iOS End User Experience Boilerplate](../includes/apple-enterprise-sso-macos-end-user-experience-boilerplate.md)]

## Next steps

- For information about the Microsoft Enterprise SSO plug-in, see [Microsoft Enterprise SSO plug-in for Apple devices (preview)](/azure/active-directory/develop/apple-sso-plugin).

- For information from Apple on the single sign-on extension payload, see [Single Sign-On Extensions payload settings](https://support.apple.com/guide/mdm/single-sign-on-extensions-mdmfd9cdf845/web) (opens Apple's web site).
