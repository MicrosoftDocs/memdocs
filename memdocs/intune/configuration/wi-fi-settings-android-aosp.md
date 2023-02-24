---
# required metadata

title: Wi-Fi settings for Android AOSP - Microsoft Intune | Microsoft Docs
description: Create or add a WiFi device configuration profile for Android open source project (AOSP) devices. See the different settings, add certificates, and choose an EAP type in Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 09/20/2022
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium

# optional metadata

#ROBOTS:
#audience:
params:
  siblings_only: true
ms.reviewer: priyar, tycast
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom:
ms.collection:
- tier3
- M365-identity-device-management
---

# Add Wi-Fi settings for Android (AOSP) devices in Microsoft Intune

You can create a profile with specific Wi-Fi settings, and then deploy this profile to your Android Open Source Project (AOSP) devices. Microsoft Intune offers many features, including authenticating to your network, using a pre-shared key, and more.

This feature applies to:

- Android (AOSP)

This article describes these settings. [Use Wi-Fi on your devices](wi-fi-settings-configure.md) includes more information about the Wi-Fi feature in Microsoft Intune.

For more information on AOSP, go to [Android Open Source Project](https://source.android.com/) (opens Android's website).

## Before you begin

Create an [Android (AOSP) device configuration profile](wi-fi-settings-configure.md).

## Basic

- **Wi-Fi type**: Select **Basic**.
- **Network name**: Enter a name for this Wi-Fi connection. End users see this name when they browse their device for available Wi-Fi connections. For example, enter **Contoso WiFi**.
- **SSID**: Enter the **service set identifier**, which is the real name of the wireless network that devices connect to. However, users only see the **network name** you configured when they choose the connection.
- **Connect automatically**: **Enable** automatically connects to your Wi-Fi network when devices are in range. Select **Disable** to prevent or block this automatic connection.

  When devices are connected to another preferred Wi-Fi connection, then they won't automatically connect to this Wi-Fi network. If devices fail to connect automatically when this setting is enabled, then disconnect the devices from any existing Wi-Fi connections.

- **Hidden network**: Select **Enable** to hide this network from the list of available networks on the device. The SSID isn't broadcasted. Select **Disable** to show this network in the list of available networks on the device.
- **Wi-Fi type**: Select the security protocol to authenticate to the Wi-Fi network. Your options:

  - **Open (no authentication)**: Only use this option if the network is unsecured.
  - **WEP-Pre-shared key**: Enter the password in **Pre-shared key** (PSK). When your organization's network is set up or configured, a password or network key is also configured. Enter this password or network key for the PSK value.
  - **WPA-Pre-shared key**: Enter the password in **Pre-shared key** (PSK). When your organization's network is set up or configured, a password or network key is also configured. Enter this password or network key for the PSK value.

## Enterprise

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

    - **Identity privacy (outer identity)**: Enter the text sent in the response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent, and then followed by the real identification sent in a secure tunnel.​

  - **EAP-TTLS**: To authenticate, the Extensible Authentication Protocol (EAP) Tunneled Transport Layer Security (TTLS) uses a digital certificate on the server. When the client makes the authentication request, the server uses the tunnel, which is a secure connection, to complete the authentication request.

    Also enter:

    - **Radius server name**: Enter the DNS name that's used in the certificate presented by the Radius Server during client authentication to the Wi-Fi access point. For example, enter `Contoso.com`, `uk.contoso.com`, or `jp.contoso.com`.

      If you have multiple Radius servers with the same DNS suffix in their fully qualified domain name, then you can enter only the suffix. For example, you can enter `contoso.com`.

      When you enter this value, user devices can bypass the dynamic trust dialog that's sometimes shown when connecting to the Wi-Fi network.

      On Android 11 and newer, new Wi-Fi profiles may require this setting be configured. Otherwise, the devices may not connect to your Wi-Fi network.

    - **Root certificate for server validation**: Select an existing trusted root certificate profile. When the client connects to the network, this certificate is presented to the server, and authenticates the connection.

    - **Certificates**: Select the SCEP or PKCS client certificate profile that's also deployed to the device. This certificate is the identity presented by the device to the server to authenticate the connection.

    - **Identity privacy (outer identity)**: Enter the text sent in the response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent, and then followed by the real identification sent in a secure tunnel.

  - **PEAP**: Protected Extensible Authentication Protocol (PEAP) encrypts and authenticates using a protected tunnel. Also enter:

    - **Radius server name**: Enter the DNS name that's used in the certificate presented by the Radius Server during client authentication to the Wi-Fi access point. For example, enter `Contoso.com`, `uk.contoso.com`, or `jp.contoso.com`.

      If you have multiple Radius servers with the same DNS suffix in their fully qualified domain name, then you can enter only the suffix. For example, you can enter `contoso.com`.

      When you enter this value, user devices can bypass the dynamic trust dialog that's sometimes shown when connecting to the Wi-Fi network.

      On Android 11 and newer, new Wi-Fi profiles may require this setting be configured. Otherwise, the devices may not connect to your Wi-Fi network.

    - **Root certificate for server validation**: Select an existing trusted root certificate profile. When the client connects to the network, this certificate is presented to the server, and authenticates the connection.

    - **Certificates**: Select the SCEP or PKCS client certificate profile that's also deployed to the device. This certificate is the identity presented by the device to the server to authenticate the connection.

    - **Identity privacy (outer identity)**: Enter the text sent in the response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent, and then followed by the real identification sent in a secure tunnel.

## Next steps

The profile is created, but might not be doing anything. Be sure to [assign this profile](device-profile-assign.md) and [monitor its status.](device-profile-monitor.md).

You can also create Wi-Fi profiles for [Android Enterprise](wi-fi-settings-android-enterprise.md), [iOS/iPadOS](wi-fi-settings-ios.md), [macOS](wi-fi-settings-macos.md), and [Windows 10/11](wi-fi-settings-windows.md).

[Troubleshoot common issues with Wi-Fi profiles](/troubleshoot/mem/intune/troubleshoot-wi-fi-profiles#common-issues).
