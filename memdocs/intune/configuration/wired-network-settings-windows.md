---
# required metadata

title: Configure wired network settings for Windows devices in Microsoft Intune
titleSuffix:
description: Create or add a wired network device configuration profile for Windows 10/11 devices. See the different settings, add certificates, choose an EAP type, and select an authentication method in Microsoft Intune. 
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/25/2024
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: abalwan
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier3
- M365-identity-device-management
---

# Add wired network settings for Windows devices in Microsoft Intune

You can create a profile with specific wired network settings, and then deploy this profile to your Windows devices. For example, you can authenticate to your network, add a Simple Certificate Enrollment Protocol (SCEP) certificate, and more.

This article describes the settings you can configure.

This feature applies to:

- Windows 11
- Windows 10

## Before you begin

- Create a [wired network device configuration profile](wired-networks-configure.md).

- These settings are available for all enrollment types. For more information on the enrollment types, go to [Set up enrollment for Windows devices](../enrollment/windows-enroll.md).

- These settings use the [WiredNetwork CSP](/windows/client-management/mdm/wirednetwork-csp).

## Wired Network

- **Authentication mode**: Select how the profile authenticates with the network. If you're using certificate authentication, make sure the certificate type matches the authentication type.

  Your options:

  - **Not configured** (default): Intune doesn't change or update this setting. By default, the OS might use **User or machine** authentication.
  - **User**: The user account signed in to the device authenticates to the network.
  - **Machine**: Device credentials authenticate to the network.
  - **User or machine**: When a user is signed in to the device, user credentials authenticate to the network. When no users are signed in, then device credentials authenticate.
  - **Guest**: No credentials are associated with the network. Authentication is either open, or handled externally, such as through a web page.

- **Remember credentials at each logon**: Select to cache user credentials, or if users must enter them every time when connecting to the network. Your options:

  - **Not configured**: Intune doesn't change or update this setting. By default, the OS might enable this feature, and cache the credentials.
  - **Enable**: Caches user credentials when entered the first time users connect to the network. Cached credentials are used for future connections, and users don't need to reenter them.
  - **Disable**: User credentials aren't remembered or cached. When users connect to the network, users must enter their credentials every time.

- **Authentication period**: Enter the number of seconds devices must wait after trying to authenticate, from 1-3600. If the device doesn't connect in the time you enter, then authentication fails. If you leave this value empty or blank, then `18` seconds are used.

- **Authentication retry delay period**: Enter the number of seconds between a failed authentication attempt and the next authentication attempt, from 1-3600. If you leave this value empty or blank, then `1` second is used.

- **Start period**: Enter the number of seconds to wait before sending an EAPOL-Start message, from 1-3600. If you leave this value empty or blank, then `5` seconds are used.

- **Maximum EAPOL-start**: Enter the number of EAPOL-Start messages, from 1 and 100. If you leave this value empty or blank, then a maximum of `3` messages are sent.

- **Maximum authentication failures**: Enter the maximum number of authentication failures for this set of credentials to authenticate, from 1-100. If you leave this value empty or blank, then `1` attempt is used.

- **802.1x**: When set to **Enforce**, the automatic configuration service for wired networks (Wired AutoConfig) requires using 802.1X for port authentication. When set to **Do not enforce** (default), the Wired AutoConfig service doesn't require using 802.1X for port authentication.

  > [!WARNING]
  > When set to **Enforce**, make sure your configuration settings in the policy are correct and match your network settings. If the policy settings don't match your network settings, then internet access is blocked on the device. The device can't connect to the internet to get an updated policy version. To get internet access again, you have to manually remove the policy from the device.

- **Block period (minutes)**: After a failed authentication attempt, the OS automatically tries to authenticate again. Enter the number of minutes to block these automatic authentication attempts, from 0-1440. If you leave this value empty or blank, then the OS might automatically try to authenticate again.

- **EAP type**: To authenticate secured wired connections, select the Extensible Authentication Protocol (EAP) type. Your options:

  - **EAP-SIM**

  - **EAP-TLS**: Also enter:

    - **Server Trust** - **Certificate server names**: Enter one or more common names used in the certificates issued by your trusted certificate authority (CA). When you enter this information, you can bypass the dynamic trust window shown on user devices when they connect to this network.
    - **Root certificate for server validation**: Select one or more existing trusted root certificate profiles. When the client connects to the network, these certificates are used to establish a chain of trust with the server. If your authentication server uses a public certificate, then you don't need to include a root certificate.
    - **Client Authentication** - **Authentication method**: Select the authentication method used by your device clients. Your options:
      - **SCEP certificate**: Select an existing SCEP client certificate profile that is also deployed to the device. This certificate is the identity presented by the device to the server to authenticate the connection.
      - **PKCS certificate**: Select an existing Public Key Cryptography Standards (PKCS) **client certificate** profile and existing trusted **root certificate** that are also deployed to the device. The client certificate is the identity presented by the device to the server to authenticate the connection.
      - **PFX Import certificate**: Select an existing imported PFX certificate profile. The client certificate is the identity presented by the device to authenticate the connection.

        For more information on imported PFX certificates, go to [Configure and use imported PKCS certificates with Intune](../protect/certificates-imported-pfx-configure.md).

      - **Derived credential**: Select an existing certificate profile that is derived from a user's smart card. For more information, go to [Use derived credentials in Microsoft Intune](../protect/derived-credentials.md).

  - **EAP-TTLS**: Also enter:

    - **Server Trust** - **Certificate server names**: Enter one or more common names used in the certificates issued by your trusted certificate authority (CA). If you enter this information, you can bypass the dynamic trust dialog shown on user devices when they connect to this network.
    - **Root certificates for server validation**: Select one or more existing trusted root certificate profiles. When the client connects to the network, these certificates are used to establish a chain of trust with the server. If your authentication server uses a public certificate, then you don't need to include a root certificate.
    - **Client Authentication** - **Authentication method**: Select the authentication method used by your device clients. Your options:

      - **Username and Password**: Prompt the user for a user name and password to authenticate the network connection. Also enter:
        - **Non-EAP method (inner identity)**: Choose how to authenticate the network connection. Be sure you select the same protocol that is configured on your network.

          Your options: **Unencrypted password (PAP)**, **Challenge Handshake (CHAP)**, **Microsoft CHAP (MS-CHAP)**, or **Microsoft CHAP Version 2 (MS-CHAP v2)**

        - **Identity privacy (outer identity)**: Enter the text sent in response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent. Then, the real identification is sent in a secure tunnel.

      - **SCEP certificate**: Select an existing SCEP client certificate profile that is also deployed to the device. This certificate is the identity presented by the device to authenticate the network connection.

        - **Identity privacy (outer identity)**: Enter the text sent in response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent. Then, the real identification is sent in a secure tunnel.

      - **PKCS certificate**: Select an existing PKCS **client certificate** profile and existing trusted **root certificate** that are also deployed to the device. The client certificate is the identity presented by the device to authenticate the network connection.

        - **Identity privacy (outer identity)**: Enter the text sent in response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent. Then, the real identification is sent in a secure tunnel.

      - **PFX Import certificate**: Select an existing imported PFX certificate profile. The client certificate is the identity presented by the device to authenticate the network connection.

        For more information on imported PFX certificates, go to [Configure and use imported PKCS certificates with Intune](../protect/certificates-imported-pfx-configure.md).

        - **Identity privacy (outer identity)**: Enter the text sent in response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent. Then, the real identification is sent in a secure tunnel.

      - **Derived credential**: Select an existing certificate profile that is derived from a user's smart card. For more information, go to [Use derived credentials in Microsoft Intune](../protect/derived-credentials.md).

  - **Protected EAP (PEAP)**: Also enter:

    - **Server trust** - **Certificate server names**: Enter one or more common names used in the certificates issued by your trusted certificate authority (CA). If you enter this information, you can bypass the dynamic trust dialog shown on user devices when they connect to this network.  

    - **Root certificate for server validation**: Select one or more existing trusted root certificate profiles. When the client connects to the network, these certificates are used to establish a chain of trust with the server. If your authentication server uses a public certificate, then you don't need to include a root certificate.  

    - **Perform server validation**: When set to **Yes**, in PEAP negotiation phase 1, devices validate the certificate, and verify the server. Select **No** to block or prevent this validation. When set to **Not configured**, Intune doesn't change or update this setting.

      If you select **Yes**, also configure:

      - **Disable user prompts for server validation**: When set to **Yes**, in PEAP negotiation phase 1, user prompts asking to authorize new PEAP servers for trusted certification authorities aren't shown. Select **No** to show the prompts. When set to **Not configured** (default), Intune doesn't change or update this setting.

    - **Require cryptographic binding**: **Yes** prevents connections to PEAP servers that don't use cryptobinding during the PEAP negotiation. **No** doesn't require cryptobinding. When set to **Not configured** (default), Intune doesn't change or update this setting.

    - **Client Authentication** - **Authentication method**: Select the authentication method used by your device clients. Your options:

      - **Username and Password**: Prompt the user for a user name and password to authenticate the network connection. Also enter:

        - **Identity privacy (outer identity)**: Enter the text sent in response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent. Then, the real identification is sent in a secure tunnel.

      - **SCEP certificate**: Select an existing SCEP **client certificate** profile that is also deployed to the device. This certificate is the identity presented by the device to the server to authenticate the network connection.

        - **Identity privacy (outer identity)**: Enter the text sent in response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent. Then, the real identification is sent in a secure tunnel.

      - **PKCS certificate**: Select an existing PKCS **client certificate** profile and existing trusted **root certificate** that are also deployed to the device. The client certificate is the identity presented by the device to the server to authenticate the network connection.

        - **Identity privacy (outer identity)**: Enter the text sent in response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent. Then, the real identification is sent in a secure tunnel.

      - **PFX Import certificate**: Select an existing imported PFX certificate profile. The client certificate is the identity presented by the device to authenticate the network connection.

        For more information on imported PFX certificates, go to [Configure and use imported PKCS certificates with Intune](../protect/certificates-imported-pfx-configure.md).

        - **Identity privacy (outer identity)**: Enter the text sent in response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent. Then, the real identification is sent in a secure tunnel.

      - **Derived credential**: Select an existing certificate profile that is derived from a user's smart card. For more information, go to [Use derived credentials in Microsoft Intune](../protect/derived-credentials.md).

  - **Tunnel EAP (TEAP)**: Also enter:

    - **Server trust** - **Certificate server names**: Enter one or more common names used in the certificates issued by your trusted certificate authority (CA). If you enter this information, you can bypass the dynamic trust dialog shown on user devices when they connect to this network.  

    - **Client Authentication** - **Primary authentication method**: Select the primary authentication method used by your device clients for user authentication. This authentication method is the identity certificate that the device presents to the server.

      Your options:

      - **Username and Password**: Prompt the user for a user name and password to authenticate the network connection.

      - **SCEP certificate**: Select an existing SCEP **client certificate** profile that is also deployed to the device. This certificate is the identity presented by the device to the server to authenticate the network connection.

      - **PKCS certificate**: Select an existing PKCS **client certificate** profile and existing trusted **root certificate** that are also deployed to the device. The client certificate is the identity presented by the device to the server to authenticate the network connection.

      - **Derived credential**: Select an existing certificate profile that is derived from a user's smart card. For more information, go to [Use derived credentials in Microsoft Intune](../protect/derived-credentials.md).

    - **Client Authentication** - **Secondary authentication method**: Select the secondary authentication method used by your device clients for machine authentication. This authentication method is the identity certificate that the device presents to the server.

      If the **Primary authentication method** fails, then the **Secondary authentication method** is used. If the **Secondary authentication method** isn't available, then the **Secondary authentication method** isn't used, even if the **Primary authentication method** fails. In this scenario, authentication fails.

      Your options:

      - **Not configured**: Intune doesn't change or update this setting. By default, no secondary authentication method is used. If the **Primary authentication method** fails, then authentication fails.

      - **Username and Password**: Prompt the user for a user name and password to authenticate the network connection.

      - **SCEP certificate**: Select an existing SCEP **client certificate** profile that is also deployed to the device. This certificate is the identity presented by the device to the server to authenticate the network connection.

      - **PKCS certificate**: Select an existing PKCS **client certificate** profile and existing trusted **root certificate** that are also deployed to the device. The client certificate is the identity presented by the device to the server to authenticate the network connection.

      - **Derived credential**: Select an existing certificate profile that is derived from a user's smart card. For more information, go to [Use derived credentials in Microsoft Intune](../protect/derived-credentials.md).

## Related articles

- Be sure to [assign this profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).
- Learn more about the [wired network settings for macOS devices](wired-network-settings-macos.md).
- Get information on the [Extensible Authentication Protocol (EAP) for network access](/windows-server/networking/technologies/extensible-authentication-protocol/network-access).
