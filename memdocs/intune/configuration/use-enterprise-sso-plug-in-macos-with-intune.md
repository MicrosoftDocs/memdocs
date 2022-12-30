---
# required metadata

title: Microsoft Enterprise SSO plug-in in Microsoft Intune (macOS)
description: Add or create an macOS device profile using the Microsoft Enterprise SSO plug-in in Microsoft Intune. 
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

# Use the Microsoft Enterprise SSO plug-in on macOS devices in Microsoft Intune

The Microsoft Enterprise SSO plug-in (preview) provides a single sign-on (SSO) to apps and websites that use Microsoft Azure Active Directory (AD) for authentication, including Microsoft 365. This plug-in uses the [Apple single sign on app extension](device-features-configure.md#single-sign-on-app-extension). It reduces the number of authentication prompts users get when using devices managed by Mobile Device Management (MDM), including Microsoft Intune.

Once set up, apps that support the Microsoft Authentication Library (MSAL) automatically take advantage of the Microsoft Enterprise SSO plug-in (preview). Apps that don't support MSAL can be allowed to use the extension. Just add the application bundle ID or prefix to the extension configuration.  

For example, to allow a Microsoft app that doesn't support MSAL, add `com.microsoft.` to the **AppPrefixAllowList** property. Be careful with the apps you allow, they will be able to bypass interactive login prompts for the signed in user.

For more information, see [Microsoft Enterprise SSO plug-in for Apple devices - apps that don't use MSAL](/azure/active-directory/develop/apple-sso-plugin#applications-that-dont-use-msal).  

This article shows how to deploy the Microsoft Enterprise SSO plug-in (preview) for macOS Apple Devices with Intune.

> [!IMPORTANT]
> The Microsoft Enterprise SSO plug-in for Apple Devices is in public preview. This preview version is provided without a service level agreement (SLA). It's not recommended to use in production. Certain features might not be supported or might have restricted behavior. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## Prerequisites

- The device must support the plug-in:
  - macOS 10.15 and newer

- The device is managed with Intune.
  - (Company Portal app installed and configured on the device).

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
       - **macOS**
    - **Profile**: Select **Device features**. Or, select **Templates** > **Device features**.

4. Select **Create**.

:::image type="content" source="./media/apple-enterprise-sso-plug-in/macOS-1.png" alt-text="Device features macOS":::

5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, a good policy name is **macOS: Microsoft Enterprise SSO plug-in**.
    - **Description**: Enter a description for the policy. This setting is optional, but recommended.

6. Select **Next**.
7. In **Configuration settings**, select **Single sign-on app extension**, and configure the following properties:

    - **SSO app extension type**: Select **Microsoft Azure AD**.
    :::image type="content" source="./media/apple-enterprise-sso-plug-in/macOS-2.png" alt-text="Microsoft Azure AD SSO":::

    - **App bundle ID**: Enter a list of bundle IDs for apps that don't support MSAL **and** are allowed to use SSO. For more information, see [Applications that don't use MSAL](/azure/active-directory/develop/apple-sso-plugin#enable-sso-for-apps-that-dont-use-a-microsoft-identity-platform-library).

    - **Additional configuration**: To customize the end user experience, you can add the following properties.

      | Key | Type | Value |
      | --- | --- | --- |
      | **AppPrefixAllowList** | String | Enter a list of prefixes for apps that don't support MSAL **and** are allowed to use SSO. For example, enter `com.microsoft.` to allow all Microsoft apps.<br/><br/>Be sure these apps [meet the allowlist requirements](/azure/active-directory/develop/apple-sso-plugin#enable-sso-for-apps-that-dont-use-a-microsoft-identity-platform-library).|
      | **browser_sso_interaction_enabled** | Integer | When set to `1`, users can sign in from Safari browser, and from apps that don't support MSAL. Enabling this setting allows users to bootstrap the extension from Safari or other apps.|
      | **browser_sso_disable_mfa** | Integer | Set to `0` (default) to require the Microsoft Enterprise SSO plug-in use multi-factor authentication (MFA) during bootstrap. Requiring MFA during bootstrap reduces prompts for MFA in apps that are protected by conditional access and require MFA. Microsoft recommends MFA be enabled to increase security and improve the user experience.<br/><br/>Set to `1` to disable MFA in bootstrap. Users are prompted by individual apps that require MFA. |
      | **disable_explicit_app_prompt** | Integer | Some apps might incorrectly enforce end-user prompts at the protocol layer. If you see this problem, users are prompted to sign in, even though the Microsoft Enterprise SSO plug-in works for other apps. <br/><br/>When set to `1` (one), you reduce these prompts. |

:::image type="content" source="./media/apple-enterprise-sso-plug-in/macOS-3.png" alt-text="Additional configuration":::

      > [!TIP]
      > For more information on these properties, and other properties you can configure, see [Microsoft Enterprise SSO plug-in for Apple devices (preview)](/azure/active-directory/develop/apple-sso-plugin#more-configuration-options).

8. Continue creating the profile, and assign the profile to the users or groups that will receive these settings. For the specific steps, see [Create the profile](device-features-configure.md#create-the-profile).

For guidance on assigning profiles, see [Assign user and device profiles](device-profile-assign.md).

When the device checks in with the Intune service, it will receive this profile.
You can check that the profile was deployed correctly by going to Devices > Configuration Profiles > selecting the profile you have just created and generating a report:
:::image type="content" source="./media/apple-enterprise-sso-plug-in/macOS-4.png" alt-text="Assignement Status Report":::

For more information, see [How long does it take for devices to get a policy](device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned).

## End user experience

:::image type="content" source="./media/apple-enterprise-sso-plug-in/flow-chart-end-user-macOS.png" alt-text="End user flow chart when installing SSO app app extension on macOS devices in Microsoft Intune.":::

- Users sign in to any supported app or website to bootstrap the extension. Bootstrap is the process of signing in for the first time, which sets up the extension.  

:::image type="content" source="./media/apple-enterprise-sso-plug-in/user-signs-in.png" alt-text="Users signs in to app or website to bootstrap the SSO app extension on iOS/iPadOS and macOS devices in Microsoft Intune.":::

- After users sign in successfully, the extension is automatically used to sign in to any other supported app or website.

You can test Single Sign on by opening [Safari in Private mode](https://support.apple.com/guide/safari/browse-privately-ibrw1069/mac)  (opens Apple's web site) and opening the site https://portal.office.com, no username and password will be required.
:::image type="content" source="./media/apple-enterprise-sso-plug-in/macos-sso-animated.gif" alt-text="Users signs in to app or website to bootstrap the SSO app extension on iOS/iPadOS and macOS devices in Microsoft Intune.":::

On macOS, users are prompted to opt in or out of SSO when they sign in to a work or school app. They can select **Don’t ask me again** to opt out of SSO and block future requests.

Users can also manage their SSO preferences in the Company Portal app for macOS. To edit preferences, go to the Company Portal menu bar > **Company Portal** > **Settings**. They can select or deselect **Don’t ask me to sign in with single sign-on for this device**.
:::image type="content" source="./media/apple-enterprise-sso-plug-in/macOS-5.png" alt-text="Don’t ask me to sign in with single sign-on for this device.":::

## Next steps

- For information about the Microsoft Enterprise SSO plug-in, see [Microsoft Enterprise SSO plug-in for Apple devices (preview)](/azure/active-directory/develop/apple-sso-plugin).

- For information from Apple on the single sign-on extension payload, see [Single Sign-On Extensions payload settings](https://support.apple.com/guide/mdm/single-sign-on-extensions-mdmfd9cdf845/web) (opens Apple's web site).
