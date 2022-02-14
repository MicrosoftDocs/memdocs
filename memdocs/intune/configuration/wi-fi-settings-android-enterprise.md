---
# required metadata

title: Wi-Fi settings for Android Enterprise and kiosk devices - Microsoft Intune | Microsoft Docs
description: Create or add a WiFi device configuration profile for Android Enterprise and Android Kiosk. See the different settings, add certificates, choose an EAP type, and select an authentication method in Microsoft Intune. For kiosk devices, also enter the Pre-shared key of your network.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/23/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:
params:
  siblings_only: true
ms.reviewer: maholdaa
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: seodec18
ms.collection: M365-identity-device-management
---

# Add Wi-Fi settings for Android Enterprise dedicated and fully managed devices in Microsoft Intune

You can create a profile with specific Wi-Fi settings, and then deploy this profile to your Android Enterprise fully managed and dedicated devices. Microsoft Intune offers many features, including authenticating to your network, using a pre-shared key, and more.

This feature applies to:

- Android Enterprise personally owned devices with a work profile (BYOD)
- Android Enterprise corporate-owned work profile (COPE)
- Android Enterprise corporate owned fully managed (COBO)
- Android Enterprise corporate owned dedicated devices (COSU)

This article describes these settings. [Use Wi-Fi on your devices](wi-fi-settings-configure.md) includes more information about the Wi-Fi feature in Microsoft Intune.

## Before you begin

Create an [Android Enterprise Wi-Fi device configuration profile](wi-fi-settings-configure.md):

- Fully managed, dedicated, and corporate-owned work profile
- Personally-owned work profile

## Fully Managed, Dedicated, and Corporate-Owned Work Profile

Select this option if you're deploying to an Android Enterprise dedicated, corporate-owned work profile, or fully managed device.

### Basic

- **Wi-Fi type**: Select **Basic**.
- **Network name**: Enter a name for this Wi-Fi connection. End users see this name when they browse their device for available Wi-Fi connections. For example, enter **Contoso WiFi**.
- **SSID**: Enter the **service set identifier**, which is the real name of the wireless network that devices connect to. However, users only see the **network name** you configured when they choose the connection.
- **Connect automatically**: **Enable** automatically connects to your Wi-Fi network when devices are in range. Select **Disable** to prevent or block this automatic connection. 

  When devices are connected to another preferred Wi-Fi connection, then they won't automatically connect to this Wi-Fi network. If devices fail to connect automatically when this setting is enabled, then disconnect the devices from any existing Wi-Fi connections.

- **Hidden network**: Select **Enable** to hide this network from the list of available networks on the device. The SSID isn't broadcasted. Select **Disable** to show this network in the list of available networks on the device.
- **Wi-Fi type**: Select the security protocol to authenticate to the Wi-Fi network. Your options:

  - **Open (no authentication)**: Only use this option if the network is unsecured.
  - **WEP-Pre-shared key**: Enter the password in **Pre-shared key**. When your organization's network is set up or configured, a password or network key is also configured. Enter this password or network key for the PSK value.
  - **WPA-Pre-shared key**: Enter the password in **Pre-shared key**. When your organization's network is set up or configured, a password or network key is also configured. Enter this password or network key for the PSK value.

### Enterprise

- **Wi-Fi type**: Select **Enterprise**.
- **SSID**: Enter the **service set identifier**, which is the real name of the wireless network that devices connect to. However, users only see the **network name** you configured when they choose the connection.
- **Connect automatically**: **Enable** automatically connects to your Wi-Fi network when devices are in range. Select **Disable** to prevent or block this automatic connection. 

  When devices are connected to another preferred Wi-Fi connection, then they won't automatically connect to this Wi-Fi network. If devices fail to connect automatically when this setting is enabled, then disconnect the devices from any existing Wi-Fi connections.

- **Hidden network**: Select **Enable** to hide this network from the list of available networks on the device. The SSID isn't broadcasted. Select **Disable** to show this network in the list of available networks on the device.
- **EAP type**: Select the Extensible Authentication Protocol (EAP) type used to authenticate secured wireless connections. Your options:

  - **EAP-TLS**: To authenticate, the Extensible Authentication Protocol (EAP) Transport Layer Security (TLS) uses a digital certificate on the server, and a digital certificate on the client. Both certificates are signed by a certificate authority (CA) that the server and client trust.

    Also enter:

    - **Radius server name**: Enter the DNS name that's used in the certificate presented by the Radius Server during client authentication to the Wi-Fi access point. For example, enter `Contoso.com`, `uk.contoso.com`, or `jp.contoso.com`.

      If you have multiple Radius servers with the same DNS suffix in their fully qualified domain name, then you can enter only the suffix. For example, you can enter `contoso.com`.

      When you enter this value, user devices can bypass the dynamic trust dialog that's sometimes shown when connecting to the Wi-Fi network.

      On Android 11 and newer, new Wi-Fi profiles may require this setting be configured. Otherwise, the devices may not connect to your Wi-Fi network.

    - **Root certificate for server validation**: Select an existing trusted root certificate profile. When the client connects to the network, this certificate is presented to the server, and authenticates the connection.

    - **Authentication method**: Select the authentication method used by your device clients. Your options:
      - **Derived credential**: Use a certificate that's derived from a user's smart card. If no derived credential issuer is configured, Intune prompts you to add one. For more information, see [Use derived credentials in Microsoft Intune](../protect/derived-credentials.md).
      - **Certificates**: Select the SCEP or PKCS client certificate profile that is also deployed to the device. This certificate is the identity presented by the device to the server to authenticate the connection.

    - **Identity privacy (outer identity)**: Enter the text sent in the response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent, and then followed by the real identification sent in a secure tunnel.​

  - **EAP-TTLS**: To authenticate, the Extensible Authentication Protocol (EAP) Tunneled Transport Layer Security (TTLS) uses a digital certificate on the server. When the client makes the authentication request, the server uses the tunnel, which is a secure connection, to complete the authentication request.

    Also enter:

    - **Radius server name**: Enter the DNS name that's used in the certificate presented by the Radius Server during client authentication to the Wi-Fi access point. For example, enter `Contoso.com`, `uk.contoso.com`, or `jp.contoso.com`.

      If you have multiple Radius servers with the same DNS suffix in their fully qualified domain name, then you can enter only the suffix. For example, you can enter `contoso.com`.

      When you enter this value, user devices can bypass the dynamic trust dialog that's sometimes shown when connecting to the Wi-Fi network.

      On Android 11 and newer, new Wi-Fi profiles may require this setting be configured. Otherwise, the devices may not connect to your Wi-Fi network.

    - **Root certificate for server validation**: Select an existing trusted root certificate profile. When the client connects to the network, this certificate is presented to the server, and authenticates the connection.

    - **Authentication method**: Select the authentication method used by your device clients. Your options:

      - **Derived credential**: Use a certificate that's derived from a user's smart card. If no derived credential issuer is configured, Intune prompts you to add one. For more information, see [Use derived credentials in Microsoft Intune](../protect/derived-credentials.md).
      - **Username and Password**: Prompt the user for a user name and password to authenticate the connection. Also enter:
        - **Non-EAP method (inner identity)**: Choose how you authenticate the connection. Be sure you select the same protocol that's configured on your Wi-Fi network. Your options:

          - **Unencrypted password (PAP)**
          - **Microsoft CHAP (MS-CHAP)**
          - **Microsoft CHAP Version 2 (MS-CHAP v2)**

      - **Certificates**: Select the SCEP or PKCS client certificate profile that is also deployed to the device. This certificate is the identity presented by the device to the server to authenticate the connection.

      - **Identity privacy (outer identity)**: Enter the text sent in the response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent, and then followed by the real identification sent in a secure tunnel.

  - **PEAP**: Protected Extensible Authentication Protocol (PEAP) encrypts and authenticates using a protected tunnel. Also enter:

    - **Radius server name**: Enter the DNS name that's used in the certificate presented by the Radius Server during client authentication to the Wi-Fi access point. For example, enter `Contoso.com`, `uk.contoso.com`, or `jp.contoso.com`.

      If you have multiple Radius servers with the same DNS suffix in their fully qualified domain name, then you can enter only the suffix. For example, you can enter `contoso.com`.

      When you enter this value, user devices can bypass the dynamic trust dialog that's sometimes shown when connecting to the Wi-Fi network.

      On Android 11 and newer, new Wi-Fi profiles may require this setting be configured. Otherwise, the devices may not connect to your Wi-Fi network.

    - **Root certificate for server validation**: Select an existing trusted root certificate profile. When the client connects to the network, this certificate is presented to the server, and authenticates the connection.

    - **Authentication method**: Select the authentication method used by your device clients. Your options:

      - **Derived credential**: Use a certificate that's derived from a user's smart card. If no derived credential issuer is configured, Intune prompts you to add one. For more information, see [Use derived credentials in Microsoft Intune](../protect/derived-credentials.md).
      - **Username and Password**: Prompt the user for a user name and password to authenticate the connection. Also enter:
        - **Non-EAP method for authentication (inner identity)**: Choose how you authenticate the connection. Be sure you select the same protocol that's configured on your Wi-Fi network. Your options:

          - **None**
          - **Microsoft CHAP Version 2 (MS-CHAP v2)**

      - **Certificates**: Select the SCEP or PKCS client certificate profile that is also deployed to the device. This certificate is the identity presented by the device to the server to authenticate the connection.

      - **Identity privacy (outer identity)**: Enter the text sent in the response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent, and then followed by the real identification sent in a secure tunnel.

## Personally-owned work profile

### Basic

- **Wi-Fi type**: Select **Basic**.
- **SSID**: Enter the **service set identifier**, which is the real name of the wireless network that devices connect to. However, users only see the **network name** you configured when they choose the connection.
- **Hidden network**: Select **Enable** to hide this network from the list of available networks on the device. The SSID isn't broadcasted. Select **Disable** to show this network in the list of available networks on the device.

### Enterprise

- **Wi-Fi type**: Select **Enterprise**.
- **SSID**: Enter the **service set identifier**, which is the real name of the wireless network that devices connect to. However, users only see the **network name** you configured when they choose the connection.
- **Hidden network**: Select **Enable** to hide this network from the list of available networks on the device. The SSID isn't broadcasted. Select **Disable** to show this network in the list of available networks on the device.
- **EAP type**: Select the Extensible Authentication Protocol (EAP) type used to authenticate secured wireless connections. Your options:

  - **EAP-TLS**: Also enter:  
  
    - **Certificate server names**: **Add** one or more common names used in the certificates issued by your trusted certificate authority (CA) to your wireless network access servers. For example, add `mywirelessserver.contoso.com` or `mywirelessserver`. When you enter this information, you can bypass the dynamic trust window displayed on user's devices when they connect to this Wi-Fi network.  

    - **Root certificate for server validation**: Select an existing trusted root certificate profile. When the client connects to the network, this certificate is presented to the server, and authenticates the connection.

    - **Certificates**: Select the SCEP or PKCS client certificate profile that is also deployed to the device. This certificate is the identity presented by the device to the server to authenticate the connection.

    - **Identity privacy (outer identity)**: Enter the text sent in the response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent, and then followed by the real identification sent in a secure tunnel.

  - **EAP-TTLS**: Also enter:

    - **Root certificate for server validation**: Select an existing trusted root certificate profile. When the client connects to the network, this certificate is presented to the server, and authenticates the connection.

    - **Authentication method**: Select the authentication method used by your device clients. Your options:

      - **Username and Password**: Prompt the user for a user name and password to authenticate the connection. Also enter:
        - **Non-EAP method (inner identity)**: Choose how you authenticate the connection. Be sure you select the same protocol that's configured on your Wi-Fi network. Your options:

          - **Unencrypted password (PAP)**
          - **Microsoft CHAP (MS-CHAP)**
          - **Microsoft CHAP Version 2 (MS-CHAP v2)**

      - **Certificates**: Select the SCEP or PKCS client certificate profile that is also deployed to the device. This certificate is the identity presented by the device to the server to authenticate the connection.

      - **Identity privacy (outer identity)**: Enter the text sent in the response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent, and then followed by the real identification sent in a secure tunnel.

  - **PEAP**: Also enter:

    - **Root certificate for server validation**: Select an existing trusted root certificate profile. When the client connects to the network, this certificate is presented to the server, and authenticates the connection.

    - **Authentication method**: Select the authentication method used by your device clients. Your options:

      - **Username and Password**: Prompt the user for a user name and password to authenticate the connection. Also enter:
        - **Non-EAP method for authentication (inner identity)**: Choose how you authenticate the connection. Be sure you select the same protocol that's configured on your Wi-Fi network. Your options:

          - **None**
          - **Microsoft CHAP Version 2 (MS-CHAP v2)**

      - **Certificates**: Select the SCEP or PKCS client certificate profile that is also deployed to the device. This certificate is the identity presented by the device to the server to authenticate the connection.

      - **Identity privacy (outer identity)**: Enter the text sent in the response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent, and then followed by the real identification sent in a secure tunnel.

- **Proxy settings**: Select a proxy configuration. Your options:

  - **None**: No proxy settings are configured.
  - **Automatic**: Use a file to configure the proxy server. Enter the **Proxy server URL** that contains the configuration file. For example, enter `http://proxy.contoso.com`, `10.0.0.11`, or `http://proxy.contoso.com/proxy.pac`.

    For more information on PAC files, see [Proxy Auto-Configuration (PAC) file](https://developer.mozilla.org/docs/Web/HTTP/Proxy_servers_and_tunneling/Proxy_Auto-Configuration_(PAC)_file) (opens a non-Microsoft site).

## Next steps

The profile is created, but might not be doing anything. Be sure to [assign this profile](device-profile-assign.md) and [monitor its status.](device-profile-monitor.md).

You can also create Wi-Fi profiles for [Android](wi-fi-settings-android.md), [iOS/iPadOS](wi-fi-settings-ios.md), [macOS](wi-fi-settings-macos.md), [Windows 10](wi-fi-settings-windows.md), and [Windows 8.1](wi-fi-settings-import-windows-8-1.md) devices.

[Troubleshoot common issues with Wi-Fi profiles](/troubleshoot/mem/intune/troubleshoot-wi-fi-profiles#common-issues).
