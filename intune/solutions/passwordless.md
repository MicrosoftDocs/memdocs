---
title: Passwordless authentication with Microsoft Intune
description: Learn how Microsoft Intune supports passwordless authentication across devices. Explore key methods and plan your deployment.
ms.date: 04/13/2026
ms.topic: concept-article
author: paolomatarazzo
ms.author: paoloma
ms.reviewer:
ms.custom:
  - ai-assisted
  - msecd-doc-authoring-scenarios
ms.collection:
  - M365-identity-device-management
  - Microsoft Intune-scenario
#customer intent: As an IT admin, I want to understand how Microsoft Intune supports passwordless authentication so that I can plan and deploy passwordless methods across my device fleet.
ai-usage: ai-assisted
---

# Passwordless authentication with Microsoft Intune

Passwordless authentication reduces phishing and credential theft by replacing passwords with stronger sign-in methods such as Windows Hello, FIDO2 security keys, passkeys, certificates, Microsoft Authenticator phone sign-in, and Temporary Access Pass.

Microsoft Intune doesn't issue passwordless credentials. Instead, it prepares devices, apps, and user experiences so these passwordless methods work reliably at scale. Microsoft Entra ID is the identity authority that verifies credentials and enforces authentication and Conditional Access policies, while Microsoft Intune configures device settings, enforces compliance, and enables the platform capabilities those methods depend on. Together, Microsoft Entra ID and Microsoft Intune provide the identity foundation and device readiness required to adopt passwordless authentication across diverse platforms and form factors.

The passwordless experience varies by platform. On Windows, it commonly spans both device sign‑in and app access through SSO. On macOS, it centers on platform authentication and SSO into apps, rather than deep device‑bound identity. On iOS/iPadOS and Android, it more often focuses on app sign‑in, brokered authentication, and passkey behavior than on device sign‑in. Keep these distinctions in mind when evaluating platform requirements and planning deployment.

This article explains how Microsoft Intune supports a passwordless strategy from an administrator's perspective. For deployment details, follow the implementation links for each passwordless method.

## How Microsoft's passwordless solution works

Microsoft's passwordless solution pairs Microsoft Entra ID for identity and single sign‑on (SSO) with Microsoft Intune for device configuration and policy enforcement. This combination enables users to authenticate by using strong credentials - such as biometrics, FIDO2 security keys, or passkeys - without entering passwords.

:::row:::
   :::column span="1":::
   :::image type="icon" source="media/passwordless/entra.svg" border="false":::
   :::column-end:::
   :::column span="3":::
      **Microsoft Entra ID** is the core identity provider. It verifies passwordless credentials like Windows Hello PINs, FIDO2 keys, and passkeys. After successful authentication, Microsoft Entra ID issues a Primary Refresh Token (PRT) or equivalent, enabling seamless SSO to Microsoft 365, Azure, and other protected resources. Conditional Access policies evaluate device state, authentication strength, and risk signals before granting access.
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="1":::
   :::image type="icon" source="media/passwordless/intune.svg" border="false":::
   :::column-end:::
   :::column span="3":::
   **Microsoft Intune** prepares devices for passwordless sign-in by configuring settings, enforcing compliance, deploying required apps, and supporting the platform experiences that make passwordless practical at scale. Microsoft Intune gives admins one management plane for Windows, macOS, iOS/iPadOS, and Android.
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="1":::
   :::image type="icon" source="media/passwordless/devices.svg" border="false":::
   :::column-end:::
   :::column span="3":::
   **Platform capabilities** on Windows, macOS, iOS, and Android provide the device-bound experience, including biometrics, secure hardware (TPM on Windows, Secure Enclave on macOS), passkey support, and brokered single sign-on.
   :::column-end:::
:::row-end:::

This separation is important. Microsoft Entra ID is the identity authority. Microsoft Intune is the management layer that helps users adopt and use those methods successfully.

## Passwordless, MFA, and phishing resistance

Passwordless authentication doesn't eliminate security factors. Most passwordless methods actually fulfill multifactor authentication (MFA) requirements. For example, Windows Hello uses a device‑bound credential (possession) paired with a biometric gesture (inherence) or a PIN (knowledge), satisfying MFA by design. As a result, Conditional Access authentication strength policies classify many passwordless methods as *MFA‑compliant* or even as *phishing‑resistant MFA*.

Not all passwordless options provide the same level of protection. Understanding the difference between *phishing‑resistant* and *non‑phishing‑resistant* methods helps you select the right authentication strengths and design a secure identity strategy.

- **Phishing‑resistant** methods use hardware‑bound, asymmetric cryptographic keys that can't be intercepted or replayed - even if a user interacts with a malicious or spoofed prompt.
- **Non‑phishing‑resistant** methods use passwordless flows but can still be compromised through social engineering, prompt manipulation, or MFA fatigue.

Each method described later in this article includes its level of phishing resistance.

:::image type="icon" source="../media/icons/16/learn-more.svg" border="false"::: **Learn more**

- [Passwordless authentication options for Microsoft Entra ID](/entra/identity/authentication/concept-authentication-passwordless)
- [Get started with phishing-resistant passwordless authentication deployment in Microsoft Entra ID](/entra/identity/authentication/how-to-plan-prerequisites-phishing-resistant-passwordless-authentication)

## Benefits of passwordless authentication with Microsoft Intune

When you use Microsoft Intune, Microsoft Entra ID, and platform capabilities together, your organization gains:

- **Seamless single sign-on**: Users sign in once to the device and get automatic access to apps, cloud services, and - in some cases - on-premises resources. Password reset calls and repeated authentication prompts are eliminated.
- **User convenience across devices**: Users get a native, consistent experience across devices. Windows Hello uses OS sign‑in, macOS integrates Touch ID with Microsoft Entra ID, and mobile platforms use Microsoft Authenticator and platform passkeys. Users don't need to juggle separate passwords per device.
- **Stronger security posture**: Phishing-resistant methods prevent credential theft and replay attacks. Device compliance gating ensures that even valid credentials only work from healthy, managed devices - aligning with Zero Trust principles.
- **Reduced IT support load**: Fewer password resets, smoother onboarding with Temporary Access Pass, and self-service recovery options reduce helpdesk volume.
- **Future-ready architecture**: As standards evolve, new passwordless methods - including synced passkeys and hardware‑backed credentials - can plug into the same Microsoft Entra ID + Microsoft Intune architecture without requiring major redesign.

## How Microsoft Intune drives passwordless adoption

Microsoft Intune enables and operationalizes passwordless authentication by ensuring that devices and applications are properly configured to use strong, modern credentials. While Microsoft Entra ID governs identity and authentication policy, Microsoft Intune prepares the device environment that passwordless methods depend on.

Key contributions include:

- **Device readiness**: Enrolling, registering, and configuring devices so they can participate in passwordless sign‑in flows.
- **Configuration deployment**: Delivering the policies required for Windows Hello for Business, certificate-based authentication, Apple Platform SSO, and similar platform capabilities.
- **Compliance and access signals**: Supplying device health and compliance data that Conditional Access evaluates before granting access.
- **App and broker provisioning**: Deploying core applications—such as Microsoft Authenticator and Microsoft Intune Company Portal—that enable identity brokering and passwordless SSO scenarios.
- **Unified cross‑platform management**: Providing a consistent policy and management framework across Windows, macOS, iOS/iPadOS, and Android to streamline enterprise deployment.

The passwordless methods available to users depend on both the device platform and the authentication options enabled in Microsoft Entra ID. Microsoft Intune ensures that each device is prepared, configured, and capable of delivering a secure and reliable passwordless experience.

:::row:::
    :::column span="1":::
#### Windows Hello

:::image type="icon" source="media/passwordless/windows-hello.svg" border="false":::
:::column-end:::
:::column span="3":::
> :::image type="icon" source="../media/icons/16/check.svg" border="false"::: **Phishing-resistant**
>
> Windows Hello replaces passwords with a device-bound asymmetric key that's generated and sealed to the TPM. Access to the key is controlled by a PIN or biometric gesture (fingerprint or facial recognition), combining possession and inherence in a single sign-in step. This method is hardware-backed and phishing-resistant for Windows devices.
>
>  :::image type="icon" source="../media/icons/16/intune.svg" border="false"::: **Intune's role**  
> Microsoft Intune prepares Windows devices for Windows Hello by delivering and enforcing Windows Hello for Business policy settings.
>
> This method is most relevant when you need to:
>
> - Prepare cloud-first Windows devices for passwordless sign-in.
> - Deliver Windows Hello for Business policy settings during enrollment and ongoing management.
> - Align Windows sign-in with device compliance and modern management. 
>
> :::image type="icon" source="../media/icons/16/learn-more.svg" border="false"::: **Learn more**
> - [Windows Hello for Business overview](/windows/security/identity-protection/hello-for-business/hello-overview)
> - [Passwordless strategy guide for organizations](/windows/security/identity-protection/passwordless-strategy)
:::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
#### FIDO2 Security Keys

:::image type="icon" source="media/passwordless/security-key.svg" border="false":::
:::column-end:::
:::column span="3":::

> :::image type="icon" source="../media/icons/16/check.svg" border="false"::: **Phishing-resistant**
>
>FIDO2 security keys are physical devices (USB, NFC, or Bluetooth) that store a FIDO credential and provide phishing-resistant authentication without relying on the device platform. Because the credential is bound to the hardware key and verified through a cryptographic challenge, it can't be intercepted or replayed. FIDO2 keys are ideal for shared devices, high-assurance environments, or as a recovery path alongside platform-based credentials.
>
> :::image type="icon" source="../media/icons/16/intune.svg" border="false"::: **Intune's role**  
> Microsoft Intune can help make devices ready for this method by managing supported platforms and related sign-in experiences.
>
>This method is often a good fit when organizations need:
>
>- A portable passwordless option for shared or specialized devices.
>- A strong phishing-resistant option that isn't tied to a single platform or to Microsoft Authenticator.
>- A recovery or alternate path alongside platform-based credentials.
>
> :::image type="icon" source="../media/icons/16/learn-more.svg" border="false"::: For implementation guidance, see:
>- [Passwordless authentication options for Microsoft Entra ID](/entra/identity/authentication/concept-authentication-passwordless)

:::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
#### Passkeys

:::image type="icon" source="media/passwordless/passkey.svg" border="false":::
:::column-end:::
:::column span="3":::
> :::image type="icon" source="../media/icons/16/check.svg" border="false"::: **Phishing-resistant**
>
> Passkeys are the standards-based umbrella for FIDO credentials that can be either device-bound or synced across devices. In Microsoft Entra ID, you can use:
>
> - **Device-bound passkeys** stored in secure hardware (TPM or Secure Enclave) on a single device, such as through Windows Hello or Microsoft Authenticator on iOS 17+ and Android 14+.
> - **Synced passkeys** managed by platform password managers (such as iCloud Keychain or Google Password Manager) or supported third-party providers, which enable cross-device use.
> - **Microsoft Entra passkey on Windows** is a FIDO2 passkey that uses Windows Hello for biometric verification but doesn't require device join or registration. Users can register multiple passkeys for multiple Microsoft Entra accounts on the same device, making it well suited for shared devices, unmanaged endpoints, and scenarios where Windows Hello for Business isn't provisioned.
>
> :::image type="icon" source="../media/icons/16/intune.svg" border="false"::: **Intune's role**  
>  From a Microsoft Intune perspective, passkeys are mostly about platform and app readiness—managing the device and app prerequisites that make passkey adoption viable across platforms.
>
>This dependency is especially important on:
>
> - **Windows**, where platform sign-in and Windows Hello can intersect with broader passwordless planning. Microsoft Entra passkey on Windows extends passkey coverage to devices that aren't enrolled or joined, complementing Windows Hello for Business on managed devices.
> - **iOS/iPadOS** and **Android**, where passkeys can depend on mobile device state and app broker behavior.
> - **macOS**, where platform identity integration and user sign-in experience shape adoption.
>
> :::image type="icon" source="../media/icons/16/learn-more.svg" border="false"::: For implementation guidance, see:
> - [Passwordless authentication options for Microsoft Entra ID](/entra/identity/authentication/concept-authentication-passwordless)
> - [Microsoft Entra passkey on Windows](/entra/identity/authentication/how-to-authentication-entra-passkeys-on-windows)
:::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::

#### Microsoft Authenticator phone sign-in

:::image type="icon" source="media/passwordless/authenticator.svg" border="false":::
:::column-end:::
:::column span="3":::
>  :::image type="icon" source="../media/icons/16/caution.svg" border="false"::: **Not phishing-resistant**
>
> Microsoft Authenticator phone sign-in replaces passwords with push-based approval and number matching on the user's trusted mobile device. It's convenient and widely supported, but relies on push notifications rather than hardware-bound credentials, which means it doesn't fully prevent phishing attacks such as MFA prompt manipulation.
>
>> [!NOTE]
>> Microsoft Authenticator can *also* store device-bound passkeys (iOS 17+, Android 14+), which *are* phishing-resistant. This section covers the push-based phone sign-in flow specifically.
>
> :::image type="icon" source="../media/icons/16/intune.svg" border="false"::: **Intune's role**  
> Microsoft Intune supports this flow by deploying and managing the mobile app and device prerequisites.
>
> In many environments, this support includes:
>
> - Deploying Microsoft Authenticator to managed mobile devices.
> - Supporting the brokered sign-in experience across Microsoft apps.
> - Accounting for app protection policy considerations on mobile platforms when those are part of the broader mobile access design.
>
> :::image type="icon" source="../media/icons/16/learn-more.svg" border="false"::: For implementation guidance, see:
>
> - [Passwordless authentication options for Microsoft Entra ID](/entra/identity/authentication/concept-authentication-passwordless)
:::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
#### Temporary Access Pass

:::image type="icon" source="media/passwordless/tap.svg" border="false":::
:::column-end:::
:::column span="3":::
> :::image type="icon" source="../media/icons/16/caution.svg" border="false"::: **Not a permanent method** — used for onboarding and recovery
>
> Temporary Access Pass (TAP) is a time-limited credential that an admin issues to help users bootstrap or recover access before they complete their long-term passwordless setup. TAP isn't a permanent passwordless method and isn't phishing-resistant, but it's often a critical part of a successful rollout because it solves the first-sign-in problem without issuing a password.
>
> :::image type="icon" source="../media/icons/16/intune.svg" border="false"::: **Intune's role**  
> From a Microsoft Intune perspective, Temporary Access Pass matters when you want to:
>
> - Simplify onboarding to passwordless methods.
> - Reduce reliance on temporary passwords during deployment.
> - Connect onboarding scenarios to managed Windows device setup.
>
> **Day-zero onboarding with TAP**
>
> A common challenge in passwordless deployments is the *chicken-and-egg* problem: a new user needs to sign in to register their passwordless credential, but you don't want to issue a password for that first sign-in. TAP solves this problem by providing a short-lived credential for initial device setup and credential registration.
>
> A typical onboarding flow looks like this:
> 
> 1. **Admin issues a TAP** — The IT admin or automated workflow generates a time-limited TAP for the new user in the Microsoft Entra admin center or via Microsoft Graph API.
> 1. **User sets up their device** — The user enters the TAP during Windows Autopilot OOBE, the macOS setup assistant, or mobile device enrollment. On Windows 11, Web sign-in enables TAP entry directly at the lock screen.
> 1. **User registers a passwordless method** — After signing in with the TAP, the user is prompted to register Windows Hello, a FIDO2 security key, a passkey in Microsoft Authenticator, or another passwordless method. This is the permanent credential that replaces the TAP.
> 1. **TAP expires** — The TAP is single-use or time-limited (configurable), so it can't be reused after the user registers their passwordless method.
> 
> This flow eliminates the need to issue and then revoke a temporary password, and gives Microsoft Intune a managed onboarding path from the first sign-in.
> 
> :::image type="icon" source="../media/icons/16/learn-more.svg" border="false"::: For implementation guidance, see:
> 
> - [Use a Temporary Access Pass](/entra/identity/authentication/howto-authentication-temporary-access-pass)
> - [Overview of Windows Autopilot](/autopilot/windows-autopilot)
> - [Web sign-in for Windows](/windows/security/identity-protection/web-sign-in/?tabs=intune)

:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
#### **Certificate-Based Authentication (CBA)**

:::image type="icon" source="media/passwordless/certificate.svg" border="false":::
:::column-end:::
:::column span="3":::
> :::image type="icon" source="../media/icons/16/check.svg" border="false"::: **Phishing-resistant**
>
> Certificate-based authentication (CBA) uses digital certificates and asymmetric cryptography to verify identity, making it phishing-resistant and preventing credential replay. It's widely adopted in regulated industries and government environments, often through smart cards such as PIV and CAC. Unlike other passwordless methods where Microsoft Intune primarily prepares the device environment, CBA is one area where Microsoft Intune plays a direct role in distributing the credential itself.
>
> :::image type="icon" source="../media/icons/16/intune.svg" border="false"::: **Intune's role**  
> Microsoft Intune supports two infrastructure models for certificate delivery:
>
> - **On-premises PKI**: Organizations with an existing certification authority (CA) can use the Certificate Connector for Microsoft Intune to bridge their on-premises PKI with Microsoft Intune. The connector enables Microsoft Intune to deploy SCEP and PKCS certificate profiles to managed devices using your existing CA infrastructure. This model suits organizations that already operate an enterprise CA or need to integrate with established PKI investments.
> - **Microsoft Cloud PKI**: For organizations that want to simplify or eliminate on-premises certificate infrastructure, Microsoft Cloud PKI provides a cloud-based CA as part of the Microsoft Intune Suite. Cloud PKI issues and manages certificates without requiring on-premises servers, connectors, or hardware security modules.
>
> Regardless of infrastructure model, Microsoft Intune delivers certificates to devices using certificate profiles:
>
> - **Trusted root certificate profiles** distribute your CA's root certificate so devices can establish the trust chain.
> - **SCEP certificate profiles** request and deploy certificates from a SCEP-enabled CA.
> - **PKCS certificate profiles** request and deploy certificates using the PKCS #12 standard.
> - **Imported PFX certificate profiles** deploy pre-generated certificates that are imported into Microsoft Intune.
>
>These profiles work across Windows, macOS, iOS/iPadOS, and Android, making Microsoft Intune the delivery mechanism that connects your PKI infrastructure—whether on-premises or cloud-based—to the identity method defined in Microsoft Entra ID.
>
> :::image type="icon" source="../media/icons/16/learn-more.svg" border="false"::: For implementation guidance, see:
>
> - [Use certificates for authentication in Microsoft Intune](/certificates-configure.md)
> - [Microsoft Cloud PKI overview](../cloud-pki/index.md)
> - [Certificate Connector for Microsoft Intune](/certificate-connector-overview.md)
> - [Passwordless authentication options for Microsoft Entra ID](/entra/identity/authentication/concept-authentication-passwordless)
:::column-end:::
:::row-end:::

## Prerequisites

Before you plan a passwordless deployment, verify that your environment meets the licensing and platform requirements for the methods you intend to use. Some passwordless features require specific Microsoft Entra ID or Microsoft Intune license tiers, and each method has minimum OS version requirements.

### Licensing requirements

Depending on the passwordless methods you choose, your organization might need Microsoft Entra ID P1 or Microsoft Entra ID P2 licenses for users, as well as specific Microsoft Intune licenses for device management and certificate delivery. The following table summarizes the licensing requirements for common passwordless capabilities:

| Capability                                   | License requirement                                          |
|----------------------------------------------|--------------------------------------------------------------|
| Windows Hello                                | Microsoft Entra ID P1 (for Conditional Access enforcement)   |
| FIDO2 security keys                          | Microsoft Entra ID P1                                        |
| Passkeys (device-bound and synced)           | Microsoft Entra ID P1                                        |
| Microsoft Authenticator phone sign-in        | Microsoft Entra ID P1                                        |
| Temporary Access Pass                        | Microsoft Entra ID P1                                        |
| Certificate-based authentication (CBA)       | Microsoft Entra ID P1 (P2 for risk-based Conditional Access) |
| Authentication strength policies             | Microsoft Entra ID P1                                        |
| Risk-based Conditional Access                | Microsoft Entra ID P2                                        |
| Microsoft Cloud PKI                          | Microsoft Intune Suite add-on or standalone Cloud PKI add-on |
| Device compliance and configuration profiles | Microsoft Intune Plan 1                                      |

:::image type="icon" source="../media/icons/16/learn-more.svg" border="false"::: **Learn more**
- [Microsoft Entra plans and pricing](/entra/fundamentals/licensing)
- [Microsoft Intune licensing](../fundamentals/licensing/index.md)

### Platform requirements

The passwordless methods described in this article rely on specific platform capabilities that are only available in certain OS versions. The following table summarizes the platform requirements for each method:

| Method                                               | Windows                         | macOS                    | iOS/iPadOS               | Android     |
|------------------------------------------------------|:-------------------------------:|:------------------------:|:------------------------:|:-----------:|
| **Windows Hello**                                    | All *supported* Windows clients | —                        | —                        | —           |
| **FIDO2 security keys**                              | All *supported* Windows clients | —                        | —                        | —           |
| **Passkeys**                                         | Windows 11                      | All *supported* versions | All *supported* versions | Android 14+ |
| **Device-bound passkeys in Microsoft Authenticator** | —                               | —                        | All *supported* versions | Android 14+ |
| **Platform SSO (Secure Enclave)**                    | —                               | All *supported* versions | —                        | —           |
| **Web sign-in (TAP at lock screen)**                 | Windows 11                      | —                        | —                        | —           |
| **Microsoft Authenticator phone sign-in**            | —                               | —                        | All *supported* versions | Android 11+ |

>[!NOTE]
> 
> *Supported* refers to operating system versions that Microsoft Intune currently supports for full functionality, policy deployment, and management.  
> Platform version requirements can change with each release cycle. Always verify current requirements in the product documentation for the specific method you're deploying.

:::image type="icon" source="../media/icons/16/learn-more.svg" border="false"::: **Learn more**
- [Intune supported operating systems](../fundamentals/ref-supported-platforms.md#supported-operating-systems-and-browsers-in-intune)

## Platform considerations

Passwordless isn't one feature. It's a set of platform-specific experiences that rely on Microsoft Entra ID for identity and Microsoft Intune for device management.

:::row:::
    :::column span="1":::
#### Windows

:::image type="icon" source="media/passwordless/windows.svg" border="false":::
:::column-end:::
:::column span="3":::
> Windows is the most complete example of how device enrollment, cloud sign-in, security posture, and passwordless user experience work together.
> 
> Microsoft Intune commonly supports Windows passwordless scenarios by:
> 
> - Preparing cloud-first, Microsoft Entra joined devices.
> - Delivering Windows Hello for Business configuration.
> - Supporting FIDO2 security key experiences.
> - Aligning device readiness with compliance and modern management.
> - Supporting onboarding experiences that can connect to Windows Autopilot.
> 
> When a user signs in with Windows Hello or a FIDO2 key, Windows obtains a Primary Refresh Token from Microsoft Entra ID. That PRT enables seamless SSO to Microsoft 365 apps, SaaS applications, and - when Cloud Kerberos Trust is configured - on-premises resources like file shares, all without additional sign-in prompts.
> 
> :::image type="icon" source="../media/icons/16/learn-more.svg" border="false"::: **Learn more**
> 
> - [Windows Hello for Business overview](/windows/security/identity-protection/hello-for-business/hello-overview)
> - [Passwordless strategy guide for organizations](/windows/security/identity-protection/passwordless-strategy)
> - [Overview of Windows Autopilot](/autopilot/windows-autopilot)
>
> **Hybrid and legacy considerations**
> 
> The passwordless experiences described in this article assume a cloud-first direction with Microsoft Entra joined devices. Organizations with hybrid Microsoft Entra joined devices should be aware of these differences:
> 
> - **Web sign-in** (used for TAP at the Windows lock screen) is supported only on Microsoft Entra joined devices, not hybrid Microsoft Entra joined devices.
> - **Windows Hello for Business** works on both Microsoft Entra joined and hybrid Microsoft Entra joined devices, but hybrid deployments may require additional infrastructure depending on the trust model.
> - **On-premises resource access** from Microsoft Entra joined devices requires cloud Kerberos trust or certificate-based trust. Cloud Kerberos trust is the recommended model because it doesn't require deploying certificates for Kerberos authentication. For more information, see [cloud Kerberos trust deployment](/windows/security/identity-protection/> hello-for-business/deploy/hybrid-cloud-kerberos-trust).
> - **Legacy applications** that require Active Directory Kerberos authentication can still work with passwordless methods, but applications that require NTLM or direct LDAP bind might need extra planning.
> 
> If your environment is hybrid, plan your passwordless rollout starting with Microsoft Entra joined devices and expand to hybrid Microsoft Entra joined devices as your infrastructure supports it.
> 
> :::image type="icon" source="../media/icons/16/learn-more.svg" border="false"::: **Learn more**
> - [Configure single sign-on for Microsoft Entra joined devices](/windows/security/identity-protection/hello-for-business/hello-hybrid-aadj-sso)
:::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
#### macOS

:::image type="icon" source="media/passwordless/macos.svg" border="false":::
:::column-end:::
:::column span="3":::
> On macOS, passwordless planning depends on how Microsoft Entra ID integrates with the platform sign-in and single sign-on experience. Microsoft Intune delivers the device configuration needed for Apple-focused identity integrations.
> 
> With the Microsoft Enterprise SSO plug-in and Apple's Platform SSO framework, Microsoft Intune can deploy a configuration that allows users to sign in to the Mac using their Microsoft Entra ID credentials. When configured with the Secure Enclave key method, this provides a phishing-resistant, hardware-backed sign-in experience similar to Windows Hello.
> 
> This information matters when you're planning:
> 
> - Platform SSO and related sign-in experiences.
> - Single sign-on between the device and Microsoft apps.
> - A consistent management model alongside Windows and mobile devices.
> 
> :::image type="icon" source="../media/icons/16/learn-more.svg" border="false"::: **Learn more**
> 
> - [Microsoft Enterprise SSO plug-in and Platform SSO for Apple devices](/entra/identity-platform/apple-sso-plugin)
> - [Platform SSO configuration guide for macOS devices](../device-configuration/settings-catalog/configure-platform-sso-macos.md)
:::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
#### iOS and iPadOS

:::image type="icon" source="media/passwordless/apple-mobile.svg" border="false":::
:::column-end:::
:::column span="3":::
> On iOS and iPadOS, passwordless planning focuses more on app sign-in, brokered authentication, and passkey behavior than on device sign-in. Microsoft Intune deploys and manages the apps and settings that make those experiences consistent for users.
> 
> The Microsoft SSO extension on iOS can intercept authentication requests across Microsoft and third-party apps, enabling seamless sign-in after initial device setup. Microsoft Authenticator acts as the authentication broker, and can also store device-bound passkeys on iOS 17+ for phishing-resistant authentication.
> 
> :::image type="icon" source="../media/icons/16/learn-more.svg" border="false"::: **Learn more**
> 
> - [Microsoft Enterprise SSO plug-in and Platform SSO for Apple devices](/entra/identity-platform/apple-sso-plugin)
> - [Passwordless authentication options for Microsoft Entra ID](/entra/identity/authentication/concept-authentication-passwordless)
> - [Use the Microsoft Enterprise SSO plug-in on iOS/iPadOS devices](../device-configuration/settings-catalog/configure-enterprise-sso-plugin-ios.md)
:::row-end:::

:::row:::
:::column span="1":::
#### Android

:::image type="icon" source="media/passwordless/android.svg" border="false":::
:::column-end:::
:::column span="3":::
> On Android, Microsoft Intune establishes the managed context that passwordless and brokered authentication flows depend on. This context is especially relevant when Microsoft Authenticator or related app experiences are part of your mobile access design.
> 
> Both Company Portal and Microsoft Authenticator can act as authentication brokers on Android. After a user signs in through the broker, Microsoft Entra ID issues a Primary Refresh Token that enables SSO across all broker-aware apps in the work profile. On Android 14+, Microsoft Authenticator can also store device-bound passkeys for phishing-resistant authentication.
> 
> :::image type="icon" source="../media/icons/16/learn-more.svg" border="false"::: **Learn more**
> 
> - [Passwordless authentication options for Microsoft Entra ID](/entra/identity/authentication/concept-authentication-passwordless)
:::column-end:::
:::row-end:::

## Dependencies for passwordless authentication

### Zero Trust architecture

Passwordless authentication is one part of a broader identity and device access strategy. For a Microsoft Intune administrator, planning usually involves these layers:

- **Identity**: Phishing-resistant authentication methods in Microsoft Entra ID.
- **Device trust**: Microsoft Intune enrollment, compliance, and configuration.
- **Access policy**: Conditional Access and related exclusion planning.
- **Data protection**: Microsoft Purview capabilities that help protect content after access is granted.
- **Investigation and response**: Microsoft Defender signals and workflows when risk or compromise needs follow-up.

:::image type="icon" source="../media/icons/16/learn-more.svg" border="false"::: **Learn more**

- [What is Zero Trust?](/security/zero-trust/zero-trust-overview)
- [Common security policies for Microsoft 365 organizations](/security/zero-trust/zero-trust-identity-device-access-policies-common)

### Conditional Access

Conditional Access evaluates signals such as device state and authentication strength before granting access. When combined with passwordless methods, Conditional Access can enforce authentication strength policies that require phishing-resistant MFA - effectively mandating passwordless by blocking weaker methods like passwords or SMS codes.

When you implement Conditional Access alongside passwordless, also account for emergency access planning to prevent accidental lockout scenarios.

:::image type="icon" source="../media/icons/16/learn-more.svg" border="false"::: **Learn more**

- [Build a Conditional Access policy](/entra/identity/conditional-access/concept-conditional-access-policies)
- [Conditional Access authentication strengths](/entra/identity/authentication/concept-authentication-strengths)

### Emergency access and recovery

A common concern when removing passwords is what happens when a user loses their only passwordless device - a phone, a FIDO2 key, or a laptop with Windows Hello. Without a recovery plan, admins can face support escalations and users can be locked out of critical resources.

Plan for these scenarios as part of your passwordless deployment:

- **Emergency access accounts**: Maintain at least two break-glass accounts that are excluded from Conditional Access policies and passwordless enforcement. These accounts provide a fallback path if a misconfiguration or outage blocks all other access. Store credentials securely and monitor sign-in activity on these accounts.
- **Recovery with Temporary Access Pass**: When a user loses their passwordless device, an admin can issue a new TAP so the user can sign in and register a replacement credential. This approach avoids resetting the user to a password and keeps the recovery flow within the passwordless model.
- **Multiple registered methods**: Encourage users to register more than one passwordless method where possible. For example, a user who uses Hello for Business on their laptop might also register a passkey in Microsoft Authenticator on their phone. If one device is lost, the other method still works.
- **Self-service credential management**: Users can manage their authentication methods at [My Security Info](https://mysignins.microsoft.com/security-info). When combined with TAP-based recovery, this approach reduces helpdesk dependency for credential resets.
- **Total loss recovery with Verified ID**: For scenarios where a user loses all registered credentials and devices, Microsoft Entra account recovery using Verified ID provides an identity-verified recovery path that doesn't rely on passwords or helpdesk-issued credentials.

Planning for recovery before you enforce passwordless is essential. A rollout that blocks passwords without a recovery path creates the kind of lockout scenarios that erode admin and user confidence in the transition.

:::image type="icon" source="../media/icons/16/learn-more.svg" border="false"::: **Learn more**

- [Manage emergency access accounts in Microsoft Entra ID](/entra/identity/role-based-access-control/security-emergency-access)
- [Account recovery with Microsoft Entra Verified ID](/entra/identity/authentication/concept-account-recovery-overview)

### Compliance and device readiness

Passwordless often depends on the device being in the right state before users can rely on the experience. Readiness typically includes:

- [Supported device platforms and versions](../fundamentals/ref-supported-platforms.md)
- [Device enrollment or registration](../device-enrollment/enroll-devices.md)
- [Required apps and brokers](../intune-service/apps/apps-add.md)
- [Method-specific configuration profiles and identity prerequisites](../device-configuration/overview.md)

### Verification and ongoing operations

To validate a passwordless deployment, common checkpoints include:

- [Microsoft Entra sign-in logs](/entra/identity/monitoring-health/concept-sign-ins)
- [Microsoft Intune device and policy reporting](../device-management/reports/overview.md)
- Platform-specific verification experiences for the passwordless method you deploy.

## User adoption and communication

Technical readiness is only one part of a passwordless rollout. Users who are accustomed to passwords might experience confusion or resistance when sign-in flows change. Planning for user communication and support can make the difference between a smooth transition and widespread helpdesk escalation.

Consider these practices:

- **Communicate the change early**: Let users know that their sign-in experience is changing, why it's changing, and what to expect. Focus on the benefits - fewer passwords to remember, faster sign-in, and stronger security.
- **Provide platform-specific guidance**: The passwordless experience is different on Windows (Hello biometric or PIN), macOS (Touch ID with Platform SSO), iOS (Authenticator or passkeys), and Android (Authenticator broker). Tailor communication to the platforms your users have.
- **Identify pilot groups**: Start with a group of users who can test the experience and provide feedback before you enforce passwordless across the organization. IT staff, early adopters, and security-aware teams are often good candidates.
- **Prepare helpdesk staff**: Ensure your support team knows how to issue a Temporary Access Pass for recovery, how to guide users through credential registration, and where to check sign-in logs when issues arise.

:::image type="icon" source="../media/icons/16/learn-more.svg" border="false"::: **Learn more**

- [Microsoft Entra end-user rollout templates and materials](https://www.microsoft.com/en-us/download/details.aspx?id=57600)
- [Authentication Methods Activity](/entra/identity/authentication/howto-authentication-methods-activity)

## Related articles

- [Passwordless authentication options for Microsoft Entra ID](/entra/identity/authentication/concept-authentication-passwordless)
- [Deploy phishing-resistant passwordless authentication in Microsoft Entra ID](/entra/identity/authentication/how-to-deploy-phishing-resistant-passwordless-authentication)
- [Windows Hello for Business overview](/windows/security/identity-protection/hello-for-business/hello-overview)
- [Passwordless strategy guide for organizations](/windows/security/identity-protection/passwordless-strategy)
- [Microsoft Enterprise SSO plug-in and Platform SSO for Apple devices](/entra/identity-platform/apple-sso-plugin)
- [Use a Temporary Access Pass](/entra/identity/authentication/howto-authentication-temporary-access-pass)
- [Use certificates for authentication in Microsoft Intune](/certificates-configure.md)
- [Microsoft Cloud PKI overview](../cloud-pki/index.md)
- [Overview of Windows Autopilot](/autopilot/windows-autopilot)
- [Build a Conditional Access policy](/entra/identity/conditional-access/concept-conditional-access-policies)
- [What is Zero Trust?](/security/zero-trust/zero-trust-overview)
- [Common security policies for Microsoft 365 organizations](/security/zero-trust/zero-trust-identity-device-access-policies-common)
- [Passwordless for Students](/microsoft-365/education/guide/1-reference/protect-passwordless-students)
