---
# required metadata

title: Configure iOS/iPadOS Enterprise SSO plug-in with MDM
description: Learn more about the Microsoft Enterprise SSO plug-in. Add or create an iOS or iPadOS device configuration profile using the Microsoft Enterprise SSO plug-in in Microsoft Intune, Jamf Pro, and other MDM solution providers.
keywords: Enterprise SSO plug-in, Microsoft Intune
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/30/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: miepping, tbc, alessanc
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Use the Microsoft Enterprise SSO plug-in on iOS/iPadOS devices

[!INCLUDE [Apple SSO Boilerplate](../includes/apple-enterprise-sso-intro-boilerplate.md)]

This article applies to:

- iOS/iPadOS

This article shows how to deploy the Microsoft Enterprise SSO plug-in for iOS/iPadOS Apple devices with Intune, Jamf Pro, and other MDM solutions.

## Prerequisites

To use the Microsoft Enterprise SSO plug-in on iOS/iPadOS devices:

# [Intune](#tab/prereq-intune)

- The device is managed by Intune.
- The device must support the plug-in:
  - iOS/iPadOS 13.0 and newer
- The Microsoft Authenticator app must be installed on the device.

  The Microsoft Authenticator app can be installed manually by users, or deployed using Intune. For information on how to install the Microsoft Authenticator app, go to [Manage Apple volume-purchased apps](../apps/vpp-apps-ios.md).

# [Jamf Pro](#tab/prereq-jamf-pro)

- The device is managed by Jamf Pro.
- The device must support the plug-in:
  - iOS/iPadOS 13.0 and newer
- The Microsoft Authenticator app must be installed on the device.

  The Microsoft Authenticator app can be installed manually by users, or by deploying the app through Jamf Pro. For a list of options on how to install the Microsoft Authenticator app, go to [Managing macOS installers using Jamf Pro](https://docs.jamf.com/10.24.1/jamf-pro/administrator-guide/Managing_macOS_Installers.html) (opens Jamf Pro's web site).

- **[Jamf Pro and Intune integration for device compliance](../protect/conditional-access-integrate-jamf.md) is not required to use the SSO app extension.**

# [Other MDMs](#tab/prereq-other-mdm)

- The device is managed by a mobile device management (MDM) provider solution.
- The MDM solution must support configuring [Single Sign-on MDM payload settings for Apple devices](https://support.apple.com/guide/deployment/extensible-single-sign-on-payload-settings-depfd9cdf845/web) with a device policy.
- The device must support the plug-in:
  - iOS/iPadOS 13.0 and newer
- The Microsoft Authenticator app must be installed on the device. The Microsoft Authenticator app can be installed manually by users, or deployed with an MDM policy.

--- 

> [!NOTE]
> On iOS/iPadOS devices, Apple requires that the SSO app extension and the Microsoft Authenticator app be installed. Users don't need to use or configure the Microsoft Authenticator app, it just needs to be installed on the device.

[!INCLUDE [Apple Kerberos Extension Boilerplate](../includes/apple-enterprise-sso-kerberos-boilerplate.md)]

---

For more information on the single sign-on extension, go to [Single sign-on app extension](device-features-configure.md#single-sign-on-app-extension).

## Create a single sign-on app extension configuration profile

# [Intune](#tab/create-profile-intune)

In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create a device configuration profile. This profile includes the settings to configure the SSO app extension on devices.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Platform**: Select **iOS/iPadOS**.
    - **Profile**: Select **Templates** > **Device features**.

4. Select **Create**:

    :::image type="content" source="./media/apple-enterprise-sso-plug-in/ios-ipados-create-device-features.png" alt-text="Screenshot that shows how to create a device features configuration profile for iOS/iPadOS in Intune." lightbox="./media/apple-enterprise-sso-plug-in/ios-ipados-create-device-features.png":::

5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, a good policy name is **iOS: Microsoft Enterprise SSO plug-in**.
    - **Description**: Enter a description for the policy. This setting is optional, but recommended.

6. Select **Next**.
7. In **Configuration settings**, select **Single sign-on app extension**, and configure the following properties:

    - **SSO app extension type**: Select **Microsoft Azure AD**.

      :::image type="content" source="./media/apple-enterprise-sso-plug-in/ios-ipados-device-features-sso-extension-type.png" alt-text="Screenshot that shows the SSO app extension type and Microsoft Azure AD for iOS/iPadOS in Intune.":::

    - **Enable shared device mode**:  

      - **Not configured**: Intune doesn't change or update this setting.

        For most scenarios, including Shared iPad, personal devices, and devices with or without user affinity, select this option.
      - **Yes**: Select this option **only** if the targeted devices are using Azure AD Shared device mode. For more information, go to [Shared device mode overview](/azure/active-directory/develop/msal-shared-devices).  

    - **App bundle ID**: Enter a list of bundle IDs for apps that don't support MSAL **and** are allowed to use SSO. For more information, go to [Applications that don't use MSAL](/azure/active-directory/develop/apple-sso-plugin#enable-sso-for-apps-that-dont-use-a-microsoft-identity-platform-library).

    - **Additional configuration**: To customize the end user experience, you can add the following properties. These properties are the default values used by the Microsoft SSO Extension, but they can be customized for your organization needs:

      [!INCLUDE [Apple SSO Recommended Settings Table Boilerplate](../includes/apple-enterprise-sso-recommended-settings-ios-intune-and-generic-mdm-boilerplate.md)]

      When you're done configuring the recommended settings, the settings look similar to the following values in your Intune configuration profile:

      :::image type="content" source="./media/apple-enterprise-sso-plug-in/ios-ipados-sso-extension-additional-configuration.png" alt-text="Screenshot that shows the end user experience configuration options for the Enterprise SSO plug-in on iOS/iPadOS devices in Intune.":::

8. Continue creating the profile, and assign the profile to the users or groups that will receive these settings. For the specific steps, go to [Create the profile](device-features-configure.md#create-the-profile).

    For guidance on assigning profiles, go to [Assign user and device profiles](device-profile-assign.md).

When the device checks in with the Intune service, it will receive this profile. For more information, go to [Policy refresh intervals](device-profile-troubleshoot.md#policy-refresh-intervals).

To check that the profile deployed correctly, in the Intune admin center, go to **Devices** > **Configuration Profiles** > select the profile you created and generate a report:

:::image type="content" source="./media/apple-enterprise-sso-plug-in/ios-ipados-enterprise-sso-profile-report.png" alt-text="Screenshot that shows the iOS/iPadOS device configuration profile deployment report in Intune.":::

# [Jamf Pro](#tab/create-profile-jamf-pro)

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

    [!INCLUDE [Apple SSO Recommended Settings Table Boilerplate](../includes/apple-enterprise-sso-recommended-settings-ios-jamf-pro-boilerplate.md)]

7. Select the **Scope** tab. Enter the computers or devices that should be targeted to receive the SSO Extension MDM profile.
8. Select **Save**.

When the device checks in with the Jamf Pro service, it receives the profile.

# [Other MDMs](#tab/create-profile-other-mdm)

In the MDM portal, create a device configuration profile. This profile includes the settings to configure the SSO app extension on devices.

1. Sign in to the MDM portal.
2. Create a new device configuration profile.
3. Select a **Single Sign-On Extensions** or **SSO extension** option. The name varies depending on the MDM solution you're using.
4. Enter the following properties:

    | **Key** | **Value** |
    | --- | --- |
    | Payload Type | SSO |
    | Extension Identifier | com.microsoft.azureauthenticator.ssoextension |
    | Sign-On Type | **Redirect** |
    | URLs | - `https://login.microsoftonline.com` <br/> - `https://login.microsoft.com` <br/> - `https://sts.windows.net` <br/> - `https://login.partner.microsoftonline.cn` <br/> - `https://login.chinacloudapi.cn` <br/> - `https://login.microsoftonline.us` <br/> - `https://login-us.microsoftonline.com` |

5. Optionally, you can configure other properties. These properties are the default values used by the Microsoft SSO Extension, but they can be customized for your organization needs:

    [!INCLUDE [Apple SSO Recommended Settings Table Boilerplate](../includes/apple-enterprise-sso-recommended-settings-ios-intune-and-generic-mdm-boilerplate.md)]

6. Assign the new policy to the devices that should be targeted to receive the SSO Extension MDM profile.

When the device checks in with the MDM service, it receives this profile.

--- 

[!INCLUDE [Apple iOS End User Experience Boilerplate](../includes/apple-enterprise-sso-ios-end-user-experience-boilerplate.md)]

> [!TIP]
> Learn more about how the SSO plug-in works and how to troubleshoot the Microsoft Enterprise SSO Extension with the [SSO troubleshooting guide for Apple devices](/azure/active-directory/devices/troubleshoot-mac-sso-extension-plugin).

## Next steps

- For information about the Microsoft Enterprise SSO plug-in, go to [Microsoft Enterprise SSO plug-in for Apple devices](/azure/active-directory/develop/apple-sso-plugin).

- For information from Apple on the single sign-on extension payload, go to [single sign-on extensions payload settings](https://support.apple.com/guide/deployment/single-sign-on-payload-settings-dep7a81f07b/web) (opens Apple's web site).

- For information on troubleshooting the Microsoft Enterprise SSO Extension, go to [Troubleshooting the Microsoft Enterprise SSO Extension plugin on Apple devices](/azure/active-directory/devices/troubleshoot-mac-sso-extension-plugin).
