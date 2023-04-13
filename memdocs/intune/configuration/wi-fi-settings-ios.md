---
# required metadata

title: Configure Wi-Fi settings for iOS/iPadOS devices in Microsoft Intune
titleSuffix:
description: Create or add a WiFi device configuration profile for iOS/iPadOS devices. See the different settings, including adding certificates, choosing an EAP type, and selecting an authentication method in Microsoft Intune. 
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/06/2021
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier3
- M365-identity-device-management
---

# Add Wi-Fi settings for iOS and iPadOS devices in Microsoft Intune

You can create a profile with specific WiFi settings, and then deploy this profile to your iOS/iPadOS devices. Microsoft Intune offers many features, including authenticating to your network, adding a PKCS or SCEP certificate, and more.

These Wi-Fi settings are separated in to two categories: Basic settings and Enterprise-level settings.

This article describes these settings.

## Before you begin

Create an [iOS/iPadOS Wi-Fi device configuration profile](wi-fi-settings-configure.md).

> [!NOTE]
> These settings are available for all enrollment types. For more information on the enrollment types, see [iOS/iPadOS enrollment](/mem/intune/fundamentals/deployment-guide-enrollment-ios-ipados).
>
> These settings use the [Apple Wi-Fi payload](https://developer.apple.com/documentation/devicemanagement/wifi) (opens Apple's web site).

## Basic profiles

- **Wi-Fi type**: Select **Basic**.
- **Network name**: Enter a name for this Wi-Fi connection. This value is the name that users see when they browse the list of available connections on their device.
- **SSID**: Short for **service set identifier**. This property is the real name of the wireless network that devices connect to. However, users only see the network name you configured when they choose the connection.
- **Connect automatically**: **Enable** automatically connects to this network when the device is in range. **Disable** prevents devices from automatically connecting.
- **Hidden network**: **Enable** matches this device setting with the setting on the router Wi-Fi configuration. So if the network is set to hidden, then it's also hidden in the Wi-Fi profile. Select **Disable** if the network SSID is broadcasted and visible.
- **Security type**: Select the security protocol to authenticate to the Wi-Fi network. Your options:

  - **Open (no authentication)**: Only use this option if the network is unsecured.
  - **WPA/WPA2 - Personal**: Enter the password in **Pre-shared key**. When your organization's network is set up or configured, a password or network key is also configured. Enter this password or network key for the PSK value.
  - **WEP**

- **Proxy settings**: Your options:
  - **None**: No proxy settings are configured.
  - **Manual**: Enter the **Proxy server address** as an IP address, and its **Port number**.
  - **Automatic**: Use a file to configure the proxy server. Enter the **Proxy server URL** that contains the configuration file. For example, enter `http://proxy.contoso.com`, `10.0.0.11`, or `http://proxy.contoso.com/proxy.pac`.

    For more information on PAC files, see [Proxy Auto-Configuration (PAC) file](https://developer.mozilla.org/docs/Web/HTTP/Proxy_servers_and_tunneling/Proxy_Auto-Configuration_(PAC)_file) (opens a non-Microsoft site).

- **Disable MAC address randomization**: Starting with iOS/iPadOS 14, devices present a randomized MAC address instead of the physical MAC address when connecting to a network. Using randomized MAC addresses is recommended for privacy, as it's harder to track a device by its MAC address. However, randomized MAC addresses break functionality that relies on a static MAC address, including network access control (NAC).

  Your options:

  - **Not configured**: Intune doesn't change or update this setting. By default, when connecting to a network, devices will present a randomized MAC address instead of the physical MAC address when connecting to a new network.
  - **Yes**: Forces devices to present their actual Wi-Fi MAC address instead of a random MAC address. **Yes** allows devices to be tracked by their MAC address. Only disable MAC address randomization when necessary, such as for network access control (NAC) support.
  - **No**: Enables MAC address randomization on devices. Users can't turn it off. When connecting to a new network, devices present a randomized MAC address, instead of the physical MAC address.

  This setting applies to:  
  - iOS 14.0 and newer
  - iPadOS 14.0 and newer

## Enterprise profiles

- **Wi-Fi type**: Select **Enterprise**.
- **Network name**: Enter a name for this Wi-Fi connection. This value is the name that users see when they browse the list of available connections on their device.
- **SSID**: Short for **service set identifier**. This property is the real name of the wireless network that devices connect to. However, users only see the network name you configured when they choose the connection.
- **Connect automatically**: **Enable** automatically connects to this network when the device is in range. **Disable** prevents devices from automatically connecting.
- **Hidden network**: **Enable** matches this device setting with the setting on the router Wi-Fi configuration. So if the network is set to hidden, then it's also hidden in the Wi-Fi profile. Select **Disable** if the network SSID is broadcasted and visible.
- **Security type**: Select the security protocol to authenticate to the Wi-Fi network. Your options:
  - **WPA - Enterprise**
  - **WPA/WPA2 - Enterprise**

- **EAP type**: Select the Extensible Authentication Protocol (EAP) type used to authenticate secured wireless connections. Your options:

  - **EAP-FAST**: Enter the **Protected Access Credential (PAC) Settings**. This option uses protected access credentials to create an authenticated tunnel between the client and the authentication server. Your options:
    - **Do not use (PAC)**
    - **Use (PAC)**: If an existing PAC file exists, use it.
    - **Use and Provision PAC**: Create and add the PAC file to your devices.
    - **Use and Provision PAC Anonymously**: Create and add the PAC file to your devices without authenticating to the server.

  - **EAP-SIM**

  - **EAP-TLS**: Also enter:

    - **Certificate server names**: **Add** one or more common names used in the certificates issued by your trusted certificate authority (CA) to your wireless network access servers. For example, add `mywirelessserver.contoso.com` or `mywirelessserver`. When you enter this information, you can bypass the dynamic trust window displayed on user's devices when they connect to this Wi-Fi network.
    - **Root certificate for server validation**: Select an existing trusted root certificate profile. This certificate allows the client to trust the wireless network access server's certificate.

    - **Authentication method**: Select the authentication method used by your device clients. Your options:

      - **Derived credential**: Use a certificate that's derived from a user's smart card. If no derived credential issuer is configured, Intune prompts you to add one. For more information, see [Use derived credentials in Microsoft Intune](../protect/derived-credentials.md).

      - **Certificates**: Select the SCEP or PKCS client certificate profile that is also deployed to the device. This certificate is the identity presented by the device to the server to authenticate the connection.

      - **Identity privacy (outer identity)**: Enter the text sent in the response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent, and then followed by the real identification sent in a secure tunnel.

  - **EAP-TTLS**: Also enter:

    - **Certificate server names**: **Add** one or more common names used in the certificates issued by your trusted certificate authority (CA) to your wireless network access servers. For example, add `mywirelessserver.contoso.com` or `mywirelessserver`. When you enter this information, you can bypass the dynamic trust window displayed on user's devices when they connect to this Wi-Fi network.
    - **Root certificate for server validation**: Select an existing trusted root certificate profile. This certificate allows the client to trust the wireless network access server's certificate.

    - **Authentication method**: Select the authentication method used by your device clients. Your options:

      - **Derived credential**: Use a certificate that's derived from a user's smart card. If no derived credential issuer is configured, Intune prompts you to add one. For more information, see [Use derived credentials in Microsoft Intune](../protect/derived-credentials.md).

      - **Username and Password**: Prompt the user for a user name and password to authenticate the connection. Also enter:
        - **Non-EAP method (inner identity)**: Choose how you authenticate the connection. Be sure you choose the same protocol that's configured on your Wi-Fi network.

          Your options: **Unencrypted password (PAP)**, **Challenge Handshake Authentication Protocol (CHAP)**, **Microsoft CHAP (MS-CHAP)**, or **Microsoft CHAP Version 2 (MS-CHAP v2)**

      - **Certificates**: Select the SCEP or PKCS client certificate profile that is also deployed to the device. This certificate is the identity presented by the device to the server to authenticate the connection.

      - **Identity privacy (outer identity)**: Enter the text sent in the response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent, and then followed by the real identification sent in a secure tunnel.

  - **LEAP**

  - **PEAP**: Also enter:

    - **Certificate server names**: **Add** one or more common names used in the certificates issued by your trusted certificate authority (CA) to your wireless network access servers. For example, add `mywirelessserver.contoso.com` or `mywirelessserver`. When you enter this information, you can bypass the dynamic trust window displayed on user's devices when they connect to this Wi-Fi network.
    - **Root certificate for server validation**: Select an existing trusted root certificate profile. This certificate allows the client to trust the wireless network access server's certificate.

    - **Authentication method**: Select the authentication method used by your device clients. Your options:

      - **Derived credential**: Use a certificate that's derived from a user's smart card. If no derived credential issuer is configured, Intune prompts you to add one. For more information, see [Use derived credentials in Microsoft Intune](../protect/derived-credentials.md).

      - **Username and Password**: Prompt the user for a user name and password to authenticate the connection. 

      - **Certificates**: Select the SCEP or PKCS client certificate profile that is also deployed to the device. This certificate is the identity presented by the device to the server to authenticate the connection.

      - **Identity privacy (outer identity)**: Enter the text sent in the response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent, and then followed by the real identification sent in a secure tunnel.

- **Proxy settings**: Select a proxy configuration. Your options:

  - **None**: No proxy settings are configured.
  - **Manual**: Enter the **Proxy server address** as an IP address, and its **Port number**.
  - **Automatic**: Use a file to configure the proxy server. Enter the **Proxy server URL** that contains the configuration file. For example, enter `http://proxy.contoso.com`, `10.0.0.11`, or `http://proxy.contoso.com/proxy.pac`.

    For more information on PAC files, see [Proxy Auto-Configuration (PAC) file](https://developer.mozilla.org/docs/Web/HTTP/Proxy_servers_and_tunneling/Proxy_Auto-Configuration_(PAC)_file) (opens a non-Microsoft site).

- **Disable MAC address randomization**: Starting with iOS/iPadOS 14, devices present a randomized MAC address instead of the physical MAC address when connecting to a network. Using randomized MAC addresses is recommended for privacy, as it's harder to track a device by its MAC address. Randomized MAC addresses also break functionality that relies on a static MAC address, including network access control (NAC).

  Your options:

  - **Not configured**: Intune doesn't change or update this setting. By default, when connecting to a network, devices may present a randomized MAC address instead of the physical MAC address.
  - **Yes**: Forces devices to present their actual Wi-Fi MAC address instead of a random MAC address. **Yes** allows devices to be tracked by their MAC address. Only disable MAC address randomization when necessary, such as for network access control (NAC) support.
  - **No**: Enables MAC address randomization on devices. Users can't turn it off. When connecting to a network, devices present a randomized MAC address, instead of the physical MAC address.

  This setting applies to:

  - iOS 14.0 and newer
  - iPadOS 14.0 and newer

## Next steps

The profile is created, but may not be doing anything. Be sure to [assign this profile](device-profile-assign.md), and [monitor its status](device-profile-monitor.md).

Configure Wi-Fi settings on [Android](wi-fi-settings-android.md), [Android Enterprise](wi-fi-settings-android-enterprise.md), [macOS](wi-fi-settings-macos.md), and [Windows 10](wi-fi-settings-windows.md) devices.
