---
# required metadata

title: Configure platform SSO for macOS devices
description: 
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/22/2024
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

# Configure platform SSO for macOS devices in Microsoft Intune

> [!WARNING]
> This article is still being written and is not yet complete.

On your macOS devices, you can configure platform SSO to enable single sign-on (SSO) using a Microsoft Entra ID. Platform SSO signs users into the device using their Microsoft Entra ID.

This article applies to:

- macOS

On macOS devices, users sign in with a local account. Then, they sign into apps and websites with their Microsoft Entra ID. When platform SSO is configured, users sign into the device with their Microsoft Entra ID instead of their local account. When they sign into the device with their Microsoft Entra ID, then they get access to device features that use Microsoft Entra ID for authentication.

Platform SSO also requires the [Enterprise SSO app extension](use-enterprise-sso-plug-in-macos-with-intune.md). The Enterprise SSO app extension signs users into apps and websites that use Microsoft Entra ID for authentication, including Microsoft 365 apps.

Platform SSO and Enterprise SSO work together. Platform SSO handles the initial device sign-in, and the SSO app extension handles the sign-in for apps and websites.

Some benefits of platform SSO include:

- Helps minimize the number of times users need to enter their Entra credentials.
- Helps reduce the number of passwords users need to remember.
- Similar to signing into a Windows device with a work account, similar to Windows Hello for Business.
- Get the benefits of entra ID join, which allows any organization user to sign into the device.

This article shows you how to configure platform SSO for macOS devices in Intune.

## Prerequisites

- To create the policy, at a minimum, sign in with an account that is a member of the **Policy and Profile Manager** RBAC role. For more information on RBAC roles in Intune, go to [Role-based access control (RBAC) with Microsoft Intune](../fundamentals/role-based-access-control.md).
- macOS 13.0 and newer devices
- Company Portal app version 5.2307.99.2235 ?? Where to get this version? ??

## Step 1 - Configure the Enterprise SSO app extension policy in Intune

Platform SSO requires the Enterprise SSO app extension be configured in Microsoft Intune. For the specific steps, go to [Use the Microsoft Enterprise SSO plug-in on macOS devices](use-enterprise-sso-plug-in-macos-with-intune.md). Platform SSO is only available with Microsoft Intune. So, make sure you follow the Intune steps when creating the SSO app extension policy.

?? Oustanding questions:

- To create the Enterprise SSO app extension policy, do you use the Device features template or the settings catalog? We currently document the Device Features template but it's not clear if that's still the correct way.
- For the Enterprise SSO app extension, does the app have to be developed/coded to include something? We really don't mention this in the Intune docs and it's confusing.
??

## Step 2 - Create the platform SSO policy in Intune

To configure the platform SSO policy, use the [Intune settings catalog](settings-catalog.md).

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration** > **Create**.
3. Enter the following properties:

    - **Platform**: Select **macOS**.
    - **Profile type**: Select **Settings catalog**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, name the policy **macOS - platform SSO**.
    - **Description**: Enter a description for the policy. This setting is optional, but recommended.

6. Select **Next**.
7. In **Configuration settings**, select **Add settings**. In the settings picker, expand **Authentication**, and select **Extensible Single Sign On (SSO)**:

    :::image type="content" source="./media/platform-sso-macos/settings-picker-authentication-extensible-sso.png" alt-text="Screenshot that shows the Settings Catalog settings picker, and selecting authentication and extensible SSO category in Microsoft Intune.":::

    In the list, select the following settings:

    - **Authentication Method (Deprecated)**
    - **Extension Identifier**
    - Expand **Platform SSO** > **Authentication Method**
    - **Registration Token**
    - **Screen Locked Behavior**
    - **Team Identifier**
    - **Type**
    - **URLs**

    Close the settings picker.

8. Configure the following settings:

    - **URLs**: Enter an array of URL prefixes of the identity providers that do SSO app extensions. The URLs are required for **redirect** payloads and are ignored for **credential** payloads. For example, enter the following URLs: ??Are these URLs examples or are they the actual required URLs? ??

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
      - Query parameters and URL fragments are not allowed.
      - The URLs of all installed Extensible SSO payloads must be unique.

    - **Team Identifier**: Enter the team identifier of the app extension. For example, enter `UBF8T346G9`. ??What is the team identifier? Is it the same as the bundle ID? How does someone get the value? ??
    - **Screen Locked Behavior**: Select **Do Not Handle**. When set to **Do Not Handle**, the request continues without SSO.
    - **Registration token**: Enter the token the device uses for registration with platform SSO. This token silently registers with the Identity Provider.

      For example, enter `{{DEVICEREGISTRATION}}`. Be sure to include the curly braces.

      This setting requires that `AuthenticationMethod` has a value and isn't blank. ??Which `AuthenticationMethod`? ??

    - **Platform SSO** > **Authentication Method** (macOS 14+): Select the platform SSO authentication method that the app extension uses. The SSO app extension must also support the method.

      This setting applies to macOS 14.x and later. For macOS 13.x, use the **Authentication Method (Deprecated)** setting.

      Your options:

      - **Password** (default): Enables SSO across apps that use Microsoft Entra ID for authentication. This option:

        - Syncs the local account password with the Microsoft Entra ID password​.
        - Leaves the local account username as-is. The username isn't changed.
        - Requires fewer passwords for users and admins to remember and manage.​
        - Requires users to enter their password after a device reboots. ??Which password - the Apple password or the Entra password?? After this initial machine unlock​, Touch ID can be used to unlock local machine.
        - After unlock, the device gets the hardware-bound Primary Refresh Token (PRT) credential for Entra ID SSO.​

        This option doesn't completely remove the local account machine password. This behavior is by design due to Apple's FileVault disk encryption, which uses the local password as the unlock key.

      - **UserSecureEnclaveKey**: Enables SSO across apps that use Microsoft Entra ID for authentication by provisioning a [Secure Enclave](https://developer.apple.com/documentation/security/certificate_key_and_trust_services/keys/protecting_keys_with_the_secure_enclave) cryptographic key. This option:

        - Is considered a password-less and phish-resistant option. It's conceptually similar to Windows Hello for Business. It can use the same features as Windows Hello for Business, like Conditional Access.
        - Leaves the local account username and password as-is. These values aren't changed.​
        - After a device reboots, users must enter the password (??Which password? The Entra ID password? Or, the local account password? ??). After this initial machine unlock​, Touch ID can be used to unlock local machine.
        - After unlock, device gets the hardware-backed Primary Refresh Token (PRT) for device-wide SSO.​
        - In web browsers, this key can be used as a passkey using [WebAuthN APIs](https://webauthn.guide).
        - It's setup can be bootstrapped with an authentication app for multifactor authentication or Microsoft [Temporary Access Pass (TAP)](/entra/identity/authentication/howto-authentication-temporary-access-pass).

        This option doesn't completely remove the local account machine password. This behavior is by design due to Apple's FileVault disk encryption, which uses the local password as the unlock key.

      - **SmartCard**: Enables SSO across apps that use Microsoft Entra ID for authentication. It uses a smart card or smart card-compatible hard token, like a YubiKey. This token acts as a local machine password.​ This option:

        - Is considered a password-less option.
        - Leaves the local account username and password as-is. These values aren't changed.​

    - **Extension Data**: ??This setting was automatically added to the policy. What is it? Is it required? ??

    - **Authentication Method (Deprecated)** (macOS 13 only): Select the platform SSO authentication method that the app extension uses. The SSO app extension must also support the method.

      This setting applies to macOS 13.x only. For macOS 14.0 and later, use the **Platform SSO** > **Authentication Method** setting.

      Your options:

      - **Password** (default): Enables SSO across apps that use Microsoft Entra ID for authentication and:

        - Syncs the local account password with the Microsoft Entra ID password​.
        - Leaves the local account username as-is. The username isn't changed.
        - Requires fewer passwords for users and admins to remember and manage.​
        - Requires users to enter their password after a device reboots. ??Which password - the Apple password or the Entra password?? After this initial machine unlock​, Touch ID can be used to unlock local machine.
        - After unlock, the device gets the hardware-bound Primary Refresh Token (PRT) credential for Entra ID SSO.​

        This option doesn't completely remove the local account machine password. This behavior is by design due to Apple's FileVault disk encryption, which uses the local password as the unlock key.

      - **UserSecureEnclaveKey**: Enables SSO across apps that use Microsoft Entra ID for authentication by provisioning a [Secure Enclave](https://developer.apple.com/documentation/security/certificate_key_and_trust_services/keys/protecting_keys_with_the_secure_enclave) cryptographic key. And:

        - Is considered a password-less and phish-resistant option. It's conceptually similar to Windows Hello for Business, as it can use the same features as Windows Hello for Business, like Conditional Access.
        - Leaves the local account username and password as-is. These values aren't changed.​
        - After a device reboots, users must enter the password (??Which password? The Entra ID password? Or, the local account password? ??). After this initial machine unlock​, Touch ID can be used to unlock local machine.
        - After unlock, the device gets the hardware-backed Primary Refresh Token (PRT) for device-wide SSO.​
        - In web browsers, this key can be used as a passkey using [WebAuthN APIs](https://webauthn.guide).
        - It's setup can be bootstrapped with an authentication app for multifactor authentication or Microsoft [Temporary Access Pass (TAP)](/entra/identity/authentication/howto-authentication-temporary-access-pass).

        This option doesn't completely remove the local account machine password. This behavior is by design due to Apple's FileVault disk encryption, which uses the local password as the unlock key.

    - **Extension Identifier**: Enter the bundle ID of the app extension that performs SSO for the URLs you entered. For example, enter `com.microsoft.CompanyPortalMac.ssoextension`.

      ??How will admins know what this value is? ??

    - **Type**: Select **Redirect**.

9. Select **Next**.
10. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, see [Use RBAC roles and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

11. In **Assignments**, select the users or groups that will receive your profile. For more information on assigning profiles, see [Assign user and device profiles](device-profile-assign.md).

    Select **Next**.

12. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

The next time the device checks for configuration updates, the settings you configured are applied.

## Step 3 - Deploy the mac Company Portal app

Using Intune, you add the correct version of the Company Portal app, make it a required app, and then deploy the app to your macOS devices:

1. Add the macOS Company Portal app to Intune and make it a required app. For the steps, go to [Add macOS apps to Microsoft Intune](../apps/apps-add-macos.md).
2. Configure the Company Portal app to include your organization information. For the steps, go to [How to configure the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).

    There aren't any specific steps to configure the app for platform SSO. Just make sure the correct version of the Company Portal app is added to Intune and deployed to your macOS devices.

## Step 4 - Enroll the devices and apply the policies

To use platform SSO, the devices must be MDM enrolled in Intune using one of the following methods:

- For **organization-owned devices, create an [Automated device enrollment](../enrollment/device-enrollment-program-enroll-macos.md) policy** using Apple Business Manager or Apple School Manager. Assign this enrollment profile to your macOS devices.
- For **personally-owned devices, create a [Device enrollment](../fundamentals/deployment-guide-enrollment-macos.md#byod-device-enrollment) policy**. With this enrollment method, end users openthe Company Portal app and sign in with their Microsoft Entra ID. When they successfully sign-in, the enrollment policy applies.

If these are **new devices**, then we recommend you pre-create and configure all the necessary policies, including the enrollment policy. Then, when the devices enroll in Intune, the policies automatically apply.

If these are **existing devices** that are already enrolled, then you can assign the policies to the devices. The next time the devices sync or check-in with the Intune services, they receive the platform SSO policy settings you create.

## Step 5 - Test platform SSO

When the enrollment completes and the policies are applied, you can confirm the platform SSO is configured:

1. On the enrolled device, go to **Settings** > **Privacy and security** > **Profiles**.
2. You should see your platform SSO profile listed. Select the profile to see the settings you configured, including the URLs.

    ?? insert screenshot from https://microsoft-my.sharepoint-df.com/personal/arnab_microsoft_com/_layouts/15/onedrive.aspx?id=%2Fpersonal%2Farnab%5Fmicrosoft%5Fcom%2FDocuments%2FApple%2FMac%2FPlatform%20SSO%2F%5BEXT%5D%20MSFT%2DMacOS%2DPSSOe%2DPrivatePreview%2DReadMe%201%2Epdf&parent=%2Fpersonal%2Farnab%5Fmicrosoft%5Fcom%2FDocuments%2FApple%2FMac%2FPlatform%20SSO&ga=1&gaS=9 ??

## Next steps

[What is a Primary Refresh Token (PRT)?](/entra/identity/devices/concept-primary-refresh-token)
