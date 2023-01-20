---
# required metadata

title: Configure iOS/iPadOS Enterprise SSO plug-in in Jamf Pro
description: Add or create an iOS or iPadOS device profile using the Microsoft Enterprise SSO plug-in in Jamf Pro. 
keywords:
author: TBC
ms.author: alessanc
manager: ianfarr
ms.date: 01/19/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: miepping
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection: M365-identity-device-management
---

# Use the Microsoft Enterprise SSO plug-in on iOS/iPadOS devices in Jamf Pro

[!INCLUDE [Apple SSO Boilerplate](../includes/apple-enterprise-sso-intro-boilerplate.md)]

This feature applies to:

- iOS/iPadOS

This article shows how to deploy the Microsoft Enterprise SSO plug-in (preview) for iOS/iPadOS devices with Jamf Pro.

[!INCLUDE [Apple SSO Disclaimer Boilerplate](../includes/apple-enterprise-sso-disclaimer-boilerplate.md)]

## Prerequisites

To use the Microsoft Enterprise SSO plug-in for Apple devices:

- The device must be managed via Jamf Pro.
- The device must support the plug-in:
  - iOS/iPadOS 13.0 and newer
- The Microsoft Authenticator app must be installed on the device.

  The Microsoft Authenticator app can be installed manually by users, or by deploying the app through Jamf Pro. For a list of options on how to install the Microsoft Authenticator app, go to [Managing macOS installers using Jamf Pro](https://docs.jamf.com/10.24.1/jamf-pro/administrator-guide/Managing_macOS_Installers.html) (opens Jamf Pro's web site).

> [!NOTE]
>
> - On iOS and iPadOS devices, Apple requires that the SSO app extension and the Microsoft Authenticator app be installed. Users don't need to use the Microsoft Authenticator app, it just needs to be installed on the device.
>
> - **[Jamf Pro and Intune integration for device compliance](../protect/conditional-access-integrate-jamf.md) is not required to use the SSO app extension.**

[!INCLUDE [Apple Kerberos Extension Boilerplate](../includes/apple-enterprise-sso-kerberos-boilerplate.md)]

---

For more information on the single sign-on extension, go to [Single sign-on app extension](device-features-configure.md#single-sign-on-app-extension).

## Create a single sign-on app extension configuration profile in Jamf Pro

In the Jamf Pro portal, you create a Computer or Device configuration profile. This profile includes the settings to configure the SSO app extension on devices.

1. Sign in to the Jamf Pro portal.
2. To create an iOS/iPadOS profile, select **Devices** > **Configuration profiles** > **New**:

    :::image type="content" source="./media/apple-enterprise-sso-plug-in/ios-ipados-create-profile-jamf.png" alt-text="Screenshot that shows the Jamf Pro portal and how to create a configuration profile for iOS/iPadOS devices.":::

3. In **Name**, enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, a good policy name is: **iOS/iPadOS: Microsoft Enterprise SSO plug-in**.

4. In the **Options** column, scroll down and select **Single Sign-On Extensions** > **Add**:

    :::image type="content" source="./media/apple-enterprise-sso-plug-in/ios-ipados-sso-extensions-jamf.png" alt-text="Screenshot that shows the Jamf Pro portal. Select the configuration profiles SSO option and select add for iOS/iPadOS devices.":::

5. Enter the following properties:

    - **Payload Type**: Select **SSO**.
    - **Extension Identifier**: Enter `com.microsoft.azureauthenticator.ssoextension`.
    - **Team Identifier**: No value is needed, leave the field blank.
    - **Sign-On Type**: Select **Redirect**.
    - **URLs**: Enter the following URLs, one at a time:
      - `https://login.microsoftonline.com`
      - `https://login.microsoft.com`
      - `https://sts.windows.net`
      - `https://login.partner.microsoftonline.cn`
      - `https://login.chinacloudapi.cn`
      - `https://login.microsoftonline.us`
      - `https://login.usgovcloudapi.net`
      - `https://login-us.microsoftonline.com`

    :::image type="content" source="./media/apple-enterprise-sso-plug-in/ios-ipados-sso-extensions-settings-jamf.png" alt-text="Screenshot that shows the Jamf Pro portal and the payload type, extension identifier, team identifier, and SSO type settings for iOS/iPadOS devices.":::

    :::image type="content" source="./media/apple-enterprise-sso-plug-in/ios-ipados-sso-extensions-urls-jamf.png" alt-text="Screenshot that shows the Jamf Pro portal and the SSO URLs for iOS/iPadOS devices.":::

6. In **Custom Configuration**, you'll define other required properties. Jamf Pro requires that these properties are configured using an uploaded PLIST file. To see the full list of configurable properties, go to [Azure AD Apple SSO Extension documentation](/azure/active-directory/develop/apple-sso-plugin#manual-configuration-for-other-mdm-services).

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

    :::image type="content" source="./media/apple-enterprise-sso-plug-in/ios-ipados-custom-configuration-plist-jamf.png" alt-text="Screenshot that shows a sample custom configuration with a PLIST file for Jamf Pro.":::

    These PLIST settings configure the following SSO Extension options. These properties are the default values used by the Microsoft SSO Extension, but they can be customized for your organization needs:

    [!INCLUDE [Apple SSO Recommended Settings Table Boilerplate](../includes/apple-enterprise-sso-recommended-settings-jamf-pro-boilerplate.md)]

7. Select the **Scope** tab. Enter the computers or devices that should be targeted to receive the SSO Extension MDM profile.
8. Select **Save**.

When the device checks in with the Jamf Pro service, it receives the profile.

[!INCLUDE [Apple iOS End User Experience Boilerplate](../includes/apple-enterprise-sso-ios-end-user-experience-boilerplate.md)]

## Next steps

- For information about the Microsoft Enterprise SSO plug-in, go to [Microsoft Enterprise SSO plug-in for Apple devices (preview)](/azure/active-directory/develop/apple-sso-plugin).

- For information from Apple on the single sign-on extension payload, go to [single sign-on extensions payload settings](https://support.apple.com/guide/mdm/single-sign-on-extensions-mdmfd9cdf845/web) (opens Apple's web site).
