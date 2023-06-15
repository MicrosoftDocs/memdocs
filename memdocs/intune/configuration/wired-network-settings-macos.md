---
# required metadata

title: Configure wired network settings for macOS devices in Microsoft Intune
titleSuffix:
description: Create or add a wired network device configuration profile for macOS devices. See the different settings, add certificates, choose an EAP type, and select an authentication method in Microsoft Intune. 
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/14/2023
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier3
- M365-identity-device-management
---

# Add wired network settings for macOS devices in Microsoft Intune

> [!NOTE]
> [!INCLUDE [not-all-settings-are-documented](../includes/not-all-settings-are-documented.md)]

You can create a profile with specific wired network settings, and then deploy this profile to your macOS devices. Microsoft Intune offers many features, including authenticating to your network, adding a SCEP certificate, and more.

This feature applies to:

- macOS

This article describes the settings you can configure.

## Before you begin

- Create a [macOS wired network device configuration profile](wired-networks-configure.md).

- These settings are available for all enrollment types. For more information on the enrollment types, see [macOS enrollment](../enrollment/macos-enroll.md).

## Wired Network

- **Network Interface**: Select the network interfaces on the device the profile applies to, based on service-order priority. Your options:
  
  - **First active Ethernet** (default)
  - **Second active Ethernet**
  - **Third active Ethernet**
  - **First Ethernet**
  - **Second Ethernet**
  - **Third Ethernet**
  - **Any Ethernet**

  Options with "active" in the title use interfaces that are actively working on the device. If there are no active interfaces, the next interface in service-order priority is configured. By default, **First active Ethernet** is selected, which is also the default setting configured by macOS.

- **EAP type**: Select the Extensible Authentication Protocol (EAP) type to authenticate secured wired connections. Your options:

  - **EAP-FAST**: Enter the **Protected Access Credential (PAC) Settings**. This option uses protected access credentials to create an authenticated tunnel between the client and the authentication server. Your options:
    - **Do not use (PAC)**
    - **Use (PAC)**: If an existing PAC file exists, use it.
    - **Use and Provision PAC**: Create and add the PAC file to your devices.
    - **Use and Provision PAC Anonymously**: Create and add the PAC file to your devices without authenticating to the server.

  - **EAP-TLS**: Also enter:

    - **Server Trust** - **Certificate server names**: Enter one or more common names used in the certificates issued by your trusted certificate authority (CA). When you enter this information, you can bypass the dynamic trust window shown on user devices when they connect to this network.
    - **Root certificate for server validation**: Select one or more existing trusted root certificate profiles. When the client connects to the network, these certificates are used to establish a chain of trust with the server. If your authentication server uses a public certificate, then you don't need to include a root certificate.
    - **Client Authentication** - **Certificates**: Select an existing SCEP client certificate profile that's also deployed to the device. This certificate is the identity presented by the device to the server to authenticate the connection. PKCS certificates aren't supported.
    - **Identity privacy (outer identity)**: Enter the text sent in the response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent, and then followed by the real identification sent in a secure tunnel.

  - **EAP-TTLS**: Also enter:

    - **Server Trust** - **Certificate server names**: Enter one or more common names used in the certificates issued by your trusted certificate authority (CA). When you enter this information, you can bypass the dynamic trust window shown on user devices when they connect to this network.
    - **Root certificate for server validation**: Select one or more existing trusted root certificate profiles. When the client connects to the network, these certificates are used to establish a chain of trust with the server. If your authentication server uses a public certificate, then you don't need to include a root certificate.
    - **Client Authentication**: Select an **Authentication method**. Your options:
      - **Username and Password**: Prompts the user for a user name and password to authenticate the connection. Also enter:
        - **Non-EAP method (inner identity)**: Select how you authenticate the connection. Be sure you choose the same protocol that's configured on your network. Your options:
          - **Unencrypted password (PAP)**
          - **Challenge Handshake Authentication Protocol (CHAP)**
          - **Microsoft CHAP (MS-CHAP)**
          - **Microsoft CHAP Version 2 (MS-CHAP v2)**
      - **Certificates**: Select an existing SCEP client certificate profile that's also deployed to the device. This certificate is the identity presented by the device to the server to authenticate the connection. PKCS certificates aren't supported.
      - **Identity privacy (outer identity)**: Enter the text sent in the response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent, and then followed by the real identification sent in a secure tunnel.

  - **LEAP**

  - **PEAP**: Also enter:

    - **Server Trust** - **Certificate server names**: Enter one or more common names used in the certificates issued by your trusted certificate authority (CA). When you enter this information, you can bypass the dynamic trust window shown on user devices when they connect to this network.
    - **Root certificate for server validation**: Select one or more existing trusted root certificate profiles. When the client connects to the network, these certificates are used to establish a chain of trust with the server. If your authentication server uses a public certificate, then you don't need to include a root certificate.
    - **Client Authentication**: Select an **Authentication method**. Your options:
      - **Username and Password**: Prompts the user for a user name and password to authenticate the connection.
      - **Certificates**: Select an existing SCEP client certificate profile that's also deployed to the device. This certificate is the identity presented by the device to the server to authenticate the connection. PKCS certificates aren't supported.
      - **Identity privacy (outer identity)**: Enter the text sent in the response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent, and then followed by the real identification sent in a secure tunnel.

## Next steps

The profile is created, but it may not be doing anything. Be sure to [assign this profile](device-profile-assign.md), and [monitor its status](device-profile-monitor.md).

[Wired network settings for Windows devices](wired-network-settings-windows.md)
