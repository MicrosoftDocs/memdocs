---
# required metadata

title: Configure wired network settings for Windows devices in Microsoft Intune
titleSuffix:
description: Create or add a wired network device configuration profile for Windows 10/11 devices. See the different settings, add certificates, choose an EAP type, and select an authentication method in Microsoft Intune. 
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/18/2022
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: tycast, ochukwunyere
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Add wired network settings for Windows devices in Microsoft Intune

You can create a profile with specific wired network settings, and then deploy this profile to your Windows devices. Microsoft Intune offers many features, including authenticating to your network, adding a SCEP certificate, and more.

This article describes the settings you can configure.

## Before you begin

Create a [wired network device configuration profile](wired-networks-configure.md).

> [!NOTE]
> These settings are available for all enrollment types. For more information on the enrollment types, see [Set up enrollment for Windows devices](../enrollment/windows-enroll.md).

OUSTANDING ??
- Not configured: By default, the OS might ??
- If you leave this value empty or blank,
- What CSP? [WiredNetwork CSP](/windows/client-management/mdm/wirednetwork-csp)

## Wired Network

- **Authentication method**: Select how the profile authenticates with the network server ??what server??. If you’re using certificate authentication, make sure the certificate type matches the authentication type.

  Your options:

  - **Not configured** (default): Intune doesn't change or update this setting. By default, the OS might use **User or machine** authentication.
  - **User**: The user account signed in to the device authenticates to the network.
  - **Machine**: Device credentials authenticate to the network.
  - **User or machine**: When a user is signed in to the device, user credentials authenticate to the network. When no users are signed in, then device credentials authenticate.
  - **Guest**: No credentials are associated with the network. Authentication is either open, or handled externally, such as through a web page.

- **Remember credentials at each logon**: Select to cache user credentials, or if users must enter them every time when connecting to the network. Your options:

  - **Not configured**: Intune doesn't change or update this setting. By default, the OS might enable this feature, and cache the credentials.
  - **Enable**: Caches user credentials when entered the first time users connect to the network. Cached credentials are used for future connections, and users don't need to reenter them.
  - **Disable**: User credentials aren't remembered or cached. When connecting to the network, users must enter their credentials every time.

- **Authentication period**: Enter the number of seconds devices must wait after trying to authenticate, from 1-3600. If the device doesn't connect in the time you enter, then authentication fails. If you leave this value empty or blank, then `18` seconds is used.

- **Authentication retry delay period**: Enter the number of seconds between a failed authentication attempt and the next authentication attempt, from 1-3600. If you leave this value empty or blank, then `1` second is used.

- **Start period**: Enter the number of seconds to wait before sending an EAPOL-Start message, from 1-3600. If you leave this value empty or blank, then `5` seconds is used.

- **Maximum EAPOL-start**: Enter the number of EAPOL-Start messages, from 1 and 100. If you leave this value empty or blank, then a maximum of `3` messages are sent.

- **Maximum authentication failures**: Enter the maximum number of authentication failures for this set of credentials to authenticate, from 1-100. If you leave this value empty or blank, then `1` attempt is used.

- **802.1x**: When set to **Enforce**, the automatic configuration service for wired networks (Wired AutoConfig) requires using 802.1X for port authentication. When set to **Do not enforce** (default), the Wired AutoConfig service doesn't require using 802.1X for port authentication.

- **Block period (minutes)**: After a failed authentication attempt, the OS automatically tries to authenticate again. Enter the number of minutes to block these automatic authentication attempts, from 0-1440. If you leave this value empty or blank, then the OS automatically tries to authenticate again. ??does it eventually stop, or just keeps retrying forever??

- **EAP type**: Select the Extensible Authentication Protocol (EAP) type to authenticate secured wired connections. Your options:

  - **EAP-SIM**

  - **EAP-TLS**: Also enter:

    - **Server Trust** - **Certificate server names**: Enter one or more common names used in the certificates issued by your trusted certificate authority (CA). When you enter this information, you can bypass the dynamic trust window shown on user devices when they connect to this network.
    - **Root certificate for server validation**: Select an existing trusted root certificate profile. When the client connects to the network, this certificate is presented to the server ??what server??. This certificate authenticates the connection.
    - **Client Authentication** - **Authentication method**: Select the authentication method used by your device clients. Your options:
      - **SCEP certificate**: Select the SCEP client certificate profile that's also deployed to the device. This certificate is the identity presented by the device to the server ??What server?? to authenticate the connection. PKCS certificates aren't supported.
      - **PKCS certificate**: Select the PKCS **client certificate** profile and trusted **root certificate** that are also deployed to the device. The client certificate is the identity presented by the device to the server ??what server?? to authenticate the connection.
      - **PFX Import certificate**: Select the imported PFX certificate profile. The client certificate is the identity presented by the device to authenticate the connection. For more information on imported PFX certificates, see [Configure and use imported PKCS certificates with Intune](/protect/certificates-imported-pfx-configure).
      - **Derived credential**: Use a certificate that's derived from a user's smart card. For more information, see [Use derived credentials in Microsoft Intune](../protect/derived-credentials.md).

  - **EAP-TTLS**: Also enter:

    - **Server Trust** - **Certificate server names**: Enter one or more common names used in the certificates issued by your trusted certificate authority (CA). If you enter this information, you can bypass the dynamic trust dialog shown on user devices when they connect to this network.
    - **Root certificates for server validation**: Select the trusted root certificate profile used to authenticate the network connection.
    - **Client Authentication** - **Authentication method**: Select the authentication method used by your device clients. Your options:

      - **Username and Password**: Prompt the user for a user name and password to authenticate the network connection. Also enter:
        - **Non-EAP method (inner identity)**: Choose how you authenticate the network connection. Be sure you select the same protocol that's configured on your network.

          Your options: **Unencrypted password (PAP)**, **Challenge Handshake (CHAP)**, **Microsoft CHAP (MS-CHAP)**, and **Microsoft CHAP Version 2 (MS-CHAP v2)**

        - **Identity privacy (outer identity)**: Enter the text sent in response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent, and then followed by the real identification sent in a secure tunnel.

      - **SCEP certificate**: Select the SCEP client certificate profile that's also deployed to the device. This certificate is the identity presented by the device to authenticate the network connection.

        - **Identity privacy (outer identity)**: Enter the text sent in response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent, and then followed by the real identification sent in a secure tunnel.

      - **PKCS certificate**: Select the PKCS **client certificate** profile and trusted **root certificate** that are also deployed to the device. The client certificate is the identity presented by the device to authenticate the network connection.

        - **Identity privacy (outer identity)**: Enter the text sent in response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent, and then followed by the real identification sent in a secure tunnel.

      - **PFX Import certificate**: Select the imported PFX certificate profile. The client certificate is the identity presented by the device to authenticate the network connection. For more information on imported PFX certificates, see [Configure and use imported PKCS certificates with Intune](/protect/certificates-imported-pfx-configure).

        - **Identity privacy (outer identity)**: Enter the text sent in response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent, and then followed by the real identification sent in a secure tunnel.

      - **Derived credential**: Use a certificate that's derived from a user's smart card. For more information, see [Use derived credentials in Microsoft Intune](../protect/derived-credentials.md).

  - **Protected EAP (PEAP)**: Also enter:

    - **Server trust** - **Certificate server names**: Enter one or more common names used in the certificates issued by your trusted certificate authority (CA). If you enter this information, you can bypass the dynamic trust dialog shown on user devices when they connect to this network.  

    - **Root certificate for server validation**: Select the trusted root certificate profile used to authenticate the network connection.  

    - **Perform server validation**: When set to **Yes**, in PEAP negotiation phase 1, devices validate the certificate, and verify the server. Select **No** to block or prevent this validation. When set to **Not configured**, Intune doesn't change or update this setting.

      If you select **Yes**, also configure:

      - **Disable user prompts for server validation**: When set to **Yes**, in PEAP negotiation phase 1, user prompts asking to authorize new PEAP servers for trusted certification authorities aren't shown. Select **No** to show the prompts. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might ??

    - **Require cryptographic binding**: **Yes** prevents connections to PEAP servers that don't use cryptobinding during the PEAP negotiation. **No** doesn't require cryptobinding. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might ??

    - **Client Authentication** - **Authentication method**: Select the authentication method used by your device clients. Your options:

      - **Username and Password**: Prompt the user for a user name and password to authenticate the network connection. Also enter:

        - **Identity privacy (outer identity)**: Enter the text sent in response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent, and then followed by the real identification sent in a secure tunnel.

      - **SCEP certificate**: Select the SCEP **client certificate** profile that is also deployed to the device. This certificate is the identity presented by the device to the server to authenticate the network connection.

        - **Identity privacy (outer identity)**: Enter the text sent in response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent, and then followed by the real identification sent in a secure tunnel.

      - **PKCS certificate**: Select the PKCS **client certificate** profile and trusted **root certificate** that are also deployed to the device. The client certificate is the identity presented by the device to the server ??what server?? to authenticate the network connection.

        - **Identity privacy (outer identity)**: Enter the text sent in response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent, and then followed by the real identification sent in a secure tunnel.

      - **PFX Import certificate**: Select the imported PFX certificate profile. The client certificate is the identity presented by the device to authenticate the network connection. For more information on imported PFX certificates, see [Configure and use imported PKCS certificates with Intune](/protect/certificates-imported-pfx-configure).

        - **Identity privacy (outer identity)**: Enter the text sent in response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent, and then followed by the real identification sent in a secure tunnel.

      - **Derived credential**: Use a certificate that's derived from a user's smart card. For more information, see [Use derived credentials in Microsoft Intune](../protect/derived-credentials.md).

## Next steps

The profile is created, but it may not be doing anything. Be sure to [assign this profile](device-profile-assign.md), and [monitor its status](device-profile-monitor.md).
