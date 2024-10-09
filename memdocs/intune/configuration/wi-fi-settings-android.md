---
# required metadata

title: Configure Wi-Fi settings for Android devices in Microsoft Intune
titleSuffix:
description: Create or add a WiFi device configuration profile for Android device administrator. See the different settings, including adding certificates, choosing an EAP type, and selecting an authentication method in Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/23/2024
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: abalwan
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier3
- M365-identity-device-management
---

# Add Wi-Fi settings for devices running Android device administrator in Microsoft Intune

You can create a profile with specific WiFi settings, and then deploy this profile to your Android devices. Microsoft Intune offers many features, including authenticating to your network, adding a PKCS or SCEP certificate, and more.

This feature applies to:

- Android device administrator (DA)

These Wi-Fi settings are separated in to two categories: Basic settings and Enterprise-level settings. This article describes these settings.

[!INCLUDE [android_device_administrator_support](../includes/android-device-administrator-support.md)]

## Before you begin

- Create an [Android device administrator Wi-Fi device configuration profile](wi-fi-settings-configure.md).

## Basic

- **Wi-Fi type**: Choose **Basic**.
- **SSID**: Enter the **service set identifier**, which is the real name of the wireless network that devices connect to. However, users only see the **network name** you configured when they choose the connection.

  You can only deploy one Wi-Fi profile to the same device with the same SSID. If you try to deploy multiple Wi-Fi profiles to the same device with the same SSID, then the profile isn't deployed to the device. 

- **Hidden network**: Choose **Enable** to hide this network from the list of available networks on the device. The SSID isn't broadcasted. Choose **Disable** to show this network in the list of available networks on the device.

## Enterprise

- **Wi-Fi type**: Choose **Enterprise**.
- **SSID**: Enter the **service set identifier**, which is the real name of the wireless network that devices connect to. However, users only see the **network name** you configured when they choose the connection.

  You can only deploy one Wi-Fi profile to the same device with the same SSID. If you try to deploy multiple Wi-Fi profiles to the same device with the same SSID, then the profile isn't deployed to the device. 

- **Hidden network**: Choose **Enable** to hide this network from the list of available networks on the device. The SSID isn't broadcasted. Choose **Disable** to show this network in the list of available networks on the device.
- **EAP type**: Choose the Extensible Authentication Protocol (EAP) type used to authenticate secured wireless connections. Your options:

  - **EAP-TLS**: Also enter:

    - **Server Trust** - **Root certificate for server validation**: Select one or more existing trusted root certificate profiles. When the client connects to the network, these certificates are used to establish a chain of trust with the server. If your authentication server uses a public certificate, then you don't need to include a root certificate.

    - **Client Authentication** - **Client certificate for client authentication (Identity certificate)**: Choose the SCEP or PKCS client certificate profile that is also deployed to the device. This certificate is the identity presented by the device to the server to authenticate the connection.

    - **Identity privacy (outer identity)**: Enter the text sent in the response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent, and then followed by the real identification sent in a secure tunnel.​

  - **EAP-TTLS**: Also enter:

    - **Server Trust** - **Root certificate for server validation**: Select one or more existing trusted root certificate profiles. When the client connects to the network, these certificates are used to establish a chain of trust with the server. If your authentication server uses a public certificate, then you don't need to include a root certificate.

      > [!NOTE]
      > For Android 11 and newer, Google requires a Trusted root certificate.

    - **Client Authentication**: Choose an **Authentication method**. Your options:

      - **Username and Password**: Prompt the user for a user name and password to authenticate the connection. Also enter:
        - **Non-EAP method (inner identity)**: Choose how you authenticate the connection. Be sure you choose the same protocol that's configured on your Wi-Fi network. Your options:

          - **Unencrypted password (PAP)**
          - **Challenge Handshake Authentication Protocol (CHAP)**
          - **Microsoft CHAP (MS-CHAP)**
          - **Microsoft CHAP Version 2 (MS-CHAP v2)**

      - **Certificates**: Choose the SCEP or PKCS client certificate profile that is also deployed to the device. This certificate is the identity presented by the device to the server to authenticate the connection.

      - **Identity privacy (outer identity)**: Enter the text sent in the response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent, and then followed by the real identification sent in a secure tunnel.

  - **PEAP**: Also enter:

    - **Server Trust** - **Root certificate for server validation**: Select one or more existing trusted root certificate profiles. When the client connects to the network, these certificates are used to establish a chain of trust with the server. If your authentication server uses a public certificate, then you don't need to include a root certificate.

    - **Client Authentication**: Choose an **Authentication method**. Your options:

      - **Username and Password**: Prompt the user for a user name and password to authenticate the connection. Also enter:
        - **Non-EAP method for authentication (inner identity)**: Choose how you authenticate the connection. Be sure you choose the same protocol that's configured on your Wi-Fi network. Your options:

          - **None**
          - **Microsoft CHAP Version 2 (MS-CHAP v2)**

      - **Certificates**: Choose the SCEP or PKCS client certificate profile that is also deployed to the device. This certificate is the identity presented by the device to the server to authenticate the connection.

      - **Identity privacy (outer identity)**: Enter the text sent in the response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent, and then followed by the real identification sent in a secure tunnel.

## Next steps

The profile is created, but it's not doing anything. Next, [assign this profile](device-profile-assign.md).

## More resources

- [Wi-Fi settings overview](wi-fi-settings-configure.md), including other platforms.

- Using Android Enterprise or Android Kiosk devices? If yes, then look at [Wi-Fi settings for devices running Android Enterprise and dedicated devices](wi-fi-settings-android-enterprise.md).
