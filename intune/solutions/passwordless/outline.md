---
title: Passwordless Solutions With Microsoft Intune outline
description: (Outline) Discover how Microsoft Intune and Entra ID work together to enable passwordless authentication across devices and platforms.
ms.date: 11/04/2025
ms.topic: concept-article
author: paolomatarazzo
ms.author: paoloma
ms.reviewer: 
---

# Passwordless Solutions with Microsoft Intune outline

Passwordless authentication eliminates passwords as a security risk while improving user experience. Microsoft's approach is built on three interconnected building blocks:

- Identity (Microsoft Entra ID) for strong, phishing-resistant credentials and policy enforcement
- Management (Microsoft Intune) for device compliance and configuration
- Endpoint (Devices) for secure, intuitive sign-in using platform authenticators like passkeys and FIDO2 keys

These components work together to deliver passwordless access while aligning with Zero Trust principles, ensuring every sign-in is verified based on identity, device health, and context.

:::row:::
    :::column:::
#### Microsoft Entra ID

:::image type="icon" source="icons/entra.svg" border="false":::

    - Phishing-resistant credentials (FIDO2, CBA, passkeys)
    - Authentication strengths & policies
    - Conditional Access decision engine
    :::column-end:::
    :::column:::
#### Microsoft Intune

    :::image type="icon" source="icons/intune.svg" border="false":::

    - Device compliance
    - Device configuration (updates, apps, policies)
    - Security baselines
    - Risk posture signals (compliance, MTD, MAM)

    :::column-end:::
    :::column:::
#### Devices

        :::image type="icon" source="icons/devices.svg" border="false":::

    - Platform authenticators (biometrics, PIN)
    - Microsoft Authenticator app (mobile-based sign-in)
    - Hardware-backed security (TPM, secure enclaves)
    - User experience & enrollment readiness
    :::column-end:::
:::row-end:::

[!INCLUDE [learn-more](includes/learn-more.md)]
- [Passwordless strategy overview](https://learn.microsoft.com/windows/security/identity-protection/passwordless-strategy)
- [Passwordless strategy overview](https://learn.microsoft.com/windows/security/identity-protection/passwordless-strategy)
- [Passwordless strategy overview](https://learn.microsoft.com/windows/security/identity-protection/passwordless-strategy)

---

Before diving into how Intune supports passwordless, it's important to understand key concepts around passwordless authentication, multi-factor authentication (MFA), and phishing resistance.

## MFA and passwordless

MFA adds layers of security by requiring two or more factors (something you know, have, or are). Passwordless methods often satisfy MFA because they combine possession (device or key) and inherence (biometrics).

## Phising resistance

:::row:::
    :::column span="1":::

:::image type="icon" source="icons/phishing.svg" border="false":::

:::column-end:::
:::column span="3":::
Phishing attacks trick users into revealing credentials or approving malicious sign-ins. Passwordless methods combined with strong multi-factor authentication (MFA) help mitigate these risks.

It's essential to understand the difference between phishing-resistant and non-phishing-resistant authentication methods when designing a passwordless strategy. A phishing-resistant method ensures that even if a user is tricked into interacting with a fraudulent prompt, the attacker cannot gain access. On the other hand, non-phishing-resistant methods can still be compromised if users are deceived into sharing secrets or approving fake requests.

    :::column-end:::
:::row-end:::

Some exaples include:

| Phishing-resistant Authentication  | Non-phishing-resistant Authentication  |
|-----------------------------------|---------------------------------------|
| - Windows Hello for Business<br>-Platform credential for macOS<br>FIDO2 security keys<br>- Microsoft Authenticator app passkeys<br>- Other passkeys and providers, such as iCloud Keychain<br>- Certificate-based authentication (including derived credentials like Purebred)| - SMS or voice-based codes<br>- OTP apps<br>- Push notifications without cryptographic binding |

[!INCLUDE [learn-more](includes/learn-more.md)]
- [Get started with phishing-resistant passwordless authentication deployment in Microsoft Entra ID](/entra/identity/authentication/how-to-plan-prerequisites-phishing-resistant-passwordless-authentication)

### Phishing resistance and Zero Trust

Zero Trust assumes no implicit trust—every access request must be verified. Phishing-resistant authentication is essential because:

- Strong identity assurance: Credentials cannot be intercepted or replayed, aligning with Zero Trust's principle of continuous verification.
- Prevents credential compromise: Cryptographic binding eliminates shared secrets that attackers exploit.
- Supports least privilege and conditional access: Secure identity verification enables enforcement of device compliance and risk-based policies.

Without phishing resistance, attackers can bypass MFA through social engineering or prompt bombing, undermining Zero Trust protections.

[!INCLUDE [learn-more](includes/learn-more.md)]
> - [What is Zero Trust?](/en-us/security/zero-trust/zero-trust-overview)

## Passwordless Authentication Methods in Microsoft Entra ID

Before exploring Intune's role, it's important to understand the passwordless authentication methods supported by Microsoft Entra ID. Let's briefly review them.

#### Passkeys (FIDO2)
:::row:::
    :::column span="1":::
:::image type="icon" source="icons/passkey.svg" border="false":::
:::column-end:::
:::column span="3":::
Passkeys are phishing-resistant credentials built on the FIDO2 and WebAuthn standards. They replace passwords with asymmetric key pairs generated on a secure device, ensuring that private keys never leave the authenticator. Users can sign in by unlocking the passkey with a biometric or PIN gesture, eliminating risks like credential theft and replay attacks. Entra ID currently supports device-bound passkeys, with future plans for syncable passkeys across devices.\
 Passkeys are FIDO2-based credentials that can sync across devices. Entra ID supports passkeys via Microsoft Authenticator (iOS 17+/Android 14+).

- Passkeys (FIDO) — this is the standards-based umbrella. In Entra you can use:
  - **Device‑bound passkeys** on platform authenticators like Windows Hello for Business and Microsoft Authenticator (iOS/Android). These are stored in secure hardware (TPM/Secure Enclave) on a single device.
  - **Synced passkeys** (multi-device) in platform password managers (e.g., iCloud Keychain, Google Password Manager)

[!INCLUDE [intune](includes/intune.md)]
- Enforcing OS version requirements for passkey support.
- Ensuring Authenticator and Company Portal apps are installed.
- Maintaining compliance so Conditional Access allows passkey sign-in.
- Ensuring device compliance and app readiness for passkey use, enabling a seamless passwordless experience across platforms.

    :::column-end:::
:::row-end:::

#### FIDO2 Security Keys

:::row:::
    :::column span="1":::
:::image type="icon" source="icons/security-key.svg" border="false":::

:::column-end:::
:::column span="3":::
FIDO2 security keys are external hardware authenticators that provide phishing-resistant passwordless sign-in. These keys store private keys in a secure enclave and require a user gesture (touch, PIN, or biometric) to complete authentication. They work across platforms and are ideal for high-security environments or shared workstation scenarios where platform authenticators like indows Hello aren't practical.

External keys (USB/NFC/BLE) that hold a FIDO credential; ideal for shared devices or high‑assurance scenarios.
External FIDO2 keys (USB, NFC) let users sign in without passwords. Intune enables this via policy and identity protection profiles. Keys are portable and ideal for shared-device scenarios.

External FIDO2 keys (USB, NFC) let users sign in without passwords.
[!INCLUDE [intune](includes/intune.md)]

- Enabling FIDO2 sign-in via policy settings.
- Deploying FIDO2 through identity protection profiles targeting specific groups.
- Ensuring devices are compliant for passwordless access.
- Keys are portable and ideal for shared-device scenarios.
    :::column-end:::
:::row-end:::

#### Certificate-Based Authentication (CBA)

:::row:::
    :::column span="1":::

:::image type="icon" source="icons/certificate.svg" border="false":::
:::column-end:::
:::column span="3":::

CBA uses X.509 certificates to authenticate users without passwords. Intune can deploy certificates via SCEP or PKCS profiles and enforce CBA for apps and device sign-in. This method is ideal for high-security environments and integrates with Entra ID conditional access for strong, phishing-resistant authentication.

CBA uses X.509 certificates for strong, passwordless authentication.

[!INCLUDE [intune](includes/intune.md)]

- Deploying certificates via SCEP or PKCS profiles.
- Configuring apps and devices to enforce CBA.
- Integrating with Entra ID conditional access for secure sign-in.
- Supporting Purebred workflows for mobile certificate issuance and renewal in government or high-security environments.
- Ideal for regulated or high-security environments.

Certificate-based authentication uses X.509 certificates issued by a trusted PKI to authenticate users without passwords. It's widely adopted in regulated industries and government environments, often through smart cards (PIV/CAC). CBA provides strong identity assurance and integrates with Entra ID for single sign-on, but requires PKI infrastructure and careful lifecycle management of certificates.
- Certificate‑based authentication (CBA) / smart cards (incl. PIV/CAC) — long‑standing, phishing‑resistant certificate credentials for web and native app sign‑in.
- Derived credentials (Purebred) — mobile‑friendly CBA alternative that stores certs in secure elements on mobile devices.
    :::column-end:::
:::row-end:::

#### Windows Hello for Business

:::row:::
    :::column span="1":::
:::image type="icon" source="icons/authenticator.svg" border="false":::
:::column-end:::
:::column span="3":::
Windows Hello for Business provides a passwordless experience for Windows sign-in and organizational access. It uses a device-bound asymmetric key stored in the TPM and protected by biometrics or a PIN. This method integrates seamlessly with Entra ID and supports phishing-resistant authentication. It's ideal for managed Windows devices where users sign in locally and need strong identity assurance.

Sign in with a PIN or biometrics backed by the device's TPM. Intune can require Hello during enrollment and enforce settings like PIN complexity or biometric use. Credentials never leave the device, making them highly secure.

Sign in with a PIN or biometrics backed by the device's TPM.

[!INCLUDE [intune](includes/intune.md)]

- Requiring Windows Hello during enrollment.
- Enforcing Hello settings (PIN complexity, biometrics allowed/disallowed).
- Prompting setup during OOBE for Entra-joined devices.
- Ensuring compliance for passwordless sign-in policies.
- Credentials never leave the device, making them highly secure.

    :::column-end:::
:::row-end:::

#### Microsoft Authenticator app

:::row:::
    :::column span="1":::
:::image type="icon" source="icons/authenticator.svg" border="false":::
:::column-end:::
:::column span="3":::
The Microsoft Authenticator app enables passwordless sign-in on mobile devices. After entering a username, users approve the sign-in by matching a number and verifying with biometrics or PIN on their phone. While convenient and widely supported, this method is not considered phishing-resistant because it relies on push notifications rather than hardware-bound credentials. It's best suited for scenarios where flexibility and ease of use are priorities.
    :::column-end:::
:::row-end:::

#### Temporary Access Pass (TAP)

:::row:::
    :::column span="1":::
:::image type="icon" source="icons/tap.svg" border="false":::
:::column-end:::
:::column span="3":::

TAP is a time-limited passcode for onboarding or recovery without passwords. Intune enables TAP on Windows by turning on Web Sign-in, allowing users to enter TAP at the login screen. After sign-in, users can set up Windows Hello, completing passwordless onboarding. TAP is short-lived and secure, reducing password dependency.

TAP is a short-lived passcode for onboarding or recovery.

Intune contributes by:

- Enabling Web Sign-in on Windows devices so TAP can be used at login.
- Providing a path for passwordless onboarding by prompting Hello setup after TAP sign-in.
- Supporting fallback scenarios without compromising security.

A Temporary Access Pass is a time-limited passcode that helps bootstrap passwordless methods or recover access when primary credentials are unavailable. TAP can be configured for single use or multiple sign-ins and is particularly useful for onboarding new users or setting up Windows Hello for Business without requiring a password. It's not a long-term authentication method but a secure bridge to passwordless enrollment.
>
>[!INCLUDE [learn-more](includes/learn-more.md)]
>- [Use a Temporary Access Pass](/entra/identity/authentication/howto-authentication-temporary-access-pass#use-a-temporary-access-pass)
    :::column-end:::
:::row-end:::

### Other Options

Clarify OTP in Authenticator and transitional use cases.

---


For a deeper dive into these methods, refer to the [Passwordless authentication options for Microsoft Entra ID](/entra/identity/authentication/concept-authentication-passwordless).

Now that we have the foundational concepts covered, let's explore how Microsoft Intune plays a critical role in enabling and managing passwordless authentication across devices.



## Passwordless options in Intune and Entra

Intune ensures devices meet security baselines, are updated to support the latest passwordless innovations, and are configured for seamless sign-in experiences. For example:

- Configure device update policies to ensure the latest security features are available.
- Deploy policy settings to enable and enforce passwordless sign-in methods. For example, Windows devices can be configured with Windows Hello for Business policies, while macOS devices can be set up to use platform credentials integrated with Entra ID. 
- Configure certificate profiles for smart cards or derived credentials.
- Enforce compliance policies to ensure only secure, healthy devices can access resources.

## Intune's Role in the Passwordless Journey

This is the core section—make it actionable and Intune-centric.

### Device Compliance and Security

- Ensure OS updates and patching.
- Enforce lock screen policies.
- Integrate with Mobile Threat Defense (MTD).
- Apply Mobile App Management (MAM).

### Configuration for Passwordless Enablement

- Deploy **Windows Hello for Business** via Intune.
- Configure **FIDO2 key policies**.
- Integrate with **Conditional Access**.
- Support **TAP enrollment workflows**.

Include policy examples and actionable steps.

> **Learn more:**  
- [Passwordless experience in Windows](https://learn.microsoft.com/windows/security/identity-protection/passwordless-experience)  
- [Intune enrollment and MFA](https://learn.microsoft.com/mem/intune/enrollment/multi-factor-authentication)

---

## Device Readiness and User Experience

Cover technical and human aspects:
- How devices must be configured for passwordless.
- Educating users on new sign-in flows.
- Handling exceptions (shared devices, legacy apps).

> **Learn more:** [Add your work or school account to a Windows device](https://support.microsoft.com/en-us/account)

---

## Operational Considerations
### Monitoring and Reporting
How to track passwordless adoption in Intune and Entra.

### Troubleshooting
Common issues like TPM problems, credential recovery, and OOBE failures.

> **Learn more:** [Troubleshoot Microsoft Authenticator](https://support.microsoft.com/en-us/account)

---

## Security and Zero Trust Alignment
Explicitly map passwordless strategies to Zero Trust principles:
- **Verify explicitly** – Strong authentication methods.
- **Use least privilege** – Conditional Access policies.
- **Assume breach** – Continuous monitoring and anomaly detection.

---

## Conclusion
Summarize benefits, reiterate Intune's role, and link to next steps or resources.

---

### Links to review

[!INCLUDE [learn-more](includes/learn-more.md)]
- [Single sign-on (SSO) overview and options for Apple devices in Microsoft Intune](../../intune-service/configuration/use-enterprise-sso-plug-in-ios-ipados-macos.md)
- [Passwordless for Students](/microsoft-365/education/deploy/protect-passwordless-students)
- [App Protection Policies Overview](../../intune-service/apps/app-protection-policy.md)