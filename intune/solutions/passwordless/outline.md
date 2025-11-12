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

Passwordless authentication is a cornerstone of modern identity security and a key enabler of Zero Trust. Microsoft Entra ID provides multiple passwordless options, while Microsoft Intune ensures devices are secure, compliant, and ready to use these methods. This guide explains how these technologies work together to deliver a seamless, phishing-resistant experience.

## Why passwordless matters

Passwords are vulnerable to phishing, credential stuffing, and brute-force attacks. Moving to passwordless authentication strengthens security and improves user experience. Combined with Zero Trust principles, passwordless ensures every access request is verified based on identity, device health, and risk signals.

## Microsoft passwordless approach

Microsoft's passwordless approach is built on three pillars: identity with **Microsoft Entra ID**, management through **Microsoft Intune**, and endpoint security on devices.

Together, these components deliver passwordless access aligned with **Zero Trust** principles, verifying every sign-in based on identity, device health, and contextual signals.

:::row:::
    :::column:::
#### Microsoft Entra ID

:::image type="icon" source="icons/entra.svg" border="false":::

    - Phishing-resistant credentials
    - Authentication strengths & policies
    - Conditional Access decision engine
    :::column-end:::
    :::column:::
#### Microsoft Intune

    :::image type="icon" source="icons/intune.svg" border="false":::

    - Device compliance and configuration (updates, apps, policies)
    - Security baselines
    - Risk posture signals (compliance, MTD, MAM)

    :::column-end:::
    :::column:::
#### Devices

        :::image type="icon" source="icons/devices.svg" border="false":::

- Platform authenticators (biometrics, PIN)
- Microsoft Authenticator app for mobile sign-in
- Hardware-backed security (TPM, secure enclaves)
- Optimized user experience and enrollment readiness
    :::column-end:::
:::row-end:::


---

Before diving into how Intune supports passwordless, it's important to understand key concepts around passwordless authentication, the role played by multifactor authentication (MFA), and phishing resistance.

## MFA and passwordless

MFA adds layers of security by requiring two or more factors (something you know, have, or are). Passwordless methods often satisfy MFA because they combine possession (device or key) and inherence (biometrics).

## :::image type="icon" source="icons/phishing.svg" border="false"::: Phising resistance

Phishing attacks trick users into revealing credentials or approving malicious sign-ins. Passwordless methods combined with strong multi-factor authentication (MFA) help mitigate these risks.

It's essential to understand the difference between phishing-resistant and non-phishing-resistant authentication methods when designing a passwordless strategy. A phishing-resistant method ensures that even if a user is tricked into interacting with a fraudulent prompt, the attacker cannot gain access. On the other hand, non-phishing-resistant methods can still be compromised if users are deceived into sharing secrets or approving fake requests.

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

Microsoft Entra ID supports several passwordless methods that vary in phishing resistance and use cases. Here are the primary options:

#### :::image type="icon" source="icons/passkey.svg" border="false"::: Passkeys (FIDO2)

Passkeys are cryptographic credentials that replace passwords and can sync across devices. They offer strong phishing resistance and simplify sign-in for users. Passkeys are ideal for organizations adopting modern authentication across multiple platforms. 

[!INCLUDE [intune](includes/intune.md)]
- Enforcing OS version requirements for passkey support.
- Ensuring Authenticator and Company Portal apps are installed.
- Maintaining compliance so Conditional Access allows passkey sign-in.

#### FIDO2 Security Keys

:::row:::
    :::column span="1":::
:::image type="icon" source="icons/security-key.svg" border="false":::

:::column-end:::
:::column span="5":::
FIDO2 keys are hardware-based authenticators that provide strong phishing resistance and offline capabilities. They're best suited for high-security environments or shared devices.

[!INCLUDE [intune](includes/intune.md)]

- Enabling FIDO2 sign-in via policy settings.
- Deploying FIDO2 through identity protection profiles targeting specific groups.
- Ensuring devices are compliant for passwordless access.
    :::column-end:::
:::row-end:::

#### Certificate-Based Authentication (CBA)

:::row:::
    :::column span="1":::

:::image type="icon" source="icons/certificate.svg" border="false":::
:::column-end:::
:::column span="3":::

Certificate-based authentication uses digital certificates to verify identity, commonly required in regulated industries. Because it relies on asymmetric cryptography, CBA is phishing-resistant and prevents credential replay attacks. It's widely adopted in regulated industries and government environments, often through smart cards such as PIV (Personal Identity Verification) and CAC (Common Access Card). For mobile-friendly deployments, organizations can use derived credentials (e.g., Purebred), which store certificates in secure elements on mobile devices

[!INCLUDE [intune](includes/intune.md)]

- Deploying certificates via SCEP or PKCS profiles.
- Configuring apps and devices to enforce CBA.
- Integrating with Entra ID conditional access for secure sign-in.
- Supporting Purebred workflows for mobile certificate issuance and renewal in government or high-security environments.
- Offering a cloud-based PKI option to reduce infrastructure complexity.

    :::column-end:::
:::row-end:::

#### Windows Hello for Business

:::row:::
    :::column span="1":::
:::image type="icon" source="icons/windows-hello.svg" border="false":::
:::column-end:::
:::column span="5":::
Windows Hello for Business provides a passwordless experience for Windows sign-in and organizational access. It uses a device-bound asymmetric key stored in the TPM and protected by biometrics or a PIN. This method integrates seamlessly with Entra ID and supports phishing-resistant authentication. It's ideal for managed Windows devices where users sign in locally and need strong identity assurance.

[!INCLUDE [intune](includes/intune.md)]

- Requiring Windows Hello during enrollment.
- Enforcing Hello settings (PIN complexity, biometrics allowed/disallowed).
- Prompting setup during OOBE for Entra-joined devices.
- Ensuring compliance for passwordless sign-in policies.

    :::column-end:::
:::row-end:::

#### Microsoft Authenticator app

:::row:::
    :::column span="1":::
:::image type="icon" source="icons/authenticator.svg" border="false":::
:::column-end:::
:::column span="3":::
The Microsoft Authenticator app enables passwordless sign-in on mobile devices. After entering a username, users approve the sign-in by matching a number and verifying with biometrics or PIN on their phone. While convenient and widely supported, this method is not considered phishing-resistant because it relies on push notifications rather than hardware-bound credentials. It's best suited for scenarios where flexibility and ease of use are priorities.


Microsoft Authenticator enables two passwordless approaches and one legacy MFA approach—be explicit about which you're using:

Passwordless phone sign‑in: Users approve sign‑in on the trusted device after unlocking it (biometric/PIN). Passwordless; mitigates MFA fatigue with number matching and device unlock.
Passkeys in Authenticator: Authenticator can store a FIDO‑based passkey for an Entra account. Passwordless and phishing‑resistant.
TOTP/OTP codes: One‑time codes in Authenticator. MFA but not passwordless and not phishing‑resistant; include for completeness but steer readers to the methods above.

[!INCLUDE [intune](includes/intune.md)]

- Deploying the Authenticator app.
- Enforcing device compliance.
- Applying App Protection Policies (MAM).
- Ensuring the brokered authentication flow (Company Portal/Authenticator) is present on iOS/Android.

    :::column-end:::
:::row-end:::

#### Temporary Access Pass (TAP)

:::row:::
    :::column span="1":::
:::image type="icon" source="icons/tap.svg" border="false":::
:::column-end:::
:::column span="3":::

TAP is a time-limited credential that enables onboarding or recovery without requiring a password. It's ideal for scenarios where users need initial access before setting up passwordless methods. Intune ensures devices are ready for TAP workflows and enforces compliance during onboarding.

[!INCLUDE [intune](includes/intune.md)]

- On Windows device, by enabling Web Sign-in so TAP can be used at the lock screen.
- Providing a path for passwordless onboarding by prompting Hello setup after TAP sign-in.
- Supporting fallback scenarios without compromising security.

> [!TIP]
> TAP isn't a long-term authentication method but a secure bridge to passwordless enrollment.


[!INCLUDE [learn-more](includes/learn-more.md)]
- [Use a Temporary Access Pass](/entra/identity/authentication/howto-authentication-temporary-access-pass#use-a-temporary-access-pass)
    :::column-end:::
:::row-end:::

---


For a deeper dive into these methods, refer to the [Passwordless authentication options for Microsoft Entra ID](/entra/identity/authentication/concept-authentication-passwordless).

---

<!--



Intune's role in the passwordless journey
Intune ensures devices meet compliance and configuration requirements for passwordless sign-in:


Device compliance
Enforce security baselines before enabling passwordless authentication.


Policy deployment
Configure Windows Hello for Business, Microsoft Authenticator app, and platform SSO.


Integration with Conditional Access
Provide device signals to enforce Zero Trust policies.


Lifecycle management
Keep devices updated for new passwordless capabilities and security improvements.






Aligning with Zero Trust
Passwordless authentication supports Zero Trust by:

Verifying strong identity signals.
Enforcing device health and compliance.
Reducing reliance on shared secrets.

Visual concept:
A simple diagram showing three blocks:

Microsoft Entra ID (Identity)
Microsoft Intune (Device compliance)
Conditional Access (Policy enforcement)


Implementation scenarios
Here are common solution flows:


Onboarding new devices
Use Temporary Access Pass for initial sign-in, then configure Windows Hello via Intune.


Hybrid environments
Combine FIDO2 keys with Intune compliance policies for secure access across cloud and on-premises resources.

-->



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