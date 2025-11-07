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
> - [Passwordless strategy overview](https://learn.microsoft.com/windows/security/identity-protection/passwordless-strategy)
> - [Passwordless strategy overview](https://learn.microsoft.com/windows/security/identity-protection/passwordless-strategy)
> - [Passwordless strategy overview](https://learn.microsoft.com/windows/security/identity-protection/passwordless-strategy)

---

Before diving into how Intune supports passwordless, it's important to understand key concepts around passwordless authentication, multi-factor authentication (MFA), and phishing resistance.

## MFA and passwordless

MFA adds layers of security by requiring two or more factors (something you know, have, or are). Passwordless methods often satisfy MFA because they combine possession (device or key) and inherence (biometrics).

:::row:::
    :::column span="1":::
## Phising resistance

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
> - [Get started with phishing-resistant passwordless authentication deployment in Microsoft Entra ID](/entra/identity/authentication/how-to-plan-prerequisites-phishing-resistant-passwordless-authentication)

### Phishing resistance and Zero Trust

Zero Trust assumes no implicit trust—every access request must be verified. Phishing-resistant authentication is essential because:

- Strong identity assurance: Credentials cannot be intercepted or replayed, aligning with Zero Trust's principle of continuous verification.
- Prevents credential compromise: Cryptographic binding eliminates shared secrets that attackers exploit.
- Supports least privilege and conditional access: Secure identity verification enables enforcement of device compliance and risk-based policies.

Without phishing resistance, attackers can bypass MFA through social engineering or prompt bombing, undermining Zero Trust protections.

[!INCLUDE [learn-more](includes/learn-more.md)]
> - [What is Zero Trust?](/en-us/security/zero-trust/zero-trust-overview)

## Passwordless Authentication Methods in Microsoft Entra ID

Let's explore the main passwordless authentication methods supported by Microsoft Entra ID, highlighting their phishing resistance and use cases.

:::row:::
    :::column span="1":::
### Passkeys
:::image type="icon" source="icons/passkey.svg" border="false":::
:::column-end:::
:::column span="3":::
- Passkeys (FIDO) — this is the standards-based umbrella. In Entra you can use:
  - **Device‑bound passkeys** on platform authenticators like Windows Hello for Business and Microsoft Authenticator (iOS/Android). These are stored in secure hardware (TPM/Secure Enclave) on a single device.
  - **Synced passkeys** (multi-device) in platform password managers (e.g., iCloud Keychain, Google Password Manager)
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
### FIDO2 Security Keys
:::image type="icon" source="icons/security-key.svg" border="false":::
:::column-end:::
:::column span="3":::
External keys (USB/NFC/BLE) that hold a FIDO credential; ideal for shared devices or high‑assurance scenarios.
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
### Certificate-Based Authentication (CBA)
:::image type="icon" source="icons/certificate.svg" border="false":::
:::column-end:::
:::column span="3":::
- Certificate‑based authentication (CBA) / smart cards (incl. PIV/CAC) — long‑standing, phishing‑resistant certificate credentials for web and native app sign‑in.
- Derived credentials (Purebred) — mobile‑friendly CBA alternative that stores certs in secure elements on mobile devices.
    :::column-end:::
:::row-end:::

:::row:::
    :::column span="1":::
### Temporary Access Pass (TAP)
:::image type="icon" source="icons/tap.svg" border="false":::
:::column-end:::
:::column span="3":::
Used for bootstrap during initial passwordless setup.
    :::column-end:::
:::row-end:::

### Other Options

Clarify OTP in Authenticator and transitional use cases.

---

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