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

The Microsoft Enterprise SSO plug-in (preview) provides a single sign-on (SSO) to apps and websites that use Microsoft Azure Active Directory (AD) for authentication, including Microsoft 365. This plug-in uses the [Apple single sign on app extension](device-features-configure.md#single-sign-on-app-extension). It reduces the number of authentication prompts users get when using devices managed by Mobile Device Management (MDM), including Microsoft Intune.

Once set up, apps that support the Microsoft Authentication Library (MSAL) automatically take advantage of the Microsoft Enterprise SSO plug-in (preview). Apps that don't support MSAL can be allowed to use the extension. Just add the application bundle ID or prefix to the extension configuration.  

For example, to allow a Microsoft app that doesn't support MSAL, add `com.microsoft.` to the **AppPrefixAllowList** property. Be careful with the apps you allow, they will be able to bypass interactive login prompts for the signed in user.

For more information, see [Microsoft Enterprise SSO plug-in for Apple devices - apps that don't use MSAL](/azure/active-directory/develop/apple-sso-plugin#applications-that-dont-use-msal).  

This article shows how to deploy the Microsoft Enterprise SSO plug-in (preview) for iOS/iPadOS Apple Devices with Intune.

> [!IMPORTANT]
> The Microsoft Enterprise SSO plug-in for Apple Devices is in public preview. This preview version is provided without a service level agreement (SLA). It's not recommended to use in production. Certain features might not be supported or might have restricted behavior. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## Prerequisites

- The device must support the plug-in:
  - The device is managed with Intune.
  - iOS/iPadOS 13.0 and newer
- Microsoft Authenticator app installed on the device.
  The Microsoft Authenticator app can be installed manually by users, or deployed via Intune. For information on how to install the Microsoft Authenticator app, see [Manage Apple volume-purchased apps](../apps/vpp-apps-ios.md).

> [!NOTE]
> On iOS and iPadOS devices, Apple requires that the SSO app extension and the Microsoft Authenticator app be installed. Users don't need to use or configure the Microsoft Authenticator app, it just needs to be installed on the device.

## Microsoft Enterprise SSO plug-in vs. Kerberos SSO extension

In Intune, when you use the SSO app extension, you use **Microsoft Azure AD** or **Kerberos** for authentication. The SSO app extension is designed to improve the sign-in experience for apps and websites that use these authentication methods.

The Microsoft Enterprise SSO plug-in uses the SSO app extension with **Microsoft Azure AD** authentication. The Microsoft Azure AD and Kerberos extension types can both be used on a device at the same time. Be sure to create separate device profiles for each extension type you plan to use on your devices.

To determine the correct SSO extension type for your scenario, use the following table:

---
| Microsoft Enterprise SSO plug-in for Apple Devices | Single sign-on app extension with Kerberos |
| --- | --- |
| Uses the **Microsoft Azure AD** SSO app extension type | Uses the **Kerberos** SSO app extension type |
| Supports the following apps: <br/> - Microsoft 365 <br/> - Apps, websites or services integrated with Azure AD | Supports the following apps: <br/><br/> - Apps, websites or services integrated with AD <br/> |

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

## End user experience

:::image type="content" source="./media/apple-enterprise-sso-plug-in/flow-chart-end-user-iOSiPadOS.png" alt-text="End user flow chart when installing SSO app app extension on iOS/iPadOS devices in Microsoft Intune.":::

- If you're not deploying the Microsoft Authenticator using an app policy, then users must install it manually. Users don't need to use the Authenticator app, it just needs to be installed on the device.

- Users sign in to any supported app or website to bootstrap the extension. Bootstrap is the process of signing in for the first time, which sets up the extension.  

- After users sign in successfully, the extension is automatically used to sign in to any other supported app or website.

You can test Single Sign on by opening [Safari in Private mode](https://support.apple.com/guide/ipad/browse-the-web-privately-ipad8ea0fc1a/ipados) (opens Apple's web site) and opening the site https://portal.office.com, no username and password will be required.
:::image type="content" source="./media/apple-enterprise-sso-plug-in/ipad-sso-animated.gif" alt-text="Animation showing SSO experience on iPadOS":::

## Next steps

- For information about the Microsoft Enterprise SSO plug-in, see [Microsoft Enterprise SSO plug-in for Apple devices (preview)](/azure/active-directory/develop/apple-sso-plugin).

- For information from Apple on the single sign-on extension payload, see [Single Sign-On Extensions payload settings](https://support.apple.com/guide/mdm/single-sign-on-extensions-mdmfd9cdf845/web) (opens Apple's web site).
