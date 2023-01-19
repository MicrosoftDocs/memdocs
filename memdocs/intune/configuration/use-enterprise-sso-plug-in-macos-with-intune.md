---
# required metadata

title: Configure macOS Enterprise SSO plug-in in Microsoft Intune
description: Add or create an macOS device profile using the Microsoft Enterprise SSO plug-in in Microsoft Intune. 
keywords:
author: TBC
ms.author: alessanc
manager: ianfarr
ms.date: 01/18/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: miepping, tbc
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Use the Microsoft Enterprise SSO plug-in on macOS devices in Microsoft Intune

[!INCLUDE [Apple SSO Boilerplate](../includes/apple-enterprise-sso-intro-boilerplate.md)]

This article shows how to deploy the Microsoft Enterprise SSO plug-in (preview) for macOS Apple Devices with Intune.

[!INCLUDE [Apple SSO Disclaimer Boilerplate](../includes/apple-enterprise-sso-disclaimer-boilerplate.md)]

## Prerequisites

- The device must support the plug-in:
  - macOS 10.15 and newer
- The device is managed with Intune. The Company Portal app must be installed and configured on the device.

[!INCLUDE [Apple Kerberos Extension Boilerplate](../includes/apple-enterprise-sso-kerberos-boilerplate.md)]

---

For more information on the single sign-on extension, go to [Single sign-on app extension](device-features-configure.md#single-sign-on-app-extension).

## Create a single sign-on app extension configuration profile

In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create a device configuration profile. This profile includes the settings to configure the SSO app extension on devices.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Platform**: Select **macOS**.
    - **Profile**: Select **Templates** > **Device features**.

4. Select **Create**:

    :::image type="content" source="./media/apple-enterprise-sso-plug-in/macos-create-device-features.png" alt-text="Screenshot that shows how to create a device features configuration profile for macOS in Intune.":::

5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, a good policy name is **macOS: Microsoft Enterprise SSO plug-in**.
    - **Description**: Enter a description for the policy. This setting is optional, but recommended.

6. Select **Next**.
7. In **Configuration settings**, select **Single sign-on app extension**, and configure the following properties:

    - **SSO app extension type**: Select **Microsoft Azure AD**:

      :::image type="content" source="./media/apple-enterprise-sso-plug-in/macos-device-features-sso-extension-type.png" alt-text="Screenshot that shows the SSO app extension type and Microsoft Azure AD for macOS in Intune":::

    - **App bundle ID**: Enter a list of bundle IDs for apps that don't support MSAL **and** are allowed to use SSO. For more information, go to [Applications that don't use MSAL](/azure/active-directory/develop/apple-sso-plugin#enable-sso-for-apps-that-dont-use-a-microsoft-identity-platform-library).

    - **Additional configuration**: To customize the end user experience, you can add the following properties. These properties are the default values used by the Microsoft SSO Extension, but they can be customized for your organization needs:

      [!INCLUDE [Apple SSO Recommended Settings Table Boilerplate](../includes/apple-enterprise-sso-recommended-settings-intune-and-generic-mdm-boilerplate.md)]

      When you're done configuring the recommended settings, the settings look similar to the following values in your Intune configuration profile:

      :::image type="content" source="./media/apple-enterprise-sso-plug-in/macos-sso-extension-additional-configuration.png" alt-text="Screenshot that shows the end user experience configuration options for the Enterprise SSO plug-in on macOS devices in Intune.":::

8. Continue creating the profile, and assign the profile to the users or groups that will receive these settings. For the specific steps, go to [Create the profile](device-features-configure.md#create-the-profile).

    For guidance on assigning profiles, go to [Assign user and device profiles](device-profile-assign.md).

When the device checks in with the Intune service, it will receive this profile. For more information, go to [How long does it take for devices to get a policy](device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned).

To check that the profile deployed correctly, in the Endpoint Manager admin center, go to **Devices** > **Configuration Profiles** > select the profile you created and generate a report:

:::image type="content" source="./media/apple-enterprise-sso-plug-in/macos-enterprise-sso-profile-report.png" alt-text="Screenshot that shows the macOS device configuration profile deployment report in Intune.":::

[!INCLUDE [Apple iOS End User Experience Boilerplate](../includes/apple-enterprise-sso-macos-end-user-experience-boilerplate.md)]

## Next steps

- For information about the Microsoft Enterprise SSO plug-in, go to [Microsoft Enterprise SSO plug-in for Apple devices (preview)](/azure/active-directory/develop/apple-sso-plugin).

- For information from Apple on the single sign-on extension payload, go to [single sign-on extensions payload settings](https://support.apple.com/guide/mdm/single-sign-on-extensions-mdmfd9cdf845/web) (opens Apple's web site).
