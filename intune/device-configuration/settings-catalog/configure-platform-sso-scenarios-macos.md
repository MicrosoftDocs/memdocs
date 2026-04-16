---
title: Platform SSO scenarios for macOS devices
description: Use Microsoft Intune to configure common Platform SSO scenarios for macOS devices. You can enable Kerberos SSO to on-premises Active Directory and cloud-based Microsoft Entra ID, use Touch ID biometric policy with Secure Enclave authentication, and enable SSO on non-Microsoft apps. You can also configure end user experience settings.
ms.date: 04/27/2026
author: MandiOhlinger
ms.author: mandia
ms.topic: how-to
appliesto:
- ✅ macOS
ms.reviewer: arnab, veenasoman
ms.collection: M365-identity-device-management
---

# Common Platform SSO scenarios for macOS devices in Microsoft Intune

On macOS devices, you can configure [Platform SSO](./configure-platform-sso-macos.md) in Microsoft Intune to enable single sign-on (SSO) with your Microsoft Entra accounts. Platform SSO lets users access resources on their macOS devices without entering their credentials repeatedly.

When Platform SSO is configured, you can use the scenarios described in this article to use Kerberos SSO authentication to on-premises resources, enhance security with biometrics, enable SSO on non-Microsoft apps, and improve the user experience.

This feature applies to:

- macOS

## Before you begin

- You must [configure Platform SSO for macOS devices in Microsoft Intune](./configure-platform-sso-macos.md) before you configure the scenarios in this article. When you configure it, you create a Platform SSO settings catalog policy that you use to add the scenarios described in this article.

- You can assign only one SSO policy to your groups. So if you already configured Platform SSO, add these scenario settings to your existing Platform SSO settings catalog policy.

- To update your existing settings catalog policy, at a minimum, sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) with an account that has the following Intune permissions:

  - Device Configuration **Read**, **Create**, **Update**, and **Assign** permissions

  Some built-in roles have these permissions, including the built-in **Policy and Profile Manager** Intune role. For more information on RBAC roles in Intune, see [Role-based access control (RBAC) with Microsoft Intune](../../intune-service/fundamentals/role-based-access-control.md).

## Enable Kerberos SSO to on-premises Active Directory and Microsoft Entra ID

Applies to:

- Company Portal version 2508 and newer

Microsoft Entra issues on-premises and cloud-based Kerberos Ticket Granting Tickets (TGTs). Using Platform SSO, you can configure these TGTs to access on-premises Active Directory and Microsoft Entra ID using [Apple's Kerberos SSO extension](https://support.apple.com/guide/deployment/depe6a1cda64/web) (opens Apple's website).

If you want your users to have SSO access to on-premises and cloud resources that use Kerberos authentication, then this scenario is for you. To learn more about Kerberos SSO in Microsoft Entra, see [Enable Kerberos SSO to on-premises Active Directory and Microsoft Entra ID Kerberos resources in Platform SSO](/entra/identity/devices/device-join-macos-platform-single-sign-on-kerberos-configuration).

In your existing Platform SSO settings catalog policy, add the **Extension Data** setting. The **Extension Data** setting is a similar concept to an open text field; you can configure any values you need.

1. In your existing Platform SSO settings catalog policy, add **Extension Data**:

    1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) (**Devices** > **Manage devices** > **Configuration**), select your existing Platform SSO settings catalog policy.
    2. In **Properties** > **Configuration settings**, select **Edit** > **Add settings**.
    3. In the settings picker, expand **Authentication**, and select **Extensible Single Sign On (SSO)**:

        :::image type="content" source="./media/configure-platform-sso-scenarios-macos/settings-picker-authentication-extensible-sso.png" alt-text="Screenshot of the Settings Catalog settings picker with the authentication and extensible SSO category selected in Microsoft Intune." lightbox="./media/configure-platform-sso-scenarios-macos/settings-picker-authentication-extensible-sso.png":::

    4. In the list, select **Extension Data** and close the settings picker:

        :::image type="content" source="./media/configure-platform-sso-scenarios-macos/settings-picker-authentication-extensible-sso-extension-data.png" alt-text="Screenshot of the Settings Catalog settings picker with authentication and Extension Data selected in Microsoft Intune." lightbox="./media/configure-platform-sso-scenarios-macos/settings-picker-authentication-extensible-sso-extension-data.png":::

2. In **Extension Data**, **Add** the following key and your preferred value. Only enter one value for the key.

    | Key | Type  | Value | Description |
    | --- | --- | --- | --- |
    | **custom_tgt_setting**  | Integer | `0`| **Both On-Prem and Cloud TGTs** (default) – Maps both on-premises and cloud TGTs. |
    | &nbsp; | &nbsp; | `1` | **On-Prem TGT Only** – Maps only the on-premises TGT. |
    | &nbsp; | &nbsp; | `2` | **Cloud TGT Only** – Maps only the cloud-based TGT. |
    | &nbsp; | &nbsp; | `3` | **No TGTs** – Disables TGT mapping entirely. |

3. Select **Next** to save your changes, and complete the policy. If the policy is already assigned to users or groups, then these groups receive the policy changes the next time they [sync with the Intune service](../troubleshoot-device-profiles.md#policy-refresh-intervals).

## Configure Touch ID biometric policy with Secure Enclave authentication

On devices that support Touch ID biometric authentication, use the Secure Enclave authentication option, as described in [Configure Platform SSO for macOS devices in Microsoft Intune](./configure-platform-sso-macos.md).

This policy requires users to authenticate with Touch ID whenever the User Secure Enclave Key needs to be accessed. To learn more about `UserSecureEnclaveKeyBiometricPolicy`, see [UserSecureEnclaveKeyBiometricPolicy](/entra/identity/devices/macos-psso#microsoft-platform-sso-usersecureenclavekeybiometricpolicy).

Add the **Extension Data** setting to your existing Platform SSO settings catalog policy.

1. In your existing Platform SSO settings catalog policy, add **Extension Data**:

    1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) (**Devices** > **Manage devices** > **Configuration**), select your existing Platform SSO settings catalog policy.
    2. In **Properties** > **Configuration settings**, select **Edit** > **Add settings**.
    3. In the settings picker, expand **Authentication**, and select **Extensible Single Sign On (SSO)**:

        :::image type="content" source="./media/configure-platform-sso-scenarios-macos/settings-picker-authentication-extensible-sso.png" alt-text="Screenshot that shows the Settings Catalog settings picker, and selecting authentication and extensible SSO category in Microsoft Intune." lightbox="./media/configure-platform-sso-scenarios-macos/settings-picker-authentication-extensible-sso.png":::

    4. In the list, select **Extension Data** and close the settings picker:

        :::image type="content" source="./media/configure-platform-sso-scenarios-macos/settings-picker-authentication-extensible-sso-extension-data.png" alt-text="Screenshot that shows the Settings Catalog settings picker, and selecting authentication and Extension Data in Microsoft Intune." lightbox="./media/configure-platform-sso-scenarios-macos/settings-picker-authentication-extensible-sso-extension-data.png":::

2. In **Extension Data**, **Add** the following key and value:

    | Key | Type  | Value | Description |
    | --- | --- | --- | --- |
    | **enable_se_key_biometric_policy**  | Boolean | True | Copy and paste this value. |

3. Select **Next** to save your changes, and complete the policy. If the policy is already assigned to users or groups, then these groups receive the policy changes the next time they [sync with the Intune service](../troubleshoot-device-profiles.md#policy-refresh-intervals).

## Enable SSO for non-Microsoft apps with Microsoft Enterprise SSO Extension

If you previously used the Microsoft Enterprise SSO Extension, and/or want to enable SSO on non-Microsoft apps, then add the **Extension Data** setting to your existing Platform SSO settings catalog policy.

In this scenario, we use the **Extension Data** setting to:

- Configure settings you used in your previous Microsoft Enterprise SSO Extension Intune policy.
- Configure settings that allow non-Microsoft apps to use SSO.

This scenario lists the minimum recommended settings you should add. If you had a previous Microsoft Enterprise SSO Extension policy, you might have configured more settings. We recommend you add any other key & value pair settings you configured in your previous Microsoft Enterprise SSO Extension policy.

The following settings are commonly recommended for configuring SSO settings, including configuring SSO support for non-Microsoft applications.

1. In your existing Platform SSO settings catalog policy, add **Extension Data**:

    1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) (**Devices** > **Manage devices** > **Configuration**), select your existing Platform SSO settings catalog policy.
    2. In **Properties** > **Configuration settings**, select **Edit** > **Add settings**.
    3. In the settings picker, expand **Authentication**, and select **Extensible Single Sign On (SSO)**:

        :::image type="content" source="./media/configure-platform-sso-scenarios-macos/settings-picker-authentication-extensible-sso.png" alt-text="Screenshot that shows the Settings Catalog settings picker, and selecting authentication and extensible SSO category in Microsoft Intune." lightbox="./media/configure-platform-sso-scenarios-macos/settings-picker-authentication-extensible-sso.png":::

    4. In the list, select **Extension Data** and close the settings picker:

        :::image type="content" source="./media/configure-platform-sso-scenarios-macos/settings-picker-authentication-extensible-sso-extension-data.png" alt-text="Screenshot that shows the Settings Catalog settings picker, and selecting authentication and Extension Data in Microsoft Intune." lightbox="./media/configure-platform-sso-scenarios-macos/settings-picker-authentication-extensible-sso-extension-data.png":::

2. In **Extension Data**, **Add** the following keys and values:

    | Key | Type  | Value | Description |
    | --- | --- | --- | --- |
    | **AppPrefixAllowList**  | String | `com.microsoft.,com.apple.` | Copy and paste this value in the setting. <br/><br/>**AppPrefixAllowList** lets you create a list of app vendors with apps that can use SSO. You can add more app vendors to this list as needed. |
    | **browser_sso_interaction_enabled** | Integer | `1` | Configures a recommended broker setting. |
    | **disable_explicit_app_prompt** | Integer | `1` | Configures a recommended broker setting. |

    The following example shows the recommended configuration:

    :::image type="content" source="./media/configure-platform-sso-scenarios-macos/extension-data-appprefixallowlist.png" alt-text="Screenshot of the Extension Data configuration showing AppPrefixAllowList and other Platform SSO settings in Microsoft Intune." lightbox="./media/configure-platform-sso-scenarios-macos/extension-data-appprefixallowlist.png":::

3. Select **Next** to save your changes, and complete the policy. If the policy is already assigned to users or groups, then these groups receive the policy changes the next time they [sync with the Intune service](../troubleshoot-device-profiles.md#policy-refresh-intervals).

## Apply Platform SSO policy during Automated Device Enrollment with Setup Assistant

When you enroll macOS devices using Automated Device Enrollment (ADE), you can apply the Platform SSO policy during the Setup Assistant experience. When users arrive at the desktop, they have a more integrated sign-in experience on the device and can access Microsoft Entra ID resources immediately.

For more information, see [Configure Platform Single Sign-On (PSSO) during Automated Device Enrollment for macOS devices](configure-platform-sso-during-enrollment.md).

## End user experience settings for Platform SSO

There are some settings that customize the end-user experience and give more granular control on user privileges. Any undocumented Platform SSO settings aren't supported.

In your existing Platform SSO settings catalog policy, use the following optional settings:

| Platform SSO settings | Possible values  | Usage |
| --- | --- | --- |
| **Account Display Name**  | Any string value | Customize the organization name end users see in the Platform SSO notifications. |
| **Enable Create User At Login** | **Enable** or **Disable** | Allow any organizational user to sign in to the device using their Microsoft Entra credentials. When you create new local accounts, the provided username and password must be the same as the user's Microsoft Entra ID UPN (`user@contoso.com`) and password.|
| **New User Authorization Mode** | **Standard**, **Admin**, or **Groups** | One-time permissions the user has at sign-in when the account is created using Platform SSO. Currently, **Standard** and **Admin** values are supported. At least one **Admin** user is required on the device before **Standard** mode can be used.|
| **User Authorization Mode** | **Standard**, **Admin**, or **Groups** | Persistent permissions the user has at sign-in each time the user authenticates using Platform SSO. Currently, **Standard** and **Admin** values are supported. At least one **Admin** user is required on the device before **Standard** mode can be used.|
| **Non Platform SSO Accounts** | Enter the local account names you want to exclude from Platform SSO. | This list of local accounts aren't prompted to register for Platform SSO. This setting is appropriate for accounts that shouldn't be registered with a Microsoft Entra account, like the local admin account. The accounts listed in this policy aren't subject to the `FileVaultPolicy`, `LoginPolicy`, or `UnlockPolicy`. |
| **FileVault Policy** | **AttemptAuthentication**, **RequireAuthentication**, **AllowOfflineGracePeriod** or **AllowAuthenticationGracePeriod** | Use **AttemptAuthentication** to force the device to verify the Microsoft Entra ID password with Microsoft Entra when a Mac device is turned on. This setting applies to macOS 15 and later. |

## Related articles

- [Platform SSO for macOS devices](./configure-platform-sso-macos.md)
