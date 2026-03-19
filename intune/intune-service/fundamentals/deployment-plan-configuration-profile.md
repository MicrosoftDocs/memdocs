---
title: Configure security, email, VPN, and Wi-Fi device configuration profiles
description: Step 4 to deploy device configuration profiles as part of the minimum set of policies for your devices using Microsoft Intune. The starting point is to enable the firewall, install AV, scan for malware, install software updates, create a strong PIN policy, and create email, VPN, and Wi-Fi device configuration profiles.
author: MandiOhlinger
ms.author: mandia
ms.date: 03/18/2026
ms.topic: how-to
ms.collection:
- M365-identity-device-management
- highpri
---

# Step 4 - Configure device features and settings to secure devices and access resources

So far, you set up your Intune subscription, created app protection policies, and created device compliance policies.

In this step, you're ready to configure a minimum or baseline set of security and device features that all devices must have.

:::image type="content" source="./media/deployment-plan-configuration-profile/deployment-plan-config-devices.png" alt-text="Diagram that shows getting started with Microsoft Intune with step 4, which is configuring devices features and security settings.":::

This article applies to:

- Android
- iOS/iPadOS
- macOS
- Windows

When you create device configuration profiles, you can choose from different levels and types of policies. These levels are the minimum Microsoft recommended policies. Know that your environment and business needs can be different.

- **Level 1 - Minimum device configuration**: In this level, Microsoft recommends you create policies that:

  - Focus on device security, including installing antivirus, creating a strong password policy, and regularly installing software updates.
  - Give users access to their organization email and controlled secure access to your network, wherever they are.

- **Level 2 - Enhanced device configuration**: In this level, Microsoft recommends you create policies that:

  - Expand device security, including configuring disk encryption, enabling secure boot, and adding more password rules.
  - Use the built-in features and templates to configure more settings that are important for your organization, including analyzing on-premises Group Policy Objects (GPOs).

- **Level 3 - High device configuration**: In this level, Microsoft recommends you create policies that:

  - Move to password-less authentication, including using certificates, configuring single sign-on (SSO) to apps, enabling multifactor authentication (MFA), and configuring Microsoft Tunnel.
  - Add extra layers of security by using Android common criteria mode or creating DFCI policies for Windows devices.
  - Use the built-in features to configure kiosk devices, dedicated devices, shared devices, and other specialized devices.
  - Deploy existing shell scripts.

This article lists the different levels of device configuration policies that organizations should use. Most of these policies focus on access to organization resources and security.

Configure these features in device configuration profiles in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). When the Intune profiles are ready, assign them to your users and devices.

> [!TIP]
> [Take a tour of Intune and the Microsoft Intune admin center](tutorial-walkthrough-endpoint-manager.md).

## Level 1 - Create your security baseline

To help keep your organization's data and devices secure, create different policies that focus on security. Create a list of security features that all users and devices must have. This list is your security baseline.

In your baseline, at a minimum, include the following security policies:

- Install antivirus (AV) software and regularly scan for malware.
- Use detection and response.
- Turn on the firewall.
- Install software updates regularly.
- Create a strong PIN or password policy.

This section lists the Intune and Microsoft services you can use to create these security policies.

For a more granular list of Windows settings and their recommended values, see [Windows security baselines](../protect/security-baselines.md).

### Antivirus and scanning

:::image type="icon" source="../../media/icons/16/check.svg" border="false"::: **Install antivirus software and regularly scan for malware**

Install antivirus software on all devices and regularly scan for malware. Intune integrates with third-party partner mobile threat defense (MTD) services that provide AV and threat scanning. Antivirus and scanning are built in to Intune by using Microsoft Defender for Endpoint.

Your policy options:

| Platform | Policy type |
| --- | --- |
| Android Enterprise | - [Mobile threat defense partner](../protect/mobile-threat-defense.md) </br>- [Microsoft Defender for Endpoint](/defender-endpoint/mtd) |
| iOS/iPadOS | - [Mobile threat defense partner](../protect/mobile-threat-defense.md) </br>- [Microsoft Defender for Endpoint](/defender-endpoint/mtd) |
| macOS | - [Intune Endpoint Security antivirus profile](../protect/endpoint-security-antivirus-policy.md) (Microsoft Defender for Endpoint) |
| Windows client | - [Intune security baselines](../protect/security-baselines.md) (recommended)</br>- [Intune Endpoint Security antivirus profile](../protect/endpoint-security-antivirus-policy.md) (Microsoft Defender for Endpoint) |

### Detection and response

:::image type="icon" source="../../media/icons/16/check.svg" border="false"::: **Detect attacks and act on these threats**

When you detect threats quickly, you can help minimize the impact of the threat. When you combine these policies with Conditional Access, you can block users and devices from accessing organization resources if a threat is detected.

Your policy options:

| Platform | Policy type |
| --- | --- |
| Android Enterprise | - [Mobile threat defense partner](../protect/mobile-threat-defense.md)</br>- [Microsoft Defender for Endpoint](/defender-endpoint/mtd) |
| iOS/iPadOS | - [Mobile threat defense partner](../protect/mobile-threat-defense.md)</br>- [Microsoft Defender for Endpoint](/defender-endpoint/mtd) |
| macOS | [Intune endpoint detection and response profile](../protect/endpoint-security-edr-policy.md) (Microsoft Defender for Endpoint) |
| Windows client | - [Intune security baselines](../protect/security-baselines.md) (recommended)</br>- [Intune endpoint detection and response profile](../protect/endpoint-security-edr-policy.md) (Microsoft Defender for Endpoint) |

### Firewall

:::image type="icon" source="../../media/icons/16/check.svg" border="false"::: **Enable the firewall on all devices**

Some platforms come with a built-in firewall. On other platforms, you might need to install a firewall separately. Intune integrates with third-party partner mobile threat defense (MTD) services that can manage a firewall for Android and iOS/iPadOS devices. For macOS and Windows, Intune includes built-in firewall security through Microsoft Defender for Endpoint.

Your policy options:

| Platform | Policy type |
| --- | --- |
| Android Enterprise | [Mobile threat defense partner](../protect/mobile-threat-defense.md) |
| iOS/iPadOS | [Mobile threat defense partner](../protect/mobile-threat-defense.md) |
| macOS | [Intune Endpoint Security firewall profile](../protect/endpoint-security-firewall-policy.md) (Microsoft Defender for Endpoint) |
| Windows client | - [Intune security baselines](../protect/security-baselines.md) (recommended)</br>- [Intune Endpoint Security firewall profile](../protect/endpoint-security-firewall-policy.md) (Microsoft Defender for Endpoint) |

### Password policy

:::image type="icon" source="../../media/icons/16/check.svg" border="false"::: **Create a strong password or PIN policy and block simple passcodes**

PINs unlock devices. On devices that access organization data, including personally owned devices, require strong PINs or passcodes and support biometrics to unlock devices. Using biometrics is part of a password-less approach, which is recommended.

Use the settings catalog and device restrictions template profiles in Intune to create and configure password requirements.

Your policy options:

| Platform | Policy type |
| --- | --- |
| Android Enterprise | [Intune settings catalog](../configuration/settings-catalog-android.md) for Corporate owned, Fully Managed, and Dedicated devices to manage the: <br/>- **Device password**<br/>- **Work profile password**<br/><br/>[Intune device restrictions template](../configuration/device-restrictions-android-for-work.md) for Corporate owned and Personally owned devices to manage the: <br/>- **Device password**<br/>- **Work profile password** <br/>- **Password**|
| Android Open-Source Project (AOSP) | - [Intune settings catalog](../configuration/settings-catalog-android.md) > **Device password** <br/>- [Intune device restrictions template](../configuration/device-restrictions-android-for-work.md) > **Device password** |
| iOS/iPadOS | - [Intune settings catalog](../configuration/apple-settings-catalog-configurations.md) > Declarative Device Management (DDM) > **Passcode** (recommended) <br/> - [Intune settings catalog](../configuration/apple-settings-catalog-configurations.md) > Security > **Passcode** <br/>- [Intune device restrictions template](../configuration/device-restrictions-apple.md) > **Password** |
| macOS | - [Intune settings catalog](../configuration/apple-settings-catalog-configurations.md) > Declarative Device Management (DDM) > **Passcode** (recommended) <br/> - [Intune settings catalog](../configuration/apple-settings-catalog-configurations.md) > Security > **Passcode** <br/>- [Intune device restrictions template](../configuration/device-restrictions-apple.md) > **Password** |
| Windows client | - [Intune security baselines](../protect/security-baselines.md) (recommended) </br>- [Intune device restrictions template](../configuration/device-restrictions-windows-10.md) > **Password** </br>- [Manage Windows Hello for Business when devices enroll](../protect/windows-hello.md) </br>- [Manage Windows Hello for Business after devices enroll](../protect/identity-protection-configure.md) |

### Software updates

:::image type="icon" source="../../media/icons/16/check.svg" border="false"::: **Regularly install software updates**

Update all devices regularly, and create policies to make sure these updates are successfully installed. For most platforms, Intune has policy settings that focus on managing and installing updates.

Your policy options:

| Platform | Policy type |
| --- | --- |
| Android Enterprise organization owned devices | [Intune device restrictions template](../configuration/device-restrictions-android-for-work.md) > Corporate owned > General > System update |
| Android Enterprise personally owned devices | Not available <br/><br/>Can use [compliance policies](../protect/compliance-policy-create-android-for-work.md#personally-owned-work-profile) to set a minimum patch level, min/max OS version, and more. |
| iOS/iPadOS | [Intune settings catalog managed software updates](../../device-updates/apple/index.md) |
| macOS | [Intune settings catalog managed software updates](../../device-updates/apple/index.md) |
| Windows client | - [Intune feature updates policy](../../device-updates/windows/feature-updates.md) </br>- [Intune quality updates policy](../../device-updates/windows/quality-updates.md) |

## Level 1 - Access organization email, connect to VPN or Wi-Fi

This section focuses on accessing resources in your organization. These resources include:

- Email for work or school accounts
- VPN connection for remote connectivity
- Wi-Fi connection for on-premises connectivity

:::image type="content" source="./media/deployment-plan-configuration-profile/deploy-email-vpn-wifi.png" alt-text="Diagram that shows an email, VPN, and Wi-Fi profiles deployed from Microsoft Intune to end user devices.":::

### Email

Many organizations deploy email profiles with preconfigured settings to user devices.

:::image type="icon" source="../../media/icons/16/check.svg" border="false"::: **Automatically connect to user email accounts**

The profile includes the email configuration settings that connect to your email server.

Depending on the settings you configure, the email profile can also automatically connect the users to their individual email account settings.

:::image type="icon" source="../../media/icons/16/check.svg" border="false"::: **Use enterprise level email apps**

Email profiles in Intune use common and popular email apps, like Outlook. The email app is deployed to user devices. After the app is deployed, you deploy the email device configuration profile with the settings that configure the email app.

The email device configuration profile includes settings that connect to your Exchange.

:::image type="icon" source="../../media/icons/16/check.svg" border="false"::: **Access work or school email**

Creating an email profile is a common minimum baseline policy for organizations with users that use email on their devices.

Intune has built-in email settings for Android, iOS/iPadOS, and Windows client devices. When users open their email app, they can automatically connect, authenticate, and synchronize their organizational email accounts on their devices.

:::image type="icon" source="../../media/icons/16/check.svg" border="false"::: **Deploy anytime**

On new devices, deploy the email app during the enrollment process. When enrollment completes, deploy the email device configuration policy.

If you have existing devices, deploy the email app at any time. Then, deploy the email device configuration policy.

#### Get started with email profiles

To get started:

1. Deploy an email app to your devices. For some guidance, see [Add email settings to devices using Intune](../configuration/email-settings-configure.md).

2. [Create an email device configuration profile in Intune](../configuration/email-settings-configure.md). Depending on the email app your organization uses, you might not need the email device configuration profile.

    For some guidance, see [Add email settings to devices using Intune](../configuration/email-settings-configure.md).

3. In the email device configuration profile, configure the settings for your platform:

    - [Android Enterprise personally owned devices with a work profile email settings](../configuration/email-settings-android-enterprise.md)

      Android Enterprise organization-owned devices don't use email device configuration profiles.

    - [iOS/iPadOS email settings](../configuration/email-settings-ios.md)
    - [Windows email settings](../configuration/email-settings-windows-10.md)

4. [Assign the email device configuration profile](../configuration/device-profile-assign.md) to your users or user groups.

### VPN

Many organizations deploy VPN profiles with preconfigured settings to user devices. The VPN connects your devices to your internal organization network.

If your organization uses cloud services with modern authentication and secure identities, then you probably don't need a VPN profile. Cloud-native services don't require a VPN connection.

If your apps or services aren't cloud-based or aren't cloud-native, deploy a VPN profile to connect to your internal organization network.

:::image type="icon" source="../../media/icons/16/check.svg" border="false"::: **Work from anywhere**

Creating a VPN profile is a common minimum baseline policy for organizations with remote workers and hybrid workers.

As users work from anywhere, they can use the VPN profile to securely connect to your organization's network to access resources.

Intune has built-in VPN settings for Android, iOS/iPadOS, macOS, and Windows client devices. On user devices, your VPN connection appears as an available connection. Users select it. And, depending on the settings in your VPN profile, users can automatically authenticate and connect to the VPN on their devices.

:::image type="icon" source="../../media/icons/16/check.svg" border="false"::: **Use enterprise level VPN apps**

VPN profiles in Intune use common enterprise VPN apps, like Check Point, Cisco, Microsoft Tunnel, and more. The VPN app is deployed to user devices. After the app is deployed, then you deploy the VPN connection profile with settings that configure the VPN app.

The VPN device configuration profile includes settings that connect to your VPN server.

:::image type="icon" source="../../media/icons/16/check.svg" border="false"::: **Deploy anytime**

On new devices, deploy the VPN app during the enrollment process. When enrollment completes, deploy the VPN device configuration policy.

If you have existing devices, deploy the VPN app at any time, and then deploy the VPN device configuration policy.

#### Get started with VPN profiles

To get started:

1. Deploy a VPN app to your devices.

    - For a list of supported VPN apps, see [Supported VPN connection apps in Intune](../configuration/vpn-settings-configure.md#vpn-connection-types).
    - For the steps to add apps to Intune, see [Add apps to Microsoft Intune](../apps/apps-add.md).

2. [Create a VPN configuration profile in Intune](../configuration/vpn-settings-configure.md).
3. In the VPN device configuration profile, configure the settings for your platform:

    - [Android Enterprise VPN settings](../configuration/vpn-settings-android-enterprise.md)
    - [iOS/iPadOS VPN settings](../configuration/vpn-settings-apple.md)
    - [macOS VPN settings](../configuration/vpn-settings-apple.md)
    - [Windows VPN settings](../configuration/vpn-settings-windows-10.md)

4. [Assign the VPN device configuration profile](../configuration/device-profile-assign.md) to your users or user groups.

### Wi-Fi

Many organizations deploy Wi-Fi profiles with preconfigured settings to user devices. If your organization has a remote-only workforce, then you don't need to deploy Wi-Fi connection profiles. Wi-Fi profiles are optional and are used for on-premises connectivity.

:::image type="icon" source="../../media/icons/16/check.svg" border="false"::: **Connect wirelessly**

As users work from different mobile devices, they can use the Wi-Fi profile to wirelessly and securely connect to your organization's network.

The profile includes the Wi-Fi configuration settings that automatically connect to your network and/or SSID (service set identifier). Users don't have to manually configure their Wi-Fi settings.

:::image type="icon" source="../../media/icons/16/check.svg" border="false"::: **Support mobile devices on-premises**

Creating a Wi-Fi profile is a common minimum baseline policy for organizations with mobile devices that work on-premises.

Intune has built-in Wi-Fi settings for Android, iOS/iPadOS, macOS, and Windows client devices. On user devices, your Wi-Fi connection appears as an available connection. Users select it. And, depending on the settings in your Wi-Fi profile, users can automatically authenticate and connect to the Wi-Fi on their devices.

:::image type="icon" source="../../media/icons/16/check.svg" border="false"::: **Deploy anytime**

On new devices, deploy the Wi-Fi device configuration policy when devices enroll in Intune.

If you have existing devices, you can deploy the Wi-Fi device configuration policy at any time.

#### Get started with Wi-Fi profiles

To get started:

1. [Create a Wi-Fi device configuration profile in Intune](../configuration/wi-fi-settings-configure.md).
2. Configure the settings for your platform:

    - [Android Enterprise Wi-Fi settings](../configuration/wi-fi-settings-android-enterprise.md)
    - [iOS/iPadOS Wi-Fi settings](../configuration/wi-fi-settings-apple.md)
    - [macOS Wi-Fi settings](../configuration/wi-fi-settings-apple.md)
    - [Windows Wi-Fi settings](../configuration/vpn-settings-windows-10.md)

3. [Assign the Wi-Fi device configuration profile](../configuration/device-profile-assign.md) to your users or user groups.

## Level 2 - Enhanced protection and configuration

This level expands on what you configured in level 1 and adds more security for your devices. In this section, you create a level 2 set of policies that configure more security settings for your devices.

Microsoft recommends the following level 2 security policies:

- Enable **disk encryption, secure boot, and TPM** on your devices. Use these features with a strong PIN policy or biometric unlocking.

  # [Android](#tab/android-disk)

  On Android devices, the operating system might include disk encryption and Samsung Knox. You might automatically enable disk encryption when you configure the lock screen settings, which are enabled and allowed by default.

  In Intune, you can:

  - Create a settings catalog policy that disables the lock screen (not recommended). When you disable the lock screen, the device isn't encrypted.
  - Create a device restrictions template profile that disables individual features when the lock screen is on.

  For a list of the password and lock screen settings you can configure, see:

  - [Android settings catalog settings](../configuration/settings-catalog-android.md) for Fully Managed and Dedicated devices > **Device password** and **Work profile password** settings
  - [Android device restrictions template settings](../configuration/device-restrictions-android-for-work.md) for Corporate-owned and Personally owned devices > **Device password** and **Work profile password** settings

  # [iOS/iPadOS](#tab/ios-disk)

  On iOS/iPadOS devices, the operating system includes disk encryption and Secure Enclave, and automatically enables them. There aren't any Intune settings to configure these specific features.

  For more specific information, see [Introduction to Apple platform security](https://support.apple.com/guide/security/intro-to-apple-platform-security-seccd5016d31/web) and [Secure Enclave](https://support.apple.com/guide/security/secure-enclave-sec59b0b31ff/web) (opens Apple's web site).

  The settings catalog and the [device restrictions template](../configuration/device-restrictions-apple.md) include Intune policy settings that focus on password settings and encrypting backups, like the **Force Encrypted Backup** setting.

  # [macOS](#tab/macos-disk)

  On macOS devices, use a settings catalog policy (recommended) or an endpoint security policy (deprecated) to [configure and use FileVault](../protect/encrypt-devices-filevault.md) for disk encryption.

  Secure Enclave is built into the operating system and automatically enabled. For more specific information, see [Introduction to Apple platform security](https://support.apple.com/guide/security/intro-to-apple-platform-security-seccd5016d31/web) and [Secure Enclave](https://support.apple.com/guide/security/secure-enclave-sec59b0b31ff/web) (opens Apple's web site).

  # [Windows](#tab/windows-disk)

  On Windows devices, use Intune endpoint protection policies that [manage BitLocker, including TPM](../protect/encrypt-devices.md) and [manage Windows settings, including secure boot](../protect/endpoint-protection-windows-10.md#windows-encryption).

---

- **Expire passwords and regulate reusing old passwords**. In Level 1, you created a strong PIN or password policy. If you didn't already, be sure you configure your PINs and passwords to expire and set some password-reuse rules.

  Use Intune to create a [settings catalog](../configuration/settings-catalog.md) policy or a [device restrictions template](../configuration/device-restrictions-configure.md) that configures these settings. For more information on the password settings you can configure, see the following articles:

  # [Android](#tab/android-password)

  On Android devices, use a settings catalog policy or a device restrictions template profile to set password rules. For a list of the password and lock screen settings you can configure, see:

  - [Android settings catalog settings](../configuration/settings-catalog-android.md) for Fully Managed and Dedicated devices > Review the **Device password** and **Work profile password** settings.
  - [Android device restrictions template settings](../configuration/device-restrictions-android-for-work.md) for Corporate-owned and Personally owned devices > Review the **Device password** and **Work profile password** settings.

  # [iOS/iPadOS](#tab/ios-password)

  On iOS/iPadOS devices, use device restrictions policies and/or the settings catalog to set password rules:

  - [Settings catalog](../configuration/settings-catalog.md) > Search for `Passcode`
  - [Device restrictions template > Password settings](../configuration/device-restrictions-apple.md)

  # [macOS](#tab/macos-password)

    On macOS devices, use device restrictions policies and/or the settings catalog to set password rules:

  - [Settings catalog](../configuration/settings-catalog.md) > Search for `Passcode`
  - [Device restrictions template > Password settings](../configuration/device-restrictions-apple.md)

  # [Windows](#tab/windows-password)

    On Windows devices, use device restrictions policies and/or the settings catalog to set password rules:

  - [Settings catalog](../configuration/settings-catalog.md) > Search for `Device lock`
  - [Device restrictions template > Password settings](../configuration/device-restrictions-windows-10.md#password)

---

- Intune includes **hundreds of settings that can manage device features** and settings, like disabling the built-in camera, controlling notifications, allowing Bluetooth, blocking games, and more.

  Use the [settings catalog](../configuration/settings-catalog.md) or the [built-in templates](../configuration/device-profiles.md) to see and configure the settings.

  - **[Use the settings catalog](../configuration/settings-catalog.md)** to see and configure all the available settings. You can use the settings catalog on the following platforms:

    - Android
    - iOS/iPadOS
    - macOS
    - Windows

  - **[Device restrictions templates](../configuration/device-restrictions-configure.md)** are logical groups of built-in settings that you can use to control different parts of the devices, including security, hardware, data sharing, and more.

    Use these templates on the following platforms:

    - Android
    - iOS/iPadOS
    - macOS
    - Windows

- If you use **on-premises GPOs** and want to know if these same settings are available in Intune, then use [Group Policy analytics](../configuration/group-policy-analytics.md). This feature analyzes your GPOs and depending on the analysis, can import them into an Intune settings catalog policy.

  For more information, see [Analyze your on-premises GPOs and import them in Intune](../configuration/group-policy-analytics.md).

## Level 3 - High protection and configuration

This level expands on what you configured in levels 1 and 2. It adds extra security features used in enterprise-level organizations.

- **Expand password-less authentication** to other services used by your workforce. In level 1, you enabled biometrics so users can sign in to their devices with a fingerprint or facial recognition. In this level, expand password-less to other parts of the organization.

  - **Use certificates to authenticate** email, VPN, and Wi-Fi connections. Deploy certificates to users and devices, and then use them to access resources in your organization through the email, VPN, and Wi-Fi connections.

    To learn more about using certificates in Intune, see:

    - [Use PKCS or SCEP certificates for authentication](../protect/certificates-configure.md)
    - [Use derived credentials](../protect/derived-credentials.md)

  - **Configure single sign-on** (SSO) for a more seamless experience when users open business apps, like Microsoft 365 apps. Users sign in once and then are automatically signed in to all the apps that support your SSO configuration.

    To learn about using SSO in Intune and Microsoft Entra ID, see:

    # [Android](#tab/android-sso)

    Uses the Microsoft Authentication Library (MSAL), which is a feature of Microsoft Entra ID. It helps you enable SSO across your applications and acts as a broker, so you can extend SSO across the entire device.

    - [Enable cross-app SSO on Android using MSAL in Microsoft Entra ID](/entra/msal/android/single-sign-on)

    # [iOS/iPadOS](#tab/ios-sso)

    Uses the Microsoft Enterprise SSO plug-in, which is a feature in Microsoft Entra ID. It provides single sign-on (SSO) features for Apple devices and uses the Apple single sign-on app extension framework.

    - [Use the Enterprise SSO plug-in in Intune and other MDMs](../configuration/use-enterprise-sso-plug-in-ios-ipados-with-intune.md)

    # [macOS](#tab/macos-sso)

    Uses the Microsoft Enterprise SSO plug-in, which is a feature in Microsoft Entra ID. It provides single sign-on (SSO) features for macOS devices by using the built-in SSO app extension and Platform SSO features that optimize your SSO configuration.

    - [Configure Platform SSO in an Intune settings catalog policy](../configuration/platform-sso-macos.md)

    # [Windows](#tab/windows-sso)

    Microsoft Entra ID Single sign-on is an authentication method that allows users to sign in using one set of credentials to multiple independent software systems. Many apps already exist in Microsoft Entra ID that you can use with SSO.

    - [Configure SSO with Microsoft Entra ID](/entra/identity/enterprise-apps/what-is-single-sign-on)

    ---

  - **Use multifactor authentication** (MFA). When you move to password-less, MFA adds an extra layer of security, and it can help protect your organization from phishing attacks. Use MFA with authenticator apps, like Microsoft Authenticator, or with a phone call or text message. You can also use MFA when users enroll their devices in Intune.

    Multifactor authentication is a feature of Microsoft Entra ID and you can use it with Microsoft Entra accounts. For more information, see:

    - [Microsoft Entra ID Protection overview](/azure/active-directory/identity-protection/overview-identity-protection)
    - [Microsoft Entra multifactor authentication](/azure/active-directory/authentication/concept-mfa-howitworks)
    - [Require multifactor authentication for Intune device enrollments](../enrollment/multi-factor-authentication.md)

  - **Set up Microsoft Tunnel** for your enrolled Android and iOS/iPadOS devices. Microsoft Tunnel uses Linux to allow these devices access to on-premises resources by using modern authentication and Conditional Access.

    Microsoft Tunnel uses Intune, Microsoft Entra ID, and Active Directory Federation Services (AD FS). For more information, see [Microsoft Tunnel for Microsoft Intune](../protect/microsoft-tunnel-overview.md).

  - **Use Microsoft Tunnel for Mobile Application Management** (Tunnel for MAM) to extend tunnel capabilities to Android and iOS/iPad devices that are *not enrolled* with Intune. [Tunnel for MAM](../protect/microsoft-tunnel-mam.md) is available as an Intune add-on that requires an extra license.

    For more information, see [Use Intune Suite add-on capabilities](../fundamentals/intune-add-ons.md).

- **Use Local Administrator Password Solution (LAPS) policy** to manage and back up the local administrator account on your devices.

  # [macOS](#tab/macos-laps)

  You can configure LAPS on new and existing macOS automated device enrollment (ADE) profiles. Devices are provisioned with a local administrator account that has a strong, encrypted, and randomized admin password, which is stored and encrypted by Intune.

  For more information, see [macOS LAPS in Intune](../enrollment/macos-laps.md).

  # [Windows](#tab/windows-laps)

  On Windows devices, the built-in local admin account can't be deleted and has full permissions to the device. A LAPS policy helps you manage and secure this account, which is an important step in securing your organization's devices.

  For more information, see [Windows LAPS in Intune](../protect/windows-laps-overview.md).

  ---

- Use **Microsoft Intune Endpoint Privilege Management** (EPM) to reduce the attack surface of your Windows devices. EPM empowers you to have users that run as standard users (without administrator rights) yet remain productive by determining when those users can run apps in an elevated context.

  EPM elevation rules can be based on file hashes, certificate rules, and more. The rules you configure help to ensure that only the expected and trusted applications you allow can run as elevated. Rules can:

  - Manage the child processes that an app creates.
  - Support requests by users to elevate a managed process.
  - Allow for automatic elevations of files that just need to run without any user interruption.

  [Endpoint Privilege Management](../protect/epm-overview.md) is available as an Intune add-on that requires an extra license. For more information, see [Use Intune Suite add-on capabilities](../fundamentals/intune-add-ons.md).

- **Use Android Common Criteria mode** on Android devices that are used by highly sensitive organizations, like government establishments.

  For more information on this feature, search for Common Criteria mode at:

  - [Android settings catalog settings](../configuration/settings-catalog-android.md)
  - [Android device restrictions template settings](../configuration/device-restrictions-android-for-work.md)

- Create policies that **apply to the firmware layer**:

  # [Android](#tab/android-firmware)

  These policies help you manage firmware updates, which can include software and security patches, feature updates, and other changes to the device's firmware.

  - [Firmware Over-the-Air (FOTA) updates](../../device-updates/android/fota-updates.md)
  - [Zebra LifeGuard Over-the-Air updates](../../device-updates/android/zebra-lifeguard-ota-integration.md)

  # [Windows](#tab/windows-firmware)

  These policies can help prevent malware from communicating with the OS processes. You can control security features, the built-in hardware, and the boot options in the UEFI layer.

  - [Use Device Firmware Configuration Interface (DFCI) profiles on Windows devices](../configuration/device-firmware-configuration-interface-windows.md)

  ---

- **Configure kiosks, shared devices, and other specialized devices**:

  # [Android](#tab/android-kiosk)

  - **Android Enterprise**:
    - [Use and manage Android Enterprise devices with OEMConfig](../configuration/android-oem-configuration-overview.md)
    - [Android device restrictions template settings](../configuration/device-restrictions-android-for-work.md) > Device experience

  - **Android device administrator**
    - [Use and manage Zebra devices with Zebra Mobility Extensions](../configuration/android-zebra-mx-overview.md)
    - [Device settings to run as a kiosk](../configuration/device-restrictions-android.md#kiosk)

      [!INCLUDE [android_device_administrator_support](../includes/android-device-administrator-support.md)]

  # [iOS/iPadOS](#tab/ios-kiosk)

  **Autonomous single app mode** (ASAM) locks the device into running one specific app only. The app must support ASAM and only the app can exit out of ASAM. It's designed for dedicated devices where users can't exit the app. Commonly used for exams, check‑in stations, and healthcare or industrial terminals.

  - [Settings catalog](../configuration/settings-catalog.md) > Restrictions > Autonomous single app mode (ASAM)
  - [Device restrictions template](../configuration/device-restrictions-apple.md) > Autonomous single app mode (ASAM)

  **App Lock** locks the device into running one app. You can choose any app, and admins can exit out of App Lock mode. Commonly used for kiosks and signage.

  - [Settings catalog](../configuration/settings-catalog.md) > App management > App Lock
  - [Device restrictions template](../configuration/device-restrictions-apple.md) > Kiosk

  **Shared iPads** are designed for use by multiple people, most commonly in education environments like classrooms or labs. Each user signs in to the same physical iPad and gets their own data and settings.

  - [Configure settings for Shared iPads](../enrollment/device-enrollment-shared-ipad.md#configure-settings-for-shared-ipads)

  # [macOS](#tab/macos-kiosk)

  **Autonomous single app mode** (ASAM) locks the device into running one specific app only. The app must support ASAM and only the app can exit out of ASAM. It's designed for dedicated devices where users can't exit the app. Commonly used for exams, check‑in stations, and healthcare or industrial terminals.

  - [Settings catalog](../configuration/settings-catalog.md) > App management > Autonomous single app mode

  # [Windows](#tab/windows-kiosk)

  - **Windows**
    - [Device settings to run as a dedicated kiosk](../configuration/kiosk-settings.md)
    - [Device settings to run as a kiosk](../configuration/kiosk-settings-windows.md)
    - [Shared PC or multi-user devices](../configuration/shared-user-device-settings.md)

  - **Windows Holographic for Business**
    - [Device settings to run as a kiosk](../configuration/kiosk-settings-holographic.md)
    - [Device settings to run as a dedicated kiosk](../configuration/kiosk-settings.md)

  ---

- **Deploy shell scripts**:

  # [macOS](#tab/macos-shell)

  Use shell scripts to manage settings and features that aren't available in Intune natively. You can add a script, set the script frequency, and more.

  - [Use shell scripts](../apps/macos-shell-scripts.md)

  # [Windows](#tab/windows-shell)

  Use Windows PowerShell scripts when you need customization, automation, or one‑time remediation on Windows devices.

  - [Use Windows PowerShell scripts](../apps/powershell-scripts.md)

  ---

## Follow the minimum recommended baseline policies

This article is part of a five-step series that describes how to deploy Microsoft Intune. The series includes the following articles, in order:

1. [Set up Microsoft Intune](deployment-plan-setup.md)
2. [Add, configure, and protect apps](deployment-plan-protect-apps.md)
3. [Plan for compliance policies](deployment-plan-compliance-policies.md)
4. 🡺 **Configure device features** (this article)
5. [Enroll devices](deployment-guide-enroll.md)
