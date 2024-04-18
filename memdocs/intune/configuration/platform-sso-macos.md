---
# required metadata

title: Configure Platform SSO for macOS devices
description: Use Microsoft Intune to configure Platform SSO for macOS devices. Platform SSO enables single sign-on (SSO) using a Microsoft Entra ID.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/18/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: arnab
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Configure Platform SSO for macOS devices in Microsoft Intune

On your macOS devices, you can configure Platform SSO to enable single sign-on (SSO) using passwordless authentication, Microsoft Entra user accounts, or smart cards. Platform SSO is an enhancement to the [Microsoft Enterprise SSO plug-in](/entra/identity-platform/apple-sso-plugin) and the [SSO app extension](use-enterprise-sso-plug-in-macos-with-intune.md). Platform SSO can sign users into their managed Mac devices using their Microsoft Entra user account and Touch ID.

This article applies to:

- macOS

The [Microsoft Enterprise SSO plug-in](/entra/identity-platform/apple-sso-plugin) in Microsoft Entra includes two SSO features - **Platform SSO** and the **SSO app extension**.

Some benefits of Platform SSO include:

- Go passwordless with phishing-resistant credentials that are hardware-bound to the Mac device.
- The sign in experience is similar to signing into a Windows device with a work or school account, like users do with Windows Hello for Business.
- Helps minimize the number of times users need to enter their Microsoft Entra credentials.
- Helps reduce the number of passwords users need to remember.
- Get the benefits of Microsoft Entra ID Join, which allows any organization user to sign into the device.
- Included with all [Microsoft Intune licensing plans](../fundamentals/licenses.md).

Platform SSO uses the Microsoft Intune [settings catalog](settings-catalog.md) to configure the policy. When the policy is ready, you assign the policy to your users or devices. Microsoft recommends you assign the policy when the device enrolls in Intune. But, it can be assigned at any time, including on existing devices. 

This article shows you how to configure Platform SSO for macOS devices in Intune.

## Prerequisites

- Devices must be macOS 13.0 and newer devices.
- Microsoft Intune [Company Portal app](../apps/apps-company-portal-macos.md) version 5.2401.2 and newer is required. This version includes Platform SSO.

  You can add this app to Intune and deploy it at any time.

  - For information on deploying the Company Portal app, go to [Step 3 - Deploy the Company Portal app](#step-3---deploy-the-company-portal-app-for-macos) (in this article).
  - For information on the end user experience with the Company Portal app, go to [Manage Company Portal preferences for macOS](../user-help/intune-company-portal-preferences-macos.md).

- Supported web browsers include:
  - Microsoft Edge
  - Safari

    When Mac devices join a Microsoft Entra tenant, the devices get a workplace join (WPJ) certificate that is hardware-bound and only accessible by the [Microsoft Enterprise SSO plug-in](/entra/identity-platform/apple-sso-plugin). To access resources protected using Conditional Access, apps and web browsers need this WPJ certificate. With Platform SSO configured, the SSO app extension acts as the broker for Microsoft Entra ID authentication and Conditional Access.

    These browsers are broker-aware and can redirect to the SSO app extension for Microsoft Entra ID authentication or Conditional Access check.

- To create the Intune policy, at a minimum, sign in with an account that has the **Policy and Profile Manager** Intune RBAC role. For more information on RBAC roles in Intune, go to [Role-based access control (RBAC) with Microsoft Intune](../fundamentals/role-based-access-control.md).

## Step 1 - Decide the authentication method

When you create the platform SSO policy in Intune, you need to decide the authentication method you want to use.

??The SSO app extension must also support the method you choose. The SSO app extension must also support the method. In the policy, we enter a set list of URLs. How do we know which auth methods they support? ??

The Platform SSO policy and the authentication method you use changes how users sign in to the devices.

- When you configure Platform SSO, users sign in to their macOS devices with the authentication method you configure.
- When you don't use Platform SSO, users sign in to their macOS devices with a local account. Then, they sign into apps and websites with their Microsoft Entra ID.

Use the information in this step to learn the differences between the authentication methods and how they affect the user sign-in experience.

Your authentication options:

- **Secure Enclave**: When you configure Platform SSO with the **Secure Enclave** authentication method, the SSO plug-in uses hardware-bound cryptographic keys. It doesn't use the Microsoft Entra user account to authenticate the user to apps and websites.

  Microsoft recommends using **Secure Enclave** as the authentication method when configuring Platform SSO.

  **Secure Enclave**:

  - Is considered password-less and meets phish-resistant multifactor (MFA) requirements. It's conceptually similar to Windows Hello for Business. It can also use the same features as Windows Hello for Business, like Conditional Access.
  - Leaves the local account username and password as-is. These values aren't changed.​ This behavior is by design due to Apple's FileVault disk encryption, which uses the local password as the unlock key.
  - After a device reboots, users must enter the local account password. After this initial machine unlock​, Touch ID can be used to unlock the device.
  - After unlock, the device gets the hardware-backed Primary Refresh Token (PRT) for device-wide SSO.​
  - In web browsers, this PRT key can be used as a passkey using [WebAuthN APIs](https://webauthn.guide).
  - Its setup can be bootstrapped with an authentication app for MFA authentication or Microsoft [Temporary Access Pass (TAP)](/entra/identity/authentication/howto-authentication-temporary-access-pass).
  - Enables the creation and usage of Microsoft Entra ID passkeys.

- **Password**: When you configure Platform SSO with the **Password** authentication method, users sign in on the Mac with their Microsoft Entra ID user account instead of their local account password.

  With the **Password** authentication method:

  - The Microsoft Entra password​ replaces the local account password, and keeps the password in sync.

    The local account machine password isn't completely removed from the device. This behavior is by design due to Apple's FileVault disk encryption, which uses the local password as the unlock key.

  - The local account username isn't changed and is left as-is.
  - End users can use Touch ID to sign in to the device.
  - There are fewer passwords for users and admins to remember and manage.​
  - Users must enter their Microsoft Entra password after a device reboots. After this initial machine unlock​, Touch ID can unlock the device.
  - After unlock, the device gets the hardware-bound Primary Refresh Token (PRT) credential for Microsoft Entra SSO.​

- **Smart card**: When you configure Platform SSO with the **Smart card** authentication method, users can use the smart card certificate and the associated PIN to sign in to the device and authenticate to apps and websites.

  This option:

  - Is considered password-less.
  - Leaves the local account username and password as-is. These values aren't changed.​

## Step 2 - Create the Platform SSO policy in Intune

To configure the Platform SSO policy, use the following steps to create an [Intune settings catalog](settings-catalog.md) policy.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration** > **Create** > **New policy**.
3. Enter the following properties:

    - **Platform**: Select **macOS**.
    - **Profile type**: Select **Settings catalog**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, name the policy **macOS - Platform SSO**.
    - **Description**: Enter a description for the policy. This setting is optional, but recommended.

6. Select **Next**.
7. In **Configuration settings**, select **Add settings**. In the settings picker, expand **Authentication**, and select **Extensible Single Sign On (SSO)**:

    :::image type="content" source="./media/platform-sso-macos/settings-picker-authentication-extensible-sso.png" alt-text="Screenshot that shows the Settings Catalog settings picker, and selecting authentication and extensible SSO category in Microsoft Intune.":::

    In the list, select the following settings:

    - **Authentication Method (Deprecated)** (macOS 13 only)
    - **Extension Identifier**
    - Expand **Platform SSO** > select **Authentication Method** (macOS 14+) and **Use Shared Device Keys**
    - **Registration Token**
    - **Screen Locked Behavior**
    - **Team Identifier**
    - **Type**
    - **URLs**

    Close the settings picker.

8. Configure the following settings:

    - **URLs**: Enter the following array of URL prefixes. These URL prefixes are the identity providers that do SSO app extensions. The URLs are required for **redirect** payloads and are ignored for **credential** payloads.

      - `https://login.microsoftonline.com`
      - `https://login.microsoft.com`
      - `https://sts.windows.net`
      - `https://login.partner.microsoftonline.cn`
      - `https://login.chinacloudapi.cn`
      - `https://login.microsoftonline.us`
      - `https://login-us.microsoftonline.com`

      For the URLs to work, they must meet the following requirements:

      - The URLs must begin with `http://` or `https://`.
      - The scheme and host name must match and are case-insensitive.
      - Query parameters and URL fragments aren't allowed.
      - The URLs of all installed Extensible SSO payloads must be unique.

      > [!NOTE]
      > These URLs are required by the Microsoft Enterprise SSO plug-in. For more information, go to [Microsoft Enterprise SSO plug-in for Apple devices](/entra/identity-platform/apple-sso-plugin).

    - **Team Identifier**: Enter `UBF8T346G9`, which is the team identifier of the Enterprise SSO plug-in app extension.
    - **Screen Locked Behavior**: Select **Do Not Handle**. When set to **Do Not Handle**, the request continues without SSO.
    - **Registration token**: Enter the token the device uses for registration with Platform SSO. This token silently registers with the Identity Provider.

      For example, enter `{{DEVICEREGISTRATION}}`. You must include the curly braces. For more information on this registration token, go to [Configure Microsoft Entra device registration](/entra/identity-platform/apple-sso-plugin#configure-microsoft-entra-device-registration).

      This setting requires that you also configure the `AuthenticationMethod` setting.

      - If you use macOS 13 devices, then configure the **Authentication Method (Deprecated)** setting.
      - If you use macOS 14+ devices, then configure the **Platform SSO** > **Authentication Method** setting.
      - If you have a mix of macOS 13 and macOS 14+ devices, then configure both authentication settings in the same profile.

    - **Platform SSO** > **Authentication Method** (macOS 14+): Select the Platform SSO authentication method that you chose in [Step 1 - Decide the authentication method](#step-1---decide-the-authentication-method) (in this article). Make sure you choose the same authentication method that the app extension supports and uses.

      This setting applies to macOS 14 and later. For macOS 13, use the **Authentication Method (Deprecated)** setting.

      Your options:

      - **Password** (default): Enables SSO across apps that use Microsoft Entra ID for authentication.

        Any Intune password policy you configure also affects this setting. For example, if you have a password policy that blocks simple passwords, then simple passwords are also blocked for this setting. Make sure your Intune password policy and/or compliance policy matches your Microsoft Entra password policy. If the policies don't match, then the password might not sync and end users are denied access.

      - **UserSecureEnclaveKey**: Enables SSO across apps that use Microsoft Entra ID for authentication by provisioning a [Secure Enclave](https://developer.apple.com/documentation/security/certificate_key_and_trust_services/keys/protecting_keys_with_the_secure_enclave) cryptographic key.

      - **SmartCard**: Enables SSO across apps that use Microsoft Entra ID for authentication. It uses a smart card or smart card-compatible hard token, like a YubiKey. This token acts as a local machine password.​

    - **Authentication Method (Deprecated)** (macOS 13 only): Select the Platform SSO authentication method that you chose in [Step 1 - Decide the authentication method](#step-1---decide-the-authentication-method) (in this article).

      This setting applies to macOS 13 only. For macOS 14.0 and later, use the **Platform SSO** > **Authentication Method** setting.

      Your options:

      - **Password** (default): Enables SSO across apps that use Microsoft Entra ID for authentication.

        Any Intune password policy you configure also affects this setting. For example, if you have a password policy that blocks simple passwords, then simple passwords are also blocked for this setting. Make sure your Intune password policy and/or compliance policy matches your Microsoft Entra password policy. If the policies don't match, then the password might not sync and end users are denied access.

      - **UserSecureEnclaveKey**: Enables SSO across apps that use Microsoft Entra ID for authentication by provisioning a [Secure Enclave](https://developer.apple.com/documentation/security/certificate_key_and_trust_services/keys/protecting_keys_with_the_secure_enclave) cryptographic key.

    - **Platform SSO** > **Use Shared Device Keys** (macOS 14+): Select **Enabled**.

      When enabled, Platform SSO uses the same signing and encryption keys for all users on the same device. If you enable this setting after a user completes the Platform SSO registration or a Platform SSO user upgrades from macOS 13.x to macOS 14.x after registration, then end users see a prompt to register the device again.

    - **Extension Identifier**: Enter `com.microsoft.CompanyPortalMac.ssoextension`. This ID is the SSO app extension that the profile needs for SSO to work.

      The **Extension Identifier** and **Team Identifier** values work together.

    - **Type**: Select **Redirect**.

9. Select **Next**.
10. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, see [Use RBAC roles and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

11. In **Assignments**, select the users or groups that will receive your profile. For more information on assigning profiles, see [Assign user and device profiles](device-profile-assign.md).

    Select **Next**.

12. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

The next time the device checks for configuration updates, the settings you configured are applied.

## Step 3 - Deploy the Company Portal app for macOS

> [!IMPORTANT]
> Platform SSO requires the [Company Portal app](/mem/intune/apps/apps-company-portal-macos) version 5.2401.2 and newer.

The Company Portal app for macOS deploys and installs the Microsoft Enterprise SSO plug-in. This plug-in enables Platform SSO.

Using Intune policies, you add the Company Portal app, make it a required app, and then deploy the app to your macOS devices:

1. Add the Company Portal app for macOS to Intune and make it a required app. For the steps, go to [Add the Company Portal app for macOS](../apps/apps-company-portal-macos.md).
2. Configure the Company Portal app to include your organization information. For the steps, go to [How to configure the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).

    There aren't any specific steps to configure the app for Platform SSO. Just make sure the latest Company Portal app is added to Intune and deployed to your macOS devices. If you have an older version of the Company Portal app installed, then Platform SSO won't work.

For information on the end user out of box experience (OOBE), go to [Join a Mac device with Microsoft Entra ID during the OOBE with macOS Platform SSO](/entra/identity/devices/device-join-macos-platform-single-sign-on).

## Step 4 - Enroll the devices and apply the policies

To use Platform SSO, the devices must be MDM enrolled in Intune using one of the following methods:

- For **organization-owned devices**, you can:

  - Create an [Automated device enrollment](../enrollment/device-enrollment-program-enroll-macos.md) policy using Apple Business Manager or Apple School Manager.
  - Create a [Direct enrollment](../enrollment/device-enrollment-direct-enroll-macos.md) policy using Apple Configurator.

  Assign your enrollment profile to your macOS devices.

- For **personally-owned devices**, create a [Device enrollment](../fundamentals/deployment-guide-enrollment-macos.md#byod-device-enrollment) policy. With this enrollment method, end users open the Company Portal app and sign in with their Microsoft Entra ID. When they successfully sign-in, the enrollment policy applies.

For **new devices**, we recommend you precreate and configure all the necessary policies, including the enrollment policy. Then, when the devices enroll in Intune, the policies automatically apply.

For **existing devices**, assign the policies to the devices. The next time the devices sync or check-in with the Intune services, they receive the Platform SSO policy settings you create.

On enrolled devices, you can also go to **Settings** > **Privacy and security** > **Profiles**. Your Platform SSO profile is shown under `com.apple.extensiblesso Profile`. Select the profile to see the settings you configured, including the URLs.

## Step 5 - Register the device

When the device receives the policy, there's a **Registration required** notification that pops up or appears in the Notification Center.

End users select this notification, sign in to the Microsoft Entra ID plug-in with their organization account, and complete multifactor authentication (MFA).

When they successfully authenticate, the device is Microsoft Entra-Joined to the organization and the workplace join (WPJ) certificate is bound to the device.

For more information about the different end-user experiences for device registration, go to [Join a Mac device with Microsoft Entra ID](/entra/identity/devices/device-join-microsoft-entra-company-portal).

## Step 6 - Confirm the settings on the device

Once Platform SSO registration completes, you can confirm that Platform SSO is configured. For the steps, go to [Microsoft Entra ID - Check your device registration status](/entra/identity/devices/device-join-macos-platform-single-sign-on#check-your-device-registration-status).

To troubleshoot Platform SSO, go to [macOS Platform single sign-on known issues and troubleshooting](/entra/identity/devices/troubleshoot-macos-platform-single-sign-on-extension).

## Step 7 - Unassign any existing SSO app extension profiles

After you confirm that your settings catalog policy is working, then we recommend you unassign any existing [SSO app extension](use-enterprise-sso-plug-in-macos-with-intune.md) profiles created using the Intune Device Features template.

Both policies can coexist as you test the settings catalog policy. But, when testing is complete, be sure you unassign any SSO app extension profiles.

## More Platform SSO settings you can configure

When you create the settings catalog profile in [Step 2 - Create the Platform SSO policy in Intune](#step-2---create-the-platform-sso-policy-in-intune), there are more settings that you can configure.

The following settings let you customize the end-user experience and give more granular control on user privileges.

| Platform SSO settings | Possible values  | Usage |
| --- | --- | --- |
| **Account Display Name**  | Any string value. | Customize the organization name end users see in the Platform SSO notifications. |
| **Enable Create User At Login** | **Enable** or **Disable**. | Allow any organizational user to sign in to the device using their Microsoft Entra credentials.  |
| **New User Authorization Mode** | **Standard**, **Admin**, or **Groups** | One-time permissions the user has at sign-in when the account is created using Platform SSO. Currently, **Standard** and **Admin** values are supported. At least one **Admin** user is required on the device before **Standard** mode can be used.|
| **User Authorization Mode** | **Standard**, **Admin**, or **Groups** | Persistent permissions the user has at sign-in each time the user authenticates using Platform SSO. Currently, **Standard** and **Admin** values are supported. At least one **Admin** user is required on the device before **Standard** mode can be used.|

> [!NOTE]
> Any undocumented Platform SSO settings aren't supported.

## Related articles

- [Microsoft Enterprise SSO plug-in](/entra/identity-platform/apple-sso-plugin)
- [Use the Microsoft Enterprise SSO app extension on macOS devices](use-enterprise-sso-plug-in-macos-with-intune.md)
- [What is a Primary Refresh Token (PRT)?](/entra/identity/devices/concept-primary-refresh-token)
- [macOS Platform single sign-on known issues and troubleshooting](/entra-docs-pr/blob/release-macos-platform-sso/docs/identity/devices/troubleshoot-macos-platform-single-sign-on-extension.md)
