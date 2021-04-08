---
# required metadata

title: Configure Wi-Fi settings for macOS devices in Microsoft Intune - Azure | Microsoft Docs
titleSuffix:
description: Create or add a WiFi device configuration profile for macOS devices. See the different settings, add certificates, choose an EAP type, and select an authentication method in Microsoft Intune. 
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/29/2021
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Add Wi-Fi settings for macOS devices in Microsoft Intune

You can create a profile with specific Wi-Fi settings, and then deploy this profile to your macOS devices. Microsoft Intune offers many features, including authenticating to your network, adding a PKCS or SCEP certificate, and more.

These Wi-Fi settings are separated in to two categories: Basic settings and Enterprise settings.

This article describes these settings.

## Before you begin

Create a [macOS Wi-Fi device configuration profile](wi-fi-settings-configure.md).

> [!NOTE]
> These settings are available for all enrollment types. For more information on the enrollment types, see [macOS enrollment](../enrollment/macos-enroll.md).

## Basic profiles

Basic or personal profiles use WPA/WPA2 to secure the Wi-Fi connection on devices. Typically, WPA/WPA2 is used on home networks or personal networks. You can also add a pre-shared key to authenticate the connection.

- **Wi-Fi type**: Select **Basic**.
- **SSID**: Short for **service set identifier**. This property is the real name of the wireless network that devices connect to. However, users only see the network name you configured when they choose the connection.
- **Connect automatically**: Select **Enable** to automatically connect to this network when the device is in range. Select **Disable** to prevent devices from automatically connecting.
- **Hidden network**: Select **Enable** to hide this network from the list of available networks on the device. The SSID isn't broadcasted. Select **Disable** to show this network in the list of available networks on the device.
- **Security type**: Select the security protocol to authenticate to the Wi-Fi network. Your options:

  - **Open (no authentication)**: Only use this option if the network is unsecured.
  - **WPA/WPA2 - Personal**: Enter the password in **Pre-shared key**. When your organization's network is set up or configured, a password or network key is also configured. Enter this password or network key for the PSK value.
  - **WEP**

- **Proxy settings**: Your options:
  - **None**: No proxy settings are configured.
  - **Manual**: Enter the **Proxy server address** as an IP address, and its **Port number**.
  - **Automatic**: Use a file to configure the proxy server. Enter the **Proxy server URL** that contains the configuration file. For example, enter `http://proxy.contoso.com`, `10.0.0.11`, or `http://proxy.contoso.com/proxy.pac`.

    For more information on PAC files, see [Proxy Auto-Configuration (PAC) file](https://developer.mozilla.org/docs/Web/HTTP/Proxy_servers_and_tunneling/Proxy_Auto-Configuration_(PAC)_file) (opens a non-Microsoft site).

## Enterprise profiles

Enterprise profiles use Extensible Authentication Protocol (EAP) to authenticate Wi-Fi connections. EAP is often used by enterprises, as you can use certificates to authenticate and secure connections, and configure more security options.

- **Wi-Fi type**: Select **Enterprise**.
- **SSID**: Short for **service set identifier**. This property is the real name of the wireless network that devices connect to. However, users only see the network name you configured when they choose the connection.
- **Connect automatically**: Select **Enable** to automatically connect to this network when the device is in range. Select **Disable** to prevent devices from automatically connecting.
- **Hidden network**: Select **Enable** to hide this network from the list of available networks on the device. The SSID isn't broadcasted. Select **Disable** to show this network in the list of available networks on the device.

- **EAP type**: Select the Extensible Authentication Protocol (EAP) type used to authenticate secured wireless connections. Your options:

  - **EAP-FAST**: Enter the **Protected Access Credential (PAC) Settings**. This option uses protected access credentials to create an authenticated tunnel between the client and the authentication server. Your options:
    - **Do not use (PAC)**
    - **Use (PAC)**: If an existing PAC file exists, use it.
    - **Use and Provision PAC**: Create and add the PAC file to your devices.
    - **Use and Provision PAC Anonymously**: Create and add the PAC file to your devices without authenticating to the server.

  - **EAP-SIM**

  - **EAP-TLS**: Also enter:

    - **Certificate server names**: **Add** one or more common names used in the certificates issued by your trusted certificate authority (CA). When you enter this information, you can bypass the dynamic trust window displayed on user's devices when they connect to this Wi-Fi network.
    - **Root certificate for server validation**: Select one or more existing trusted root certificate profiles. When the client connects to the network, these certificates are presented to the server. They authenticate the connection.

    - **Certificates**: Select the SCEP or PKCS client certificate profile that is also deployed to the device. This certificate is the identity presented by the device to the server to authenticate the connection.

    - **Identity privacy (outer identity)**: Enter the text sent in the response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent, and then followed by the real identification sent in a secure tunnel.

  - **EAP-TTLS**: Also enter:

    - **Certificate server names**: **Add** one or more common names used in the certificates issued by your trusted certificate authority (CA). When you enter this information, you can bypass the dynamic trust window displayed on user's devices when they connect to this Wi-Fi network.
    - **Root certificates for server validation**: Select one or more existing trusted root certificate profiles. When the client connects to the network, these certificates are presented to the server. They authenticate the connection.

    - **Authentication method**: Select the authentication method used by your device clients. Your options:

      - **Username and Password**: Prompt the user for a user name and password to authenticate the connection. Also enter:
        - **Non-EAP method (inner identity)**: Choose how you authenticate the connection. Be sure you choose the same protocol that's configured on your Wi-Fi network.

          Your options: **Unencrypted password (PAP)**, **Challenge Handshake Authentication Protocol (CHAP)**, **Microsoft CHAP (MS-CHAP)**, or **Microsoft CHAP Version 2 (MS-CHAP v2)**

      - **Certificates**: Select the SCEP or PKCS client certificate profile that is also deployed to the device. This certificate is the identity presented by the device to the server to authenticate the connection.

      - **Identity privacy (outer identity)**: Enter the text sent in the response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent, and then followed by the real identification sent in a secure tunnel.

  - **LEAP**

  - **PEAP**: Also enter:

    - **Certificate server names**: **Add** one or more common names used in the certificates issued by your trusted certificate authority (CA). When you enter this information, you can bypass the dynamic trust window displayed on user's devices when they connect to this Wi-Fi network.
    - **Root certificate for server validation**: Select one or more existing trusted root certificate profiles. When the client connects to the network, these certificates are presented to the server. They authenticate the connection.

    - **Authentication method**: Select the authentication method used by your device clients. Your options:

      - **Username and Password**: Prompt the user for a user name and password to authenticate the connection. 

      - **Certificates**: Select the SCEP or PKCS client certificate profile that is also deployed to the device. This certificate is the identity presented by the device to the server to authenticate the connection.

      - **Identity privacy (outer identity)**: Enter the text sent in the response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent, and then followed by the real identification sent in a secure tunnel.

- **Proxy settings**: Select a proxy configuration. Your options:

  - **None**: No proxy settings are configured.
  - **Manual**: Enter the **Proxy server address** as an IP address, and its **Port number**.
  - **Automatic**: Use a file to configure the proxy server. Enter the **Proxy server URL** that contains the configuration file. For example, enter `http://proxy.contoso.com`, `10.0.0.11`, or `http://proxy.contoso.com/proxy.pac`.

    For more information on PAC files, see [Proxy Auto-Configuration (PAC) file](https://developer.mozilla.org/docs/Web/HTTP/Proxy_servers_and_tunneling/Proxy_Auto-Configuration_(PAC)_file) (opens a non-Microsoft site).

## Next steps

The profile is created, but may not be doing anything. Be sure to [assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).

Configure Wi-Fi settings on [Android](wi-fi-settings-android.md), [Android Enterprise](wi-fi-settings-android-enterprise.md), [iOS/iPadOS](wi-fi-settings-ios.md), and [Windows 10](wi-fi-settings-windows.md) devices.
