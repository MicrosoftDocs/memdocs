---
title: Passwordless Solutions With Microsoft Intune
description: Discover how Microsoft Intune and Entra ID work together to enable passwordless authentication across devices and platforms.
ms.date: 11/04/2025
ms.topic: concept-article
author: paolomatarazzo
ms.author: paoloma
ms.reviewer: 
---

# Passwordless solutions with Microsoft Intune

Microsoft's passwordless authentication strategy helps organizations reduce reliance on passwords—one of the most common attack vectors—by enabling secure, user-friendly sign-in experiences across platforms. This article describes how Intune and Entra ID collaborate to deliver passwordless sign-in capabilities, the supported methods, and optimizations for deployment in organizations of all sizes.

## How Microsoft's passwordless solution works

Microsoft's passwordless solution integrates Entra ID for identity and single sign-on (SSO) with Intune for device configuration and policy enforcement. This combination enables users to authenticate using strong credentials—such as biometrics, FIDO2 security keys, or passkeys—without entering passwords.

:::row:::
   :::column span="1":::
   :::image type="icon" source="icons/entra.svg" border="false":::
   :::column-end:::
   :::column span="3":::
    #### Microsoft Entra ID: Identity and token issuance
   :::column-end:::
:::row-end:::

Microsoft Entra ID is the core identity provider that verifies passwordless credentials like Windows Hello PINs, FIDO2 keys, and passkeys. Upon successful authentication, Entra ID issues a Primary Refresh Token (PRT) or equivalent, enabling seamless SSO to Microsoft 365, Azure, and other protected resources. This eliminates repeated credential prompts and supports a frictionless user experience.


:::row:::
   :::column span="1":::
   :::image type="icon" source="icons/intune.svg" border="false"::: 
   :::column-end:::
   :::column span="3":::
    #### Microsoft Intune: device management and policy enforcement
   :::column-end:::
:::row-end:::

Microsoft Intune configures passwordless sign-in policies across managed endpoints. For example:
- Enforce Windows Hello for Business on Windows devices to block password prompts during in-session authentication.
- Enable FIDO2 security key sign-in at the Windows lock screen.
- Deploy certificate-based authentication (CBA) for smart card logon.
- Deploy the Microsoft Enterprise SSO plug-in on Apple devices to support biometric authentication and Entra ID credentials.
- Guide mobile users to use the Microsoft Authenticator app or passkeys for secure sign-in.

:::row:::
   :::column span="1":::
   :::image type="icon" source="icons/devices.svg" border="false"::: 
   :::column-end:::
   :::column span="3":::
    #### Cross-platform SSO
   :::column-end:::
:::row-end:::

Passwordless authentication is supported across Windows, macOS, iOS, and Android:
- On Windows, Entra join and Intune policies enable Windows Hello or FIDO2 sign-in with instant cloud and on-premises SSO.
- On macOS, Platform SSO allows users to sign in with Entra ID credentials and gain token-based access to apps.
- On mobile, the Authenticator app acts as a broker, sharing Entra ID tokens across apps after a single biometric or passkey-based sign-in.
- On all platforms, certificate-based authentication (CBA) can be deployed for smart card logon.

[!INCLUDE [learn-more](includes/learn-more.md)]
> - [Passwordless strategy overview](https://learn.microsoft.com/windows/security/identity-protection/passwordless-strategy)
> - [Passwordless strategy overview](https://learn.microsoft.com/windows/security/identity-protection/passwordless-strategy)
> - [Passwordless strategy overview](https://learn.microsoft.com/windows/security/identity-protection/passwordless-strategy)

[!INCLUDE [learn-more](includes/learn-more.md)]
> - [Passwordless strategy overview](https://learn.microsoft.com/windows/security/identity-protection/passwordless-strategy)

## What counts as passwordless in Microsoft Entra ID?

### Phishing‑resistant methods

Phishing attacks trick users into revealing credentials or approving fraudulent sign-ins. Multi-factor authentication (MFA) reduces risk, but not all MFA methods are equally strong. Phishing-resistant MFA ensures credentials can't be intercepted or replayed, even if a user is tricked.

- Passkeys (FIDO) — this is the standards-based umbrella. In Entra you can use:
  - **Device‑bound passkeys** on platform authenticators like Windows Hello for Business and Microsoft Authenticator (iOS/Android). These are stored in secure hardware (TPM/Secure Enclave) on a single device.
  - **Synced passkeys** (multi-device) in platform password managers (e.g., iCloud Keychain, Google Password Manager) and some 3rd‑party providers—supported/rolling out per roadmap
- FIDO2 security keys — external keys (USB/NFC/BLE) that hold a FIDO credential; ideal for shared devices or high‑assurance scenarios. [643422_Phi...hods_FINAL | PowerPoint], [OA for Pas...ment Guide | Word]
Certificate‑based authentication (CBA) / smart cards (incl. PIV/CAC) — long‑standing, phishing‑resistant certificate credentials for web and native app sign‑in. [643422_Phi...hods_FINAL | PowerPoint]

### Other methods

Passwordless but typically used as a bootstrap or special case:

Temporary Access Pass (TAP): time‑limited, strong credential you issue to get a user into the system so they can register a phishing‑resistant method (great for new joiners or when a device/key was lost).

Still available, but not phishing‑resistant:

**Authenticator - phone sign‑in** (Approve on phone): remains a passwordless option, but it's not phishing‑resistant the way passkeys/FIDO/CBA are. Many orgs are moving users from phone sign‑in to passkeys.

[!INCLUDE [learn-more](includes/learn-more.md)]
> - [Passwordless strategy overview](https://learn.microsoft.com/windows/security/identity-protection/passwordless-strategy)

## Intune-Supported Passwordless Authentication Methods 

Intune supports multiple passwordless options to replace passwords with stronger, phishing-resistant credentials on managed devices. For each method, Intune plays a key role in enabling, enforcing, and managing the experience.

#### Windows Hello for Business

:::row:::
   :::column span="1":::
   :::image type="icon" source="icons/windows-hello.svg" border="false":::
   :::column-end:::
   :::column span="3":::
>Sign in with a PIN or biometrics backed by the device's TPM. Intune can require Hello during enrollment and enforce settings like PIN complexity or biometric use. Credentials never leave the device, making them highly secure.

Sign in with a PIN or biometrics backed by the device's TPM.
Intune contributes by:

Requiring Windows Hello during enrollment.
Enforcing Hello settings (PIN complexity, biometrics allowed/disallowed).
Prompting setup during OOBE for Entra-joined devices.
Ensuring compliance for passwordless sign-in policies.
Credentials never leave the device, making them highly secure.

   :::column-end:::
:::row-end:::

#### FIDO2 Security Keys

:::row:::
   :::column span="1":::
   :::image type="icon" source="icons/security-key.svg" border="false":::
   :::column-end:::
   :::column span="3":::
>External FIDO2 keys (USB, NFC) let users sign in without passwords. Intune enables this via policy and identity protection profiles. Keys are portable and ideal for shared-device scenarios.

External FIDO2 keys (USB, NFC) let users sign in without passwords.
Intune contributes by:


Enabling FIDO2 sign-in via policy settings.
Deploying FIDO2 through identity protection profiles targeting specific groups.
Ensuring devices are compliant for passwordless access.
Keys are portable and ideal for shared-device scenarios.

   :::column-end:::
:::row-end:::

#### Passkeys

:::row:::
   :::column span="1":::
   :::image type="icon" source="icons/passkey.svg" border="false":::
   :::column-end:::
   :::column span="3":::
Passkeys are FIDO2-based credentials that can sync across devices. Entra ID supports passkeys via Microsoft Authenticator (iOS 17+/Android 14+) and soon Windows 11. Intune ensures device compliance and app readiness for passkey use, enabling a seamless passwordless experience across platforms.
   
Passkeys are FIDO2-based credentials that can sync across devices. Entra ID supports passkeys via Microsoft Authenticator (iOS 17+/Android 14+) and soon Windows 11.
Intune contributes by:


Enforcing OS version requirements for passkey support.
Ensuring Authenticator and Company Portal apps are installed.
Maintaining compliance so Conditional Access allows passkey sign-in.
Passkeys enable a seamless passwordless experience across platforms.
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
Intune contributes by:


Deploying certificates via SCEP or PKCS profiles.
Configuring apps and devices to enforce CBA.
Integrating with Entra ID conditional access for secure sign-in.
Supporting Purebred workflows for mobile certificate issuance and renewal in government or high-security environments.
Ideal for regulated or high-security environments.

:::column-end:::
:::row-end:::

#### Temporary Access Pass (TAP)

:::row:::
   :::column span="1":::
   :::image type="icon" source="icons/tap.svg" border="false":::
   :::column-end:::
   :::column span="3":::
>TAP is a time-limited passcode for onboarding or recovery without passwords. Intune enables TAP on Windows by turning on Web Sign-in, allowing users to enter TAP at the login screen. After sign-in, users can set up Windows Hello, completing passwordless onboarding. TAP is short-lived and secure, reducing password dependency.

TAP is a short-lived passcode for onboarding or recovery.

Intune contributes by:

Enabling Web Sign-in on Windows devices so TAP can be used at login.
Providing a path for passwordless onboarding by prompting Hello setup after TAP sign-in.
Supporting fallback scenarios without compromising security.

   :::column-end:::
:::row-end:::

## Comparison of Key Passwordless Methods and Intune's Role 

| Method | Intune Configuration | Platforms | Description |
|--|--|--|--|
| Windows Hello for Business | Enable via Windows enrollment policy; set PIN/biometric requirements (Intune Identity Protection profile)1. Optionally hide password credential provider (Windows 11) to force Hello2 3. | Windows 10/11 (Azure AD-joined) | Passwordless sign-in using PIN or biometrics tied to TPM-backed keys. Provides two-factor auth (device + PIN/biometric) and yields SSO token on login. Intune can make Hello mandatory on devices. |
| FIDO2 Security Keys | Enable "Use security keys for sign-in" in Hello for Business settings4 or via Identity Protection profile5. Ensure Azure AD FIDO2 method is enabled tenant-wide. | Windows 10/11 (login); All platforms (web/app sign-in) | External authenticator (USB/NFC key) used instead of password. Intune allows Windows OS to accept FIDO2 at login6. Also used on web or apps via browser support on Windows, macOS, iOS, Android. Totally passwordless and phishing-resistant. |
| Temporary Access Pass | Enable "Web sign-in" credential provider via Intune policy (Settings Catalog > Authentication)7. TAP itself configured in Entra ID admin center (Authentication Methods > Temporary Access Pass). | Windows 10/11 (login); (Web sign-in also works for phone sign-in) |Time-limited passcode issued by Entra ID for one-time sign-in. Intune enables its use at Windows login8. Used for onboarding or recovery to sign in without a password and then set up a permanent method (like Hello). |
| Passkeys (Entra ID) | Ensure devices are eligible (e.g. Windows 11 22H2+, iOS 17+, Android 14+). Deploy Authenticator app via Intune on mobile; advise users on setup. No separate Intune toggle needed; enabled in Entra ID auth policy9. | All platforms (Windows, macOS, iOS, Android - in browsers or Authenticator) | Modern FIDO2 credentials that can sync across devices. E.g., Authenticator can store a passkey for an Entra account10, or a user can use an Apple iCloud passkey to log into Entra ID in Safari (public preview). Provides a convenient, strong login using device biometrics. Intune's device compliance and app config support their usage (making sure Authenticator or company portal is present for token flow). |

> (Table: Key passwordless authentication methods supported in an Intune-managed environment, with summary of how Intune configures/supports them and where they apply.) 
