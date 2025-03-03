---
# required metadata

title: Configure macOS Enterprise SSO app extension with MDMs
description: Learn more about the Microsoft Enterprise single sign-on (SSO) app extension plug-in. Add or create an macOS device profile using the SSO app extension in Microsoft Intune, Jamf Pro, and other MDM solution providers.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/01/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
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

# Use the Microsoft Enterprise SSO plug-in on macOS devices

[!INCLUDE [Apple SSO Boilerplate](../includes/apple-enterprise-sso-intro-boilerplate.md)]

This feature applies to:

- macOS

  For iOS/iPadOS, go to [Use the Microsoft Enterprise SSO plug-in on iOS/iPadOS devices](use-enterprise-sso-plug-in-ios-ipados-with-intune.md).

On macOS devices, you can configure SSO app extension settings in two places in Intune:

- **Device features template** (**this article**) - This option configures only the SSO app extension and uses your MDM provider, like Intune, to deploy the settings to devices.

  Use this article if you only want to configure the SSO app extension settings and don't want to also configure Platform SSO.

- **[Settings Catalog](platform-sso-macos.md)** - This option configures Platform SSO and the SSO app extension together. You use Intune to deploy the settings to your devices.

  Use the settings catalog settings if you want to configure both the Platform SSO and SSO app extension settings. For more information, go to [Configure platform SSO for macOS devices in Microsoft Intune](platform-sso-macos.md).

For an overview of your SSO options on Apple devices, go to [SSO overview and options for Apple devices in Microsoft Intune](use-enterprise-sso-plug-in-ios-ipados-macos.md).

This article shows how to create an SSO app extension configuration policy for macOS Apple devices with Intune, Jamf Pro, and other MDM solutions.

If you want to configure Platform SSO and SSO app extension settings together, then go to [Configure platform SSO for macOS devices in Microsoft Intune](platform-sso-macos.md).

## App support

[!INCLUDE [Apple SSO app support](../includes/apple-enterpsie-sso-app-support.md)]

## Prerequisites

To use the Microsoft Enterprise SSO plug-in on macOS devices:

# [Intune](#tab/prereq-intune)

- The device is MDM managed by Intune.
- The device must support the plug-in:
  - macOS 10.15 and newer
- The Microsoft Company Portal app must be installed and configured on the device.
- The Enterprise SSO plug-in requirements are configured, including the [Apple network configuration URLs](/entra/identity-platform/apple-sso-plugin#requirements).

# [Jamf Pro](#tab/prereq-jamf-pro)

- The device is managed by Jamf Pro.
- The device must support the plug-in:
  - macOS 10.15 and newer
- The Microsoft Company Portal app must be installed on the device.

  Users can install the Company Portal app manually. Or, admins can deploy the app using Jamf Pro. For a list of options on how to install the Company Portal app, go to [Package Management - Adding a Package to Jamf Admin](https://learn.jamf.com/bundle/jamf-pro-documentation-current/page/Package_Management.html#ariaid-title4) (opens Jamf Pro's web site).

  > [!NOTE]
  > On macOS devices, Apple requires the Company Portal app be installed. Users don't need to use or configure the Company Portal app, it just needs to be installed on the device.

- The Enterprise SSO plug-in requirements are configured, including the [Apple network configuration URLs](/entra/identity-platform/apple-sso-plugin#requirements).

# [Other MDMs](#tab/prereq-other-mdm)

- The device is managed by a mobile device management (MDM) provider solution.
- The MDM solution must support configuring the [Single Sign-on MDM payload settings for Apple devices](https://support.apple.com/guide/deployment/extensible-single-sign-on-payload-settings-depfd9cdf845/web) (opens Apple's web site) with a device policy.
- The device must support the plug-in:
  - macOS 10.15 and newer
- The Microsoft Company Portal app must be installed on the device.

  Users can install the Company Portal app manually. Or, admins can deploy the app using an MDM policy. You can [download the Company Portal app installer package](https://go.microsoft.com/fwlink/?linkid=853070).

  > [!NOTE]
  > On macOS devices, Apple requires the Company Portal app be installed. Users don't need to use or configure the Company Portal app, it just needs to be installed on the device.

- The Enterprise SSO plug-in requirements are configured, including the [Apple network configuration URLs](/entra/identity-platform/apple-sso-plugin#requirements).

---

[!INCLUDE [Apple Kerberos Extension Boilerplate](../includes/apple-enterprise-sso-kerberos-boilerplate.md)]

For more information on the SSO app extension, go to [SSO overview and options for Apple devices in Microsoft Intune](use-enterprise-sso-plug-in-ios-ipados-macos.md).

## Create a single sign-on app extension configuration policy

This section shows how to create an SSO app extension policy. For information on platform SSO, go to [Configure platform SSO for macOS devices in Microsoft Intune](platform-sso-macos.md).

# [Intune](#tab/create-profile-intune)

In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create a device configuration profile. This profile includes the settings to configure the SSO app extension on devices.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy**.
3. Enter the following properties:

    - **Platform**: Select **macOS**.
    - **Profile type**: Select **Templates** > **Device features**.

4. Select **Create**:

    :::image type="content" source="./media/apple-enterprise-sso-plug-in/macos-create-device-features.png" alt-text="Screenshot that shows how to create a device features configuration profile for macOS in Intune.":::

5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, a good policy name is **macOS-SSO app extension**.
    - **Description**: Enter a description for the policy. This setting is optional, but recommended.

6. Select **Next**.
7. In **Configuration settings**, select **Single sign-on app extension**, and configure the following properties:

    - **SSO app extension type**: Select **Microsoft Entra ID**:

      :::image type="content" source="./media/apple-enterprise-sso-plug-in/macos-device-features-sso-extension-type.png" alt-text="Screenshot that shows the SSO app extension type and Microsoft Entra ID for macOS in Intune":::

    - **App bundle ID**: Enter a list of bundle IDs for apps that don't support MSAL **and** are allowed to use SSO. For more information, go to [Applications that don't use MSAL](/entra/identity-platform/apple-sso-plugin#enable-sso-for-apps-that-dont-use-a-microsoft-identity-platform-library).

    - **Additional configuration**: To customize the end user experience, you can add the following properties. These properties are the default values used by the SSO app extension, but they can be customized for your organization needs:

      [!INCLUDE [Apple SSO Recommended Settings Table Boilerplate](../includes/apple-enterprise-sso-recommended-settings-macos-intune-and-generic-mdm-boilerplate.md)]

      When you're done configuring the recommended settings, the settings look similar to the following values in your Intune configuration profile:

      :::image type="content" source="./media/apple-enterprise-sso-plug-in/macos-sso-extension-additional-configuration.png" alt-text="Screenshot that shows the end user experience configuration options for the Enterprise SSO app extension plug-in on macOS devices in Microsoft Intune.":::

8. Continue creating the profile, and assign the profile to the users or groups that receive these settings. For the specific steps, go to [Create the profile](device-features-configure.md#create-the-profile).

    For guidance on assigning profiles, go to [Assign user and device profiles](device-profile-assign.md).

When the policy is ready, you assign the policy to your users. Microsoft recommends you assign the policy when the device enrolls in Intune. But, it can be assigned at any time, including on existing devices. When the device checks in with the Intune service, it receives this profile. For more information, go to [Policy refresh intervals](device-profile-troubleshoot.md#policy-refresh-intervals).

To check that the profile deployed correctly, in the Intune admin center, go to **Devices** > **Manage devices** > **Configuration** > select the profile you created and generate a report:

:::image type="content" source="./media/apple-enterprise-sso-plug-in/macos-enterprise-sso-profile-report.png" alt-text="Screenshot that shows the macOS device configuration profile deployment report in Microsoft Intune.":::

# [Jamf Pro](#tab/create-profile-jamf-pro)

In the Jamf Pro portal, you create a Computer configuration profile. This profile includes the settings to configure the SSO app extension on devices.

1. Sign in to the Jamf Pro portal.
2. To create a macOS profile, select **Computers** > **Configuration profiles** > **New**:

    :::image type="content" source="./media/apple-enterprise-sso-plug-in/jamf-pro-configuration-profiles.png" alt-text="Screenshot that shows the Jamf Pro portal and how to create a configuration profile for macOS devices.":::

3. In **Name**, enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, a good policy name is: **macOS-Microsoft Enterprise SSO plug-in**.

4. In the **Options** column, scroll down and select **Single Sign-On Extensions** > **Add**:

    :::image type="content" source="./media/apple-enterprise-sso-plug-in/sso-extension-creation.png" alt-text="Screenshot that shows the Jamf Pro portal. Select the configuration profiles SSO option and select add for macOS devices.":::

5. Enter the following properties:

    - **Payload Type**: Select **SSO**.
    - **Extension Identifier**: Enter `com.microsoft.CompanyPortalMac.ssoextension`.
    - **Team Identifier**: Enter `UBF8T346G9`.
    - **Sign-On Type**: Select **Redirect**.
    - **URLs**: Enter the following URLs, one at a time:
      - `https://login.microsoftonline.com`
      - `https://login.microsoft.com`
      - `https://sts.windows.net`
      - `https://login.partner.microsoftonline.cn`
      - `https://login.chinacloudapi.cn`
      - `https://login.microsoftonline.us`
      - `https://login-us.microsoftonline.com`

    :::image type="content" source="./media/apple-enterprise-sso-plug-in/sso-extension-basic-settings-1.png" alt-text="Screenshot that shows the Jamf Pro portal and the payload type, extension identifier, team identifier, and SSO type settings for macOS devices.":::

    :::image type="content" source="./media/apple-enterprise-sso-plug-in/sso-extension-basic-settings-2.png" alt-text="Screenshot that shows the Jamf Pro portal and the SSO URLs for macOS devices.":::

6. In **Custom Configuration**, you define other required properties. Jamf Pro requires that these properties are configured using an uploaded PLIST file. To see the full list of configurable properties, go to [Microsoft Enterprise SSO plug-in for Apple devices documentation](/entra/identity-platform/apple-sso-plugin#manual-configuration-for-other-mdm-services).

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

    :::image type="content" source="./media/apple-enterprise-sso-plug-in/sso-extension-custom-configuration-plist.png" alt-text="Screenshot that shows a sample custom configuration with a PLIST file for Jamf Pro.":::

    These PLIST settings configure the following SSO Extension options. These properties are the default values used by the SSO app extension, but they can be customized for your organization needs:

    [!INCLUDE [Apple SSO Recommended Settings Table Boilerplate](../includes/apple-enterprise-sso-recommended-settings-macos-jamf-pro-boilerplate.md)]

7. Select the **Scope** tab. Enter the computers or devices that should be targeted to receive the SSO Extension MDM profile.
8. Select **Save**.

When the device checks in with the Jamf Pro service, it receives this profile.

> [!TIP]
> If you use Jamf Connect, it is recommended that you follow the [latest Jamf guidance on integrating Jamf Connect with Microsoft Entra ID](https://learn.jamf.com/bundle/jamf-connect-documentation-current/page/Jamf_Connect_and_Microsoft_Conditional_Access.html) (opens Jamf Pro's web site). The recommended integration pattern ensures that Jamf Connect works properly with your Conditional Access policies and Microsoft Entra ID Protection.

# [Other MDMs](#tab/create-profile-other-mdm)

In the MDM portal, create a device configuration profile. This profile includes the settings to configure the SSO app extension on devices.

1. Sign in to the MDM portal.
2. Create a new device configuration profile.
3. Select an option called **Single Sign-On Extensions** or **SSO extension**. The name can vary depending on your MDM service.
4. Enter the following properties:

    | **Key** | **Value** |
    | --- | --- |
    | Payload Type | SSO |
    | Extension Identifier | `com.microsoft.CompanyPortalMac.ssoextension` |
    | Team Identifier | `UBF8T346G9` |
    | Sign-On Type | Redirect |
    | URLs | - `https://login.microsoftonline.com` <br/> - `https://login.microsoft.com` <br/> - `https://sts.windows.net` <br/> - `https://login.partner.microsoftonline.cn` <br/> - `https://login.chinacloudapi.cn` <br/>  - `https://login.microsoftonline.us` <br/> - `https://login-us.microsoftonline.com` |

5. Optionally, you can configure other properties. These properties are the default values used by the SSO app extension, but they can be customized for your organization needs:

    [!INCLUDE [Apple SSO Recommended Settings Table Boilerplate](../includes/apple-enterprise-sso-recommended-settings-macos-intune-and-generic-mdm-boilerplate.md)]

6. Assign the new policy to the devices that should be targeted to receive the SSO Extension MDM profile.

When the device checks in with the MDM service, it receives this profile.

--- 

[!INCLUDE [Apple iOS End User Experience Boilerplate](../includes/apple-enterprise-sso-macos-end-user-experience-boilerplate.md)]

> [!TIP]
> Learn more about how the SSO plug-in works and how to troubleshoot the Microsoft Enterprise SSO Extension with the [SSO troubleshooting guide for Apple devices](/entra/identity/devices/troubleshoot-mac-sso-extension-plugin).

## Related articles

- For information about the Microsoft Enterprise SSO plug-in, go to [Microsoft Enterprise SSO plug-in for Apple devices](/entra/identity-platform/apple-sso-plugin).

- For information from Apple on the single sign-on extension payload, go to [single sign-on extensions payload settings](https://support.apple.com/guide/mdm/single-sign-on-extensions-mdmfd9cdf845/web) (opens Apple's web site).

- For information on troubleshooting the Microsoft Enterprise SSO Extension, go to [Troubleshooting the Microsoft Enterprise SSO Extension plugin on Apple devices](/entra/identity/devices/troubleshoot-mac-sso-extension-plugin).
