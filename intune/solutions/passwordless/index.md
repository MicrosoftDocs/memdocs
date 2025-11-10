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
- [Passwordless strategy overview](https://learn.microsoft.com/windows/security/identity-protection/passwordless-strategy)

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
- [Passwordless strategy overview](https://learn.microsoft.com/windows/security/identity-protection/passwordless-strategy)



