---
title: Passwordless authentication with Microsoft Intune
description: Learn how Microsoft Intune supports passwordless authentication across Windows, macOS, iOS, and Android, and how it connects with Microsoft Entra ID and related platform capabilities.
ms.date: 03/24/2026
ms.topic: concept-article
author: paolomatarazzo
ms.author: paoloma
ms.reviewer:
ms.custom:
  - ai-assisted
  - msecd-doc-authoring-scenarios
ms.collection:
  - M365-identity-device-management
  - intune-scenario
ai-usage: ai-assisted
---

# Passwordless authentication with Microsoft Intune

Passwordless authentication helps reduce phishing and credential theft by replacing passwords with stronger sign-in methods, such as Windows Hello for Business, FIDO2 security keys, passkeys, certificate-based authentication, Microsoft Authenticator phone sign-in, and Temporary Access Pass.

Microsoft Intune doesn't issue passwordless credentials. Instead, it helps you prepare devices, apps, and user experiences so these methods work consistently across your organization. Microsoft Entra ID provides the identity controls and authentication methods, while Intune enforces the device state and configuration those methods depend on.

This article explains how Intune fits into a passwordless strategy from an Intune administrator's perspective. When you're ready to deploy a specific method, use the implementation links throughout this article.

## How Microsoft's passwordless solution works

Microsoft's passwordless solution integrates Entra ID for identity and single sign-on (SSO) with Intune for device configuration and policy enforcement. This combination enables users to authenticate using strong credentials—such as biometrics, FIDO2 security keys, or passkeys—without entering passwords.

:::row:::
   :::column span="1":::
   :::image type="icon" source="icons/entra.svg" border="false":::
   :::column-end:::
   :::column span="3":::
   **Microsoft Entra ID** is the core identity provider. It verifies passwordless credentials like Windows Hello PINs, FIDO2 keys, and passkeys. Upon successful authentication, Entra ID issues a Primary Refresh Token (PRT) or equivalent, enabling seamless SSO to Microsoft 365, Azure, and other protected resources. Conditional Access policies evaluate device state, authentication strength, and risk signals before granting access.
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="1":::
   :::image type="icon" source="icons/intune.svg" border="false":::
   :::column-end:::
   :::column span="3":::
   **Microsoft Intune** prepares devices for passwordless sign-in by configuring settings, enforcing compliance, deploying required apps, and supporting the platform experiences that make passwordless practical at scale. Intune gives admins one management plane for Windows, macOS, iOS/iPadOS, and Android.
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="1":::
   :::image type="icon" source="icons/devices.svg" border="false":::
   :::column-end:::
   :::column span="3":::
   **Platform capabilities** on Windows, macOS, iOS, and Android provide the device-bound experience, including biometrics, secure hardware (TPM, Secure Enclave), passkey support, and brokered single sign-on.
   :::column-end:::
:::row-end:::

This separation is important. Microsoft Entra ID is the identity authority. Microsoft Intune is the management layer that helps users adopt and use those methods successfully.

## What counts as passwordless

Not all passwordless methods offer the same level of protection. Understanding the difference between phishing-resistant and non-phishing-resistant methods is important when designing your strategy.

### Phishing-resistant methods

Phishing attacks trick users into revealing credentials or approving fraudulent sign-ins. Phishing-resistant MFA ensures credentials can't be intercepted or replayed, even if a user is tricked.

- **Passkeys (FIDO)** are the standards-based umbrella. In Entra ID you can use:
  - **Device-bound passkeys** on platform authenticators like Windows Hello for Business and Microsoft Authenticator (iOS/Android). These are stored in secure hardware (TPM/Secure Enclave) on a single device.
  - **Synced passkeys** in platform password managers (such as iCloud Keychain and Google Password Manager) and some third-party providers.
- **FIDO2 security keys** are external keys (USB/NFC/BLE) that hold a FIDO credential. Ideal for shared devices or high-assurance scenarios.
- **Certificate-based authentication (CBA)** uses digital certificates and asymmetric cryptography, preventing credential replay. Widely adopted in regulated industries and government environments through smart cards such as PIV and CAC.
- **Windows Hello for Business** uses a device-bound asymmetric key sealed to the TPM, with access controlled by PIN or biometric gesture.

### Other passwordless methods

These methods eliminate passwords but don't fully prevent phishing:

- **Microsoft Authenticator phone sign-in** replaces passwords with push-based approval and number matching. Convenient and widely supported, but relies on push notifications rather than hardware-bound credentials.
- **Temporary Access Pass (TAP)** is a time-limited credential for onboarding or recovery. Not a permanent method, but often part of a successful rollout.

For a complete comparison of authentication methods, see [Passwordless authentication options for Microsoft Entra ID](/entra/identity/authentication/concept-authentication-passwordless).

## What Microsoft Intune contributes

Microsoft Intune commonly supports passwordless adoption in these areas:

- **Device readiness**: Enrolling or registering devices and applying the settings required for supported passwordless experiences.
- **Configuration delivery**: Deploying profiles and policies for scenarios such as Windows Hello for Business, certificates, and Apple SSO-related settings.
- **Compliance and access signals**: Reporting device state that related solutions, such as Conditional Access, evaluate before granting access.
- **App and broker preparation**: Deploying apps such as Microsoft Authenticator and Company Portal where platform flows depend on them.
- **Cross-platform consistency**: Giving admins one management plane for Windows, macOS, iOS/iPadOS, and Android.

## Passwordless methods and Intune's role

### Windows Hello for Business

Windows Hello for Business is a hardware-backed, phishing-resistant sign-in method for Windows devices. Intune prepares Windows devices for Windows Hello for Business and enforces related device settings.

This method is most relevant when you need to:

- Prepare cloud-first Windows devices for passwordless sign-in.
- Deliver Windows Hello for Business settings during enrollment and ongoing management.
- Align Windows sign-in with device compliance and modern management.

For implementation guidance, see:

- [Windows Hello for Business overview](/windows/security/identity-protection/hello-for-business/hello-overview)
- [Passwordless strategy guide for organizations](/windows/security/identity-protection/passwordless-strategy)

### FIDO2 security keys

FIDO2 security keys provide phishing-resistant authentication using external hardware keys. Intune can help make devices ready for this method by managing supported platforms and related sign-in experiences, especially on Windows.

This method is often a good fit when organizations need:

- A portable passwordless option for shared or specialized devices.
- A strong phishing-resistant option that isn't tied to a single platform authenticator.
- A recovery or alternate path alongside platform-based credentials.

For implementation guidance, see:

- [Passwordless authentication options for Microsoft Entra ID](/entra/identity/authentication/concept-authentication-passwordless)

### Passkeys

Passkeys extend passwordless authentication across device-bound and synced credential models. From an Intune perspective, passkeys are mostly about platform and app readiness—managing the device and app prerequisites that make passkey adoption viable across platforms.

This dependency is especially important on:

- **Windows**, where platform sign-in and Windows Hello for Business can intersect with broader passwordless planning.
- **iOS/iPadOS** and **Android**, where passkeys can depend on mobile device state and app broker behavior.
- **macOS**, where platform identity integration and user sign-in experience shape adoption.

For implementation guidance, see:

- [Passwordless authentication options for Microsoft Entra ID](/entra/identity/authentication/concept-authentication-passwordless)

### Microsoft Authenticator phone sign-in

Microsoft Authenticator can provide a passwordless sign-in experience on mobile devices and act as a broker for Microsoft Entra ID authentication across apps. Intune supports this flow by deploying and managing the mobile app and device prerequisites.

In many environments, this support includes:

- Deploying Microsoft Authenticator to managed mobile devices.
- Supporting the brokered sign-in experience across Microsoft apps.
- Accounting for app protection policy considerations on mobile platforms when those are part of the broader mobile access design.

For implementation guidance, see:

- [Passwordless authentication options for Microsoft Entra ID](/entra/identity/authentication/concept-authentication-passwordless)

### Temporary Access Pass

Temporary Access Pass is a time-limited credential that helps users bootstrap or recover access before they complete their long-term passwordless setup. It isn't a permanent passwordless method, but it's often part of a successful rollout.

From an Intune perspective, Temporary Access Pass matters when you want to:

- Simplify onboarding to passwordless methods.
- Reduce reliance on temporary passwords during deployment.
- Connect onboarding scenarios to managed Windows device setup.

For implementation guidance, see:

- [Use a Temporary Access Pass](/entra/identity/authentication/howto-authentication-temporary-access-pass)
- [Overview of Windows Autopilot](/autopilot/windows-autopilot)

### Certificate-based authentication

Certificate-based authentication can also be part of a passwordless strategy, especially in regulated or specialized environments. Intune is relevant when certificate delivery, device trust, and platform configuration all need to work together.

This usually means:

- Deploying certificate profiles.
- Managing devices that consume those certificates.
- Connecting the device management layer to the identity method defined in Microsoft Entra ID.

For implementation guidance, see:

- [Passwordless authentication options for Microsoft Entra ID](/entra/identity/authentication/concept-authentication-passwordless)

## Platform considerations

Passwordless isn't one feature. It's a set of platform-specific experiences that rely on Microsoft Entra ID for identity and Microsoft Intune for device management.

### Windows

Windows is the deepest Intune-managed passwordless platform. It's the most complete example of how device enrollment, cloud sign-in, security posture, and passwordless user experience work together.

Intune commonly supports Windows passwordless scenarios by:

- Preparing cloud-first, Microsoft Entra joined devices.
- Delivering Windows Hello for Business configuration.
- Supporting FIDO2 security key experiences.
- Aligning device readiness with compliance and modern management.
- Supporting onboarding experiences that can connect to Windows Autopilot.

When a user signs in with Windows Hello or a FIDO2 key, Windows obtains a Primary Refresh Token from Entra ID. That PRT enables seamless SSO to Microsoft 365 apps, SaaS applications, and—when Cloud Kerberos Trust is configured—on-premises resources like file shares, all without additional sign-in prompts.

Related guidance:

- [Windows Hello for Business overview](/windows/security/identity-protection/hello-for-business/hello-overview)
- [Passwordless strategy guide for organizations](/windows/security/identity-protection/passwordless-strategy)
- [Overview of Windows Autopilot](/autopilot/windows-autopilot)

### macOS

On macOS, passwordless planning depends on how Microsoft Entra ID integrates with the platform sign-in and single sign-on experience. Intune delivers the device configuration needed for Apple-focused identity integrations.

With the Microsoft Enterprise SSO plug-in and Apple's Platform SSO framework (macOS 13+), Intune can deploy a configuration that allows users to sign in to the Mac using their Entra ID credentials. When configured with the Secure Enclave key method, this provides a phishing-resistant, hardware-backed sign-in experience similar to Windows Hello.

This matters when you're planning:

- Platform SSO and related sign-in experiences.
- Single sign-on between the device and Microsoft apps.
- A consistent management model alongside Windows and mobile devices.

Related guidance:

- [Microsoft Enterprise SSO plug-in and Platform SSO for Apple devices](/entra/identity-platform/apple-sso-plugin)

### iOS and iPadOS

On iOS and iPadOS, passwordless planning is more about app sign-in, brokered authentication, and passkey behavior than device sign-in. Intune deploys and manages the apps and settings that make those experiences consistent for users.

The Microsoft SSO extension on iOS can intercept authentication requests across Microsoft and third-party apps, enabling seamless sign-in after initial device setup. Microsoft Authenticator acts as the authentication broker, and can also store device-bound passkeys on iOS 17+ for phishing-resistant authentication.

Related guidance:

- [Microsoft Enterprise SSO plug-in and Platform SSO for Apple devices](/entra/identity-platform/apple-sso-plugin)
- [Passwordless authentication options for Microsoft Entra ID](/entra/identity/authentication/concept-authentication-passwordless)

### Android

On Android, Intune establishes the managed context that passwordless and brokered authentication flows depend on. This is especially relevant when Microsoft Authenticator or related app experiences are part of your mobile access design.

Both Company Portal and Microsoft Authenticator can act as authentication brokers on Android. Once a user signs in through the broker, Entra ID issues a Primary Refresh Token that enables SSO across all broker-aware apps in the work profile. On Android 14+, Authenticator can also store device-bound passkeys for phishing-resistant authentication.

Related guidance:

- [Passwordless authentication options for Microsoft Entra ID](/entra/identity/authentication/concept-authentication-passwordless)

## Benefits and outcomes

When Intune, Entra ID, and platform capabilities are used together, organizations gain:

- **Seamless single sign-on**: Users sign in once to the device and get automatic access to apps, cloud services, and—in some cases—on-premises resources. Password reset calls and repeated login prompts are eliminated.
- **User convenience across devices**: The passwordless experience is native to each platform. Windows Hello uses the OS login, macOS integrates Touch ID with Entra ID, and mobile devices use Authenticator in the background. Users don't manage different methods per device.
- **Stronger security posture**: Phishing-resistant methods prevent credential theft and replay attacks. Device compliance gating ensures that even valid credentials only work from healthy, managed devices—aligning with Zero Trust principles.
- **Reduced IT support load**: Fewer password resets, smoother onboarding with Temporary Access Pass, and self-service recovery options reduce helpdesk volume.
- **Future-ready architecture**: The framework is built to accommodate new methods like synced passkeys. As standards evolve, they integrate into the same Entra ID + Intune model without requiring architectural changes.

## Related dependencies to plan for

### Zero Trust architecture

Passwordless is one part of a broader identity and device access strategy. For an Intune administrator, that usually means planning across these layers:

- **Identity**: Phishing-resistant authentication methods in Microsoft Entra ID.
- **Device trust**: Microsoft Intune enrollment, compliance, and configuration.
- **Access policy**: Conditional Access and related exclusion planning.
- **Data protection**: Microsoft Purview capabilities that help protect content after access is granted.
- **Investigation and response**: Microsoft Defender signals and workflows when risk or compromise needs follow-up.

Related guidance:

- [What is Zero Trust?](/security/zero-trust/zero-trust-overview)
- [Common security policies for Microsoft 365 organizations](/security/zero-trust/zero-trust-identity-device-access-policies-common)

### Conditional Access

Conditional Access evaluates signals such as device state and authentication strength before granting access. When combined with passwordless methods, Conditional Access can enforce authentication strength policies that require phishing-resistant MFA—effectively mandating passwordless by blocking weaker methods like passwords or SMS codes.

When you implement Conditional Access alongside passwordless, also account for emergency access planning to prevent accidental lockout scenarios.

Related guidance:

- [Build a Conditional Access policy](/entra/identity/conditional-access/concept-conditional-access-policies)

### Compliance and device readiness

Passwordless often depends on the device being in the right state before users can rely on the experience. Readiness typically includes:

- Supported device platforms and versions.
- Device enrollment or registration.
- Required apps and brokers.
- Method-specific configuration profiles and identity prerequisites.

### Verification and ongoing operations

To validate a passwordless deployment, common checkpoints include:

- Microsoft Entra sign-in logs.
- Microsoft Intune device and policy reporting.
- Platform-specific verification experiences for the passwordless method you deploy.

## Related articles

- [Passwordless authentication options for Microsoft Entra ID](/entra/identity/authentication/concept-authentication-passwordless)
- [Windows Hello for Business overview](/windows/security/identity-protection/hello-for-business/hello-overview)
- [Passwordless strategy guide for organizations](/windows/security/identity-protection/passwordless-strategy)
- [Microsoft Enterprise SSO plug-in and Platform SSO for Apple devices](/entra/identity-platform/apple-sso-plugin)
- [Use a Temporary Access Pass](/entra/identity/authentication/howto-authentication-temporary-access-pass)
- [Overview of Windows Autopilot](/autopilot/windows-autopilot)
- [Build a Conditional Access policy](/entra/identity/conditional-access/concept-conditional-access-policies)
- [What is Zero Trust?](/security/zero-trust/zero-trust-overview)
- [Common security policies for Microsoft 365 organizations](/security/zero-trust/zero-trust-identity-device-access-policies-common)
