---
# required metadata

title: Microsoft Enterprise SSO plug-in in Microsoft Intune (iOS/iPadOS)
description: Add or create an iOS or iPadOS device profile using the Microsoft Enterprise SSO plug-in in Microsoft Intune. 
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

ms.reviewer: tbc
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Use the Microsoft Enterprise SSO plug-in on iOS/iPadOS devices in Microsoft Intune

[!INCLUDE [Apple SSO Boilerplate](../includes/apple-enterprise-sso-intro-boilerplate.md)]

This article shows how to deploy the Microsoft Enterprise SSO plug-in (preview) for iOS/iPadOS Apple Devices with Intune.

[!INCLUDE [Apple SSO Disclaimer Boilerplate](../includes/apple-enterprise-sso-disclaimer-boilerplate.md)]

## Prerequisites

- The device must support the plug-in:
  - The device is managed with Intune.
  - iOS/iPadOS 13.0 and newer
- Microsoft Authenticator app installed on the device.
  The Microsoft Authenticator app can be installed manually by users, or deployed via Intune. For information on how to install the Microsoft Authenticator app, see [Manage Apple volume-purchased apps](../apps/vpp-apps-ios.md).

> [!NOTE]
> On iOS and iPadOS devices, Apple requires that the SSO app extension and the Microsoft Authenticator app be installed. Users don't need to use or configure the Microsoft Authenticator app, it just needs to be installed on the device.

[!INCLUDE [Apple Kerberos Extension Boilerplate](../includes/apple-enterprise-sso-kerberos-boilerplate.md)]

---

For more information on the single sign-on extension, see [Single sign-on app extension](device-features-configure.md#single-sign-on-app-extension).

## Create a single sign-on app extension configuration profile

In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), create a device configuration profile. This profile includes the settings to configure the SSO app extension on devices.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Platform**: Choose your platform:

        - **iOS/iPadOS**

    - **Profile**: Select **Device features**. Or, select **Templates** > **Device features**.

4. Select **Create**.

:::image type="content" source="./media/apple-enterprise-sso-plug-in/iOS-1.png" alt-text="Creating a device configuration profile in Intune":::

5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, a good policy name is **iOS: Microsoft Enterprise SSO plug-in**.
    - **Description**: Enter a description for the policy. This setting is optional, but recommended.

6. Select **Next**.
7. In **Configuration settings**, select **Single sign-on app extension**, and configure the following properties:

    - **SSO app extension type**: Select **Microsoft Azure AD**. <br/>
    :::image type="content" source="./media/apple-enterprise-sso-plug-in/iOS-2.png" alt-text="Device features profile settings in Intune":::
    
    - **Enable shared device mode**:  

      - **Not configured**: Intune doesn't change or update this setting. _For most scenarios, including Shared iPad, personal devices, and devices with or without user affinity, select this option._
      - Yes: Select this option only if the targeted devices are using Azure AD Shared device mode. For more information, see [Shared device mode overview](/azure/active-directory/develop/msal-shared-devices).  

    - **App bundle ID**: Enter a list of bundle IDs for apps that don't support MSAL **and** are allowed to use SSO. For more information, see [Applications that don't use MSAL](/azure/active-directory/develop/apple-sso-plugin#enable-sso-for-apps-that-dont-use-a-microsoft-identity-platform-library).

    - **Additional configuration**: To customize the end user experience, you can add the following properties.

      | Key | Type | Value |
      | --- | --- | --- |
      | **AppPrefixAllowList** | String | Enter a list of prefixes for apps that don't support MSAL **and** are allowed to use SSO. For example, enter `com.microsoft.` to allow all Microsoft apps.<br/><br/>Be sure these apps [meet the allowlist requirements](/azure/active-directory/develop/apple-sso-plugin#enable-sso-for-apps-that-dont-use-a-microsoft-identity-platform-library).|
      | **browser_sso_interaction_enabled** | Integer | When set to `1`, users can sign in from Safari browser, and from apps that don't support MSAL. Enabling this setting allows users to bootstrap the extension from Safari or other apps.|
      | **browser_sso_disable_mfa** | Integer | Set to `0` (default) to require the Microsoft Enterprise SSO plug-in use multi-factor authentication (MFA) during bootstrap. Requiring MFA during bootstrap reduces prompts for MFA in apps that are protected by conditional access and require MFA. Microsoft recommends MFA be enabled to increase security and improve the user experience.<br/><br/>Set to `1` to disable MFA in bootstrap. Users are prompted by individual apps that require MFA. |
      | **disable_explicit_app_prompt** | Integer | Some apps might incorrectly enforce end-user prompts at the protocol layer. If you see this problem, users are prompted to sign in, even though the Microsoft Enterprise SSO plug-in works for other apps. <br/><br/>When set to `1` (one), you reduce these prompts. |

:::image type="content" source="./media/apple-enterprise-sso-plug-in/iOS-3.png" alt-text="Additional configuration options in Intune":::
 
      > [!TIP]
      > For more information on these properties, and other properties you can configure, see [Microsoft Enterprise SSO plug-in for Apple devices (preview)](/azure/active-directory/develop/apple-sso-plugin#more-configuration-options).

8. Continue creating the profile, and assign the profile to the users or groups that will receive these settings. For the specific steps, see [Create the profile](device-features-configure.md#create-the-profile).

For guidance on assigning profiles, see [Assign user and device profiles](device-profile-assign.md).

When the device checks in with the Intune service, it will receive this profile.

You can check that the profile was deployed correctly by going to **Devices** > **Configuration Profiles** > select the profile you have just created and generate a report:
:::image type="content" source="./media/apple-enterprise-sso-plug-in/iOS-4.png" alt-text="Profile deployment reporting in Intune":::

For more information, see [How long does it take for devices to get a policy](device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned).

[!INCLUDE [Apple iOS End User Experience Boilerplate](../includes/apple-enterprise-sso-ios-end-user-experience-boilerplate.md)]

## Next steps

- For information about the Microsoft Enterprise SSO plug-in, see [Microsoft Enterprise SSO plug-in for Apple devices (preview)](/azure/active-directory/develop/apple-sso-plugin).

- For information from Apple on the single sign-on extension payload, see [Single Sign-On Extensions payload settings](https://support.apple.com/guide/mdm/single-sign-on-extensions-mdmfd9cdf845/web) (opens Apple's web site).
