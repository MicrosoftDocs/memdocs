---
title: Configure Platform SSO for macOS devices
description: Use Microsoft Intune to configure Platform SSO and deploy the configuration to your macOS devices. Platform SSO enables single sign-on (SSO) using Microsoft Entra ID with the Secure Enclave, smart card, or password authentication methods. You create a settings catalog policy to configure the settings. This article is a step-by-step guide to configure Platform SSO for macOS devices using Intune.
author: MandiOhlinger
ms.author: mandia
ms.date: 11/24/2025
ms.topic: how-to
appliesto:
- ✅ macOS
ms.reviewer: arnab, veenasoman
ms.collection:
- M365-identity-device-management
---

# Platform SSO configuration guide for macOS devices using Microsoft Intune

You can configure Platform SSO to enable single sign-on (SSO) for your macOS devices using passwordless authentication, Microsoft Entra ID user accounts, or smart cards. Platform SSO is a Microsoft Entra feature that enhances the [Microsoft Enterprise SSO plug-in](/entra/identity-platform/apple-sso-plugin) and the [SSO app extension](use-enterprise-sso-plug-in-macos-with-intune.md).

This feature applies to:

- macOS

Platform SSO can sign users into their managed Mac devices using their Microsoft Entra ID credentials and Touch ID. You can use Intune to configure Platform SSO and deploy the Platform SSO configuration to your macOS devices.

The [Microsoft Enterprise SSO plug-in](/entra/identity-platform/apple-sso-plugin) in Microsoft Entra ID includes two SSO features - **Platform SSO** and the **SSO app extension**. This article focuses on configuring [Platform SSO with Microsoft Entra ID](/entra/identity/devices/macos-psso).

This article shows you how to configure Platform SSO for macOS devices in Intune. For some common Platform SSO scenarios you can also configure, go to [Common Platform SSO scenarios for macOS devices](platform-sso-scenarios.md).

## Benefits

Some benefits of Platform SSO include:

- It includes the SSO app extension. You don't configure the SSO app extension separately.
- You can go passwordless with phishing-resistant credentials that are hardware-bound to the Mac device.
- The sign in experience is similar to signing into a Windows device with a work or school account, like users do with Windows Hello for Business.
- It helps minimize the number of times users need to enter their Microsoft Entra ID credentials.
- It helps reduce the number of passwords users need to remember.
- You get the benefits of Microsoft Entra join, which allows any organization user to sign into the device.
- It's included with all [Microsoft Intune licensing plans](../fundamentals/licenses.md).

## How it works

When Mac devices join a Microsoft Entra ID tenant, the devices get a workplace join (WPJ) certificate. This WPJ certificate is hardware-bound and is only accessible by the [Microsoft Enterprise SSO plug-in](/entra/identity-platform/apple-sso-plugin). To access resources protected using Conditional Access, apps and web browsers need this WPJ certificate.

With Platform SSO configured, the SSO app extension acts as the broker for Microsoft Entra ID authentication and Conditional Access.

You configure Platform SSO using the Intune [settings catalog](settings-catalog.md). When the settings catalog policy is ready, you assign the policy. Microsoft recommends you assign the policy when the user enrolls the device in Intune. But, it can be assigned at any time, including on existing devices.

## Prerequisites

- Devices must be running macOS 13.0 and newer.

- Microsoft Intune [Company Portal app](../apps/apps-company-portal-macos.md) version **5.2404.0** and newer is required on the devices. This version includes Platform SSO.

- The following web browsers support Platform SSO:

  - Microsoft Edge
  - Google Chrome with the [Microsoft Single Sign On extension](https://chromewebstore.google.com/detail/windows-accounts/ppnbnpeolgkicgegkbkbjmhlideopiji)

    Using an [Intune preference file (.plist) policy](preference-file-settings-macos.md), you can force this extension to install. In your `.plist` file, you need some of the information at [Chrome Enterprise policy - ExtensionInstallForcelist](https://chromeenterprise.google/policies/?policy=ExtensionInstallForcelist) (opens Google's web site).

    > [!WARNING]
    > There are sample `.plist` files at [ManagedPreferencesApplications examples on GitHub](https://github.com/ProfileCreator/ProfileManifests/tree/master/Manifests/ManagedPreferencesApplications). This GitHub repository is not owned, not maintained, and not created by Microsoft. Use the information at your own risk.

  - Safari

  You can use Intune to add web browser apps, including [package (`.pkg`)](../apps/lob-apps-macos.md) and [disk image (`.dmg`)](../apps/lob-apps-macos-dmg.md) files, and deploy the app to your macOS devices. To get started, go to [Add apps to Microsoft Intune](../apps/apps-add.md).

- Platform SSO uses the Intune settings catalog to configure the required settings. To create the settings catalog policy, at a minimum, sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) with an account that has the following Intune permissions:

  - Device Configuration **Read**, **Create**, **Update**, and **Assign** permissions

  There are some built-in roles that have these permissions, including the **Policy and Profile Manager** Intune role. For more information on RBAC roles in Intune, go to [Role-based access control (RBAC) with Microsoft Intune](../fundamentals/role-based-access-control.md).

- In [Step 2 - Create the Platform SSO policy](#step-2---create-the-platform-sso-policy-in-intune) (this article), you create a settings catalog policy that configures the required settings for Platform SSO. There are other common scenarios and settings you can configure in this policy. For more information, go to [Common Platform SSO scenarios for macOS devices](platform-sso-scenarios.md).

  We recommend you review the [scenarios](platform-sso-scenarios.md) **before** you create the settings catalog policy. This way, you can configure the settings you need/want when you initially create the policy. If you don't configure the optional scenario settings initially, you can always edit the policy later. Only one SSO policy can be assigned to your groups. So, add these scenario settings to your existing Platform SSO settings catalog policy.

- In [Step 5 - Register the device](#step-5---register-the-device) (this article), users register their devices. These users must be allowed to join devices to Microsoft Entra ID. For more information, go to [Configure your device settings](/entra/identity/devices/device-join-plan#configure-your-device-settings).

## Step 1 - Decide the authentication method

When you create the platform SSO policy in Intune, you need to decide the authentication method you want to use.

The Platform SSO policy and the authentication method you use changes how users sign in to the devices.

- When you configure Platform SSO, users sign in to their macOS devices with the authentication method you configure.
- When you don't use Platform SSO, users sign in to their macOS devices with a local account. Then, they sign into apps and websites with their Microsoft Entra ID.

In this step, use the information to learn the differences with the authentication methods and how they affect the user sign-in experience.

> [!TIP]
> Microsoft recommends using **Secure Enclave** as the authentication method when configuring Platform SSO.

| Feature | Secure Enclave | Smart Card | Password |
|---|---|---|---|
|**Passwordless (phishing resistant)**|✅|✅|❌|
|**TouchID supported for unlock**|✅|✅|✅|
|**Can be used as passkey**|✅|❌|❌|
|**MFA mandatory for setup** </br></br> Multifactor authentication (MFA) is always recommended|✅|✅|❌|
|**Local Mac password synced with Entra ID**|❌|❌|✅|
|**Supported on macOS 13.x +**|✅|❌|✅|
|**Supported on macOS 14.x +**|✅|✅|✅|
|**Optionally, allow new users to log in with Entra ID credentials (macOS 14.x +)**|✅|✅|✅|

### Option 1 - Secure Enclave (recommended)

When you configure Platform SSO with the **Secure Enclave** authentication method, the SSO plug-in uses hardware-bound cryptographic keys. It doesn't use the Microsoft Entra credentials to authenticate the user to apps and websites.

For more information on Secure Enclave, go to [Secure Enclave](https://developer.apple.com/documentation/security/certificate_key_and_trust_services/keys/protecting_keys_with_the_secure_enclave) (opens Apple's web site).

Secure Enclave:

- Is considered password-less and meets phish-resistant multifactor (MFA) requirements. It's conceptually similar to Windows Hello for Business. It can also use the same features as Windows Hello for Business, like Conditional Access.
- Leaves the local account username and password as-is. These values aren't changed.​ This behavior is by design due to Apple's FileVault disk encryption, which uses the local password as the unlock key.
- After a device reboots, users must enter the local account password. After this initial machine unlock​, Touch ID can be used to unlock the device.
- After the unlock, the device gets the hardware-backed Primary Refresh Token (PRT) for device-wide SSO.​
- In web browsers, this PRT key can be used as a passkey using [WebAuthN APIs](https://webauthn.guide).
- Its setup can be bootstrapped with an authentication app for MFA authentication or Microsoft [Temporary Access Pass (TAP)](/entra/identity/authentication/howto-authentication-temporary-access-pass).
- Enables the creation and usage of Microsoft Entra ID passkeys.

### Option 2 - Smart Card

When you configure Platform SSO with the **Smart card** authentication method, users can use the smart card certificate and the associated PIN to sign in to the device and authenticate to apps and websites.

This option:

- Is considered password-less.
- Leaves the local account username and password as-is. These values aren't changed.​

For more information, go to [Microsoft Entra certificate-based authentication on iOS and macOS](/entra/identity/authentication/concept-certificate-based-authentication-mobile-ios).

### Option 3 - Password

When you configure Platform SSO with the **Password** authentication method, users sign in to the device with their Microsoft Entra ID user account instead of their local account password.

This option enables SSO across apps that use Microsoft Entra ID for authentication.

With the **Password** authentication method:

- The Microsoft Entra ID password​ replaces the local account password, and the two passwords are kept in sync.

  The local account machine password isn't completely removed from the device. This behavior is by design due to Apple's FileVault disk encryption, which uses the local password as the unlock key.

- The local account username isn't changed and stays as-is.
- End users can use Touch ID to sign in to the device.
- There are fewer passwords for users and admins to remember and manage.​
- Users must enter their Microsoft Entra ID password after a device reboots. After this initial machine unlock​, Touch ID can unlock the device.
- After the unlock, the device gets the hardware-bound Primary Refresh Token (PRT) credential for Microsoft Entra ID SSO.​

> [!NOTE]
> Any Intune password policy you configure also affects this setting. For example, if you have a password policy that blocks simple passwords, then simple passwords are also blocked for this setting.
>
> Make sure your Intune password policy and/or compliance policy matches your Microsoft Entra password policy. If the policies don't match, then the password might not sync and end users are denied access.

#### Configure keyvault recovery (optional)

When using password sync authentication, you can enable keyvault recovery to ensure that data can be recovered if a user forgets their password. IT Admins should review Apple's documentation and evaluate whether using Institutional FileVault Recovery Keys is a good option for them.

- [Manage FileVault with mobile device management](https://support.apple.com/en-ie/guide/deployment/dep0a2cb7686/web)
- [FileVault MDM payload settings for Apple devices](https://support.apple.com/en-ie/guide/deployment/dep32bf53500/1/web/1.0)

## Step 2 - Create the Platform SSO policy in Intune

To configure the Platform SSO policy, use the steps in this section to create an [Intune settings catalog](settings-catalog.md) policy. The Microsoft Enterprise SSO plug-in requires the settings listed.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy**.
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

    - **Authentication Method (Deprecated)** (Select for macOS 13 only)
    - **Extension Identifier**
    - Expand **Platform SSO**:
      - Select **Authentication Method** (Select for macOS 14+)
      - Select **FileVault Policy** (Select for macOS 15+)
      - Select **Token To User Mapping**
      - Select **Use Shared Device Keys**
    - **Registration Token**
    - **Screen Locked Behavior**
    - **Team Identifier**
    - **Type**
    - **URLs**

    Close the settings picker.

    > [!TIP]
    > There are more Platform SSO settings you can add to the policy that configure different scenarios, like enabling Kerberos SSO, using Touch ID biometric authentication, and enabling SSO on non-Microsoft apps. To learn more about these scenarios and their required settings, go to [Common Platform SSO scenarios for macOS devices](platform-sso-scenarios.md).
    >
    > If you don't configure the optional scenario settings initially, you can always edit the policy later.

8. Configure the following required settings:

    | Name | Configuration value | Description |
    |---|---|---|
    | **Authentication Method (Deprecated)** </br>(macOS 13 only) | **Password** or **UserSecureEnclaveKey** | Select the Platform SSO authentication method that you chose in [Step 1 - Decide the authentication method](#step-1---decide-the-authentication-method) (in this article). <br/><br/>This setting applies to macOS 13 only. For macOS 14.0 and later, use the **Platform SSO** > **Authentication Method** setting.|
    | **Extension Identifier** | `com.microsoft.CompanyPortalMac.ssoextension` | Copy and paste this value in the setting. <br/><br/>This ID is the SSO app extension that the profile needs for SSO to work. <br/><br/> The **Extension Identifier** and **Team Identifier** values work together. |
    | **Platform SSO** > **Authentication Method** </br>(macOS 14+) | **Password**, **UserSecureEnclaveKey**, or **SmartCard** | Select the Platform SSO authentication method that you chose in [Step 1 - Decide the authentication method](#step-1---decide-the-authentication-method) (in this article). <br/><br/>This setting applies to macOS 14 and later. For macOS 13, use the **Authentication Method (Deprecated)** setting. |
    | **Platform SSO** > **FileVault Policy** </br>(macOS 15+) | `AttemptAuthentication` | Applies when you select **Password** for the **Authentication Method** setting. Copy and paste this value in the setting. <br/><br/> This setting allows the device to verify the Microsoft Entra ID password with Microsoft Entra at the FileVault unlock screen when a Mac device is turned on. <br/><br/>This setting applies to macOS 15 and later. |
    | **Platform SSO** > **Use Shared Device Keys** </br>(macOS 14+) | **Enabled** | When enabled, Platform SSO uses the same signing and encryption keys for all users on the same device. </br></br>Users upgrading from macOS 13.x to 14.x are prompted to register again. |
    | **Registration token** | `{{DEVICEREGISTRATION}}` | Copy and paste this value in the setting. You must include the curly braces. <br/><br/>To learn more about this registration token, go to [Configure Microsoft Entra device registration](/entra/identity-platform/apple-sso-plugin#configure-microsoft-entra-device-registration). <br/><br/>This setting requires that you also configure the `AuthenticationMethod` setting.<br/><br/>- If you use only macOS 13 devices, then configure the **Authentication Method (Deprecated)** setting.<br/>- If you use only macOS 14+ devices, then configure the **Platform SSO** > **Authentication Method** setting.<br/>- If you have a mix of macOS 13 and macOS 14+ devices, then configure both authentication settings in the same profile. |
    | **Screen Locked Behavior** | **Do Not Handle** | When set to **Do Not Handle**, the request continues without SSO. |
    | **Token To User Mapping** > **Account Name** | `preferred_username` | Copy and paste this value in the setting. <br/><br/>This token specifies that the Microsoft Entra [`preferred_username`](/entra/identity-platform/id-token-claims-reference#payload-claims) attribute value is used for the macOS account's Account Name value. |
    | **Token To User Mapping** > **Full Name** | `name` | Copy and paste this value in the setting. <br/><br/>This token specifies that the Microsoft Entra [`name`](/entra/identity-platform/id-token-claims-reference#payload-claims) claim is used for the macOS account's Full Name value. |
    | **Team Identifier** | `UBF8T346G9` | Copy and paste this value in the setting. <br/><br/>This identifier is the team identifier of the Enterprise SSO plug-in app extension. |
    | **Type** | Redirect | |
    | **URLs** | Copy and paste all the following URLs: <br/><br/>`https://login.microsoftonline.com` <br/> `https://login.microsoft.com` <br/> `https://sts.windows.net` <br/><br/> If your environment needs to allow sovereign cloud domains, like Azure Government or Azure China 21Vianet, then also add the following URLs: <br/><br/> `https://login.partner.microsoftonline.cn` <br/> `https://login.chinacloudapi.cn` <br/> `https://login.microsoftonline.us` <br/> `https://login-us.microsoftonline.com` | These URL prefixes are the identity providers that do SSO app extensions. The URLs are required for **redirect** payloads and are ignored for **credential** payloads. <br/><br/>For more information on these URLs, go to [Microsoft Enterprise SSO plug-in for Apple devices](/entra/identity-platform/apple-sso-plugin). |

    > [!IMPORTANT]
    > If you have a mix of macOS 13 and macOS 14+ devices in your environment, then configure the **Platform SSO** > **Authentication Method** and the **Authentication Method (Deprecated)** authentication settings in the same profile.

    When the profile is ready, it looks similar to the following example:

    :::image type="content" source="./media/platform-sso-macos/intune-psso-device-profile.png" alt-text="Screenshot that shows the recommended Platform SSO settings in an Intune MDM profile.":::

10. Select **Next**.
11. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, go to [Use RBAC roles and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

12. In **Assignments**, select the user or device groups that receive your profile. For devices with user affinity, assign to users or user groups. For devices with multiple users that are enrolled without user affinity, assign to devices or device groups.

    > [!IMPORTANT]
    > For Platform SSO settings on devices with user affinity, it's not supported to assign to device groups or filters. When you use device group assignment or user group assignment with filters on devices with user affinity, the user might be unable to access resources protected by Conditional Access. This issue can happen:
    >
    > - If the Platform SSO settings are applied incorrectly, or,
    > - If the Company Portal app bypasses Microsoft Entra device registration when Platform SSO isn't enabled

    For more information on assigning profiles, go to [Assign user and device profiles](device-profile-assign.md).

    Select **Next**.

13. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

The next time the device checks for configuration updates, the settings you configured are applied.

### Learn more

- To learn more about the plug-in, go to [Microsoft Enterprise SSO plug-in for Apple devices](/entra/identity-platform/apple-sso-plugin).
- For details about the payload settings for the Extensible Single Sign-on extension, go to [Extensible Single Sign-on MDM payload settings for Apple devices](https://support.apple.com/guide/deployment/depfd9cdf845/web) (opens Apple's web site).

## Step 3 - Deploy the Company Portal app for macOS

The Company Portal app for macOS deploys and installs the Microsoft Enterprise SSO plug-in. This plug-in enables Platform SSO.

Using Intune, you can add the Company Portal app and deploy it as a required app to your macOS devices:

- [Add the Company Portal app for macOS](../apps/apps-company-portal-macos.md) lists the steps.
- Configure the Company Portal app to include your organization information (optional). For the steps, go to [How to configure the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).

There aren't any specific steps to configure the app for Platform SSO. Just make sure the latest Company Portal app is added to Intune and deployed to your macOS devices.

If you have an older version of the Company Portal app installed, then Platform SSO fails.

## Step 4 - Enroll the devices and apply the policies

To use Platform SSO, the devices must be MDM enrolled in Intune using one of the following methods:

- For **organization-owned devices**, you can:

  - Create an [Automated device enrollment](../enrollment/device-enrollment-program-enroll-macos.md) policy using Apple Business Manager or Apple School Manager.
  - Create a [Direct enrollment](../enrollment/device-enrollment-direct-enroll-macos.md) policy using Apple Configurator.

- For **personally-owned devices**, create a [Device enrollment](../fundamentals/deployment-guide-enrollment-macos.md#byod-device-enrollment) policy. With this enrollment method, end users open the Company Portal app and sign in with their Microsoft Entra ID. When they successfully sign in, the enrollment policy applies.

For **new devices**, we recommend you precreate and configure all the necessary policies, including the enrollment policy. Then, when the devices enroll in Intune, the policies automatically apply.

For **existing devices** already enrolled in Intune, assign the Platform SSO policy to your users or user groups. The next time the devices sync or check-in with the Intune service, they receive the Platform SSO policy settings you create.

## Step 5 - Register the device

When the device receives the policy, there's a **Registration required** notification that shows in the Notification Center.

:::image type="content" border="false" source="./media/platform-sso-macos/platform-sso-macos-registration-required.png" alt-text="Screenshot that shows the registration required prompt on end user devices when you configure Platform SSO in Microsoft Intune.":::

- End users select this notification, sign in to the Microsoft Entra ID plug-in with their organization account, and complete multifactor authentication (MFA), if required.

  > [!NOTE]
  > MFA is a feature of Microsoft Entra. Make sure MFA is enabled in your tenant. For more information, including any other app requirements, go to [Microsoft Entra multifactor authentication](/entra/identity/authentication/concept-mfa-howitworks).

- When they successfully authenticate, the device is Microsoft Entra-joined to the organization and the workplace join (WPJ) certificate is bound to the device.

The following articles show the user experience, depending on the enrollment method:

- [Join a Mac device with Microsoft Entra ID](/entra/identity/devices/device-join-microsoft-entra-company-portal).
- [Join a Mac device with Microsoft Entra ID during the OOBE with macOS Platform SSO](/entra/identity/devices/device-join-macos-platform-single-sign-on).

## Step 6 - Confirm the settings on the device

When Platform SSO registration completes, you can confirm that Platform SSO is configured. For the steps, go to [Microsoft Entra ID - Check your device registration status](/entra/identity/devices/device-join-macos-platform-single-sign-on#check-your-device-registration-status).

On Intune enrolled devices, you can also go to **Settings** > **Privacy and security** > **Profiles**. Your Platform SSO profile is shown under `com.apple.extensiblesso Profile`. Select the profile to see the settings you configured, including the URLs.

To troubleshoot Platform SSO, go to [macOS Platform single sign-on known issues and troubleshooting](/entra/identity/devices/troubleshoot-macos-platform-single-sign-on-extension).

## Step 7 - Unassign any existing SSO app extension profiles

After you confirm that your settings catalog policy is working, unassign any existing [SSO app extension](use-enterprise-sso-plug-in-macos-with-intune.md) profiles created using the Intune Device Features template.

If you keep both policies, conflicts can occur.

## Other MDMs

You can configure Platform SSO with other mobile device management services (MDMs), if that MDM supports Platform SSO. When using another MDM service, use the following guidance:

- The settings listed in this article are the Microsoft-recommended settings you should configure. You can copy/paste the setting values from this article in your MDM service policy.

  The configuration steps in your MDM service can be different. We recommend you work with your MDM service vendor to correctly configure and deploy these Platform SSO settings.

- Device registration with Platform SSO is more secure and uses hardware-bound device certificates. These changes can affect some MDM flows, like integration with [device compliance partners](../protect/device-compliance-partners.md).

  You should talk to your MDM service vendor to understand if the MDM tested Platform SSO, certified that their software works properly with Platform SSO, and is ready to support customers using Platform SSO.

## Common errors

When you configure Platform SSO, you might see the following errors:

- `10001: misconfiguration in the SSOe payload.`

  This error can occur if:

  - There's a required setting that isn't configured in the settings catalog profile.
  - There's a setting in the settings catalog profile that you configured that's not applicable for the [redirect type payload](use-enterprise-sso-plug-in-ios-ipados-macos.md#sso-app-extension).

  The authentication settings you configure in the settings catalog profile are different for macOS 13.x and 14.x devices.

  If you have macOS 13 and macOS 14 devices in your environment, then you must create one settings catalog policy, and configure their respective authentication settings in the same policy. This information is documented in [Step 2 - Create the Platform SSO policy in Intune](#step-2---create-the-platform-sso-policy-in-intune) (in this article).

- `10002: multiple SSOe payloads configured.`

  Multiple SSO extension payloads are applying to the device and are in conflict. There should only be one extension profile on the device, and that profile should be the settings catalog profile.

  If you previously created an SSO app extension profile using the Device Features template, then unassign that profile. The settings catalog profile is the only profile that should be assigned to the device.

## Related articles

- [Common Platform SSO scenarios for macOS devices](platform-sso-scenarios.md)
- [macOS Platform Single Sign-on overview (preview)](/entra/identity/devices/macos-psso)
- [Microsoft Enterprise SSO plug-in](/entra/identity-platform/apple-sso-plugin)
- [Use the Microsoft Enterprise SSO app extension on macOS devices](use-enterprise-sso-plug-in-macos-with-intune.md)
- [What is a Primary Refresh Token (PRT)?](/entra/identity/devices/concept-primary-refresh-token)
- [macOS Platform single sign-on known issues and troubleshooting](/entra/identity/devices/troubleshoot-macos-platform-single-sign-on-extension)
