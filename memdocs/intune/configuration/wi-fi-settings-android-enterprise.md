---
# required metadata

title: Wi-Fi settings for Android Enterprise and kiosk devices - Microsoft Intune | Microsoft Docs
description: Create or add a WiFi device configuration profile for Android Enterprise and Android Kiosk. See the different settings, add certificates, choose an EAP type, and select an authentication method in Microsoft Intune. For kiosk devices, also enter the Pre-shared key of your network.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/18/2024
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium

# optional metadata

#ROBOTS:
#audience:
params:
  siblings_only: true
ms.reviewer: abalwan
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.collection:
- tier3
- M365-identity-device-management
---

# Add Wi-Fi settings for Android Enterprise dedicated and fully managed devices in Microsoft Intune

You can create a profile with specific Wi-Fi settings, and then deploy this profile to your Android Enterprise fully managed and dedicated devices. Microsoft Intune offers many features, including authenticating to your network, using a pre-shared key, and more.

This feature applies to:

- Android Enterprise personally owned devices with a work profile (BYOD)
- Android Enterprise corporate owned work profile (COPE)
- Android Enterprise corporate owned fully managed (COBO)
- Android Enterprise corporate owned dedicated devices (COSU)

This article describes these settings. [Use Wi-Fi on your devices](wi-fi-settings-configure.md) includes more information about the Wi-Fi feature in Microsoft Intune.

## Before you begin

Create an [Android Enterprise Wi-Fi device configuration profile](wi-fi-settings-configure.md):

- Fully managed, dedicated, and corporate-owned work profile
- Personally owned work profile

## Fully Managed, Dedicated, and Corporate-Owned Work Profile

Select this option if you're deploying to an Android Enterprise dedicated, corporate-owned work profile, or fully managed device.

### Basic

- **Wi-Fi type**: Select **Basic**.
- **Network name**: Enter a name for this Wi-Fi connection. End users see this name when they browse their device for available Wi-Fi connections. For example, enter **Contoso WiFi**.
- **SSID**: Enter the **service set identifier**, which is the real name of the wireless network that devices connect to. However, users only see the **network name** you configured when they choose the connection.

  > [!IMPORTANT]
  > - You can't target two Wi-Fi profiles with the same SSID to the same device. So, make sure any new Wi-Fi profiles use a different SSID.
  > - If you plan to change the Trusted Root Certificate of a Wi-Fi profile, before you change the certificate, make sure the device connects to another internet connection. The backup internet connection allows the Wi-Fi profile with the updated certificate to be assigned. In a future update (no ETA), Intune will support multiple trusted root certificates in Wi-Fi profile. Then, a second internet connection isn't needed.

- **Connect automatically**: **Enable** automatically connects to your Wi-Fi network when devices are in range. Select **Disable** to prevent or block this automatic connection.

  When devices are connected to another preferred Wi-Fi connection, then they don't automatically connect to this Wi-Fi network. If devices fail to connect automatically when this setting is enabled, then disconnect the devices from any existing Wi-Fi connections.

- **Hidden network**: Select **Enable** to hide this network from the list of available networks on the device. The SSID isn't broadcasted. Select **Disable** to show this network in the list of available networks on the device.
- **Wi-Fi type**: Select the security protocol to authenticate to the Wi-Fi network. Your options:

  - **Open (no authentication)**: Only use this option if the network is unsecured.
  - **WEP-Pre-shared key**: Enter the password in **Pre-shared key**. When your organization's network is set up or configured, a password or network key is also configured. Enter this password or network key for the PSK value.

    > [!WARNING]
    > On Android 12 and later, Google deprecated support for WEP pre-shared keys (PSK) in Wi-Fi configuration profiles. It's possible WEP might still work. But, it's not recommended and is considered obsolete. Instead, use WPA pre-shared keys (PSK) in your Wi-Fi configuration profiles.
    >
    > For more information, go to the [Android developer reference - WifiConfiguration.GroupCipher](https://developer.android.com/reference/android/net/wifi/WifiConfiguration.GroupCipher#summary).

  - **WPA-Pre-shared key**: Enter the password in **Pre-shared key**. When your organization's network is set up or configured, a password or network key is also configured. Enter this password or network key for the PSK value.

- **Proxy settings**: Select a proxy configuration. Your options:

  - **None**: No proxy settings are configured.
  - **Manual**: Manually configure the proxy settings:
    - **Proxy server address**: Enter the IP address of the proxy server. For example, enter `10.0.0.22`.
    - **Port number**: Enter the port number of the proxy server. For example, enter `8080`.
    - **Exclusion list**:  Enter a hostname or IP address that won't use the proxy. You can use the `*` wildcard character and enter multiple host names and IP addresses. If you enter multiple host names or IP addresses, they must be on a separate line. For example, you can enter:

      ```string
      *.contoso.com
      test.contoso1.com
      mysite.contoso2.com
      10.0.0.5
      10.0.0.6
      ```

  - **Automatic**: Use a file to configure the proxy server. Enter the **Proxy server URL** that contains the configuration file. For example, enter `http://proxy.contoso.com`, `10.0.0.11`, or `http://proxy.contoso.com/proxy.pac`.

    For more information on PAC files, see [Proxy Auto-Configuration (PAC) file](https://developer.mozilla.org/docs/Web/HTTP/Proxy_servers_and_tunneling/Proxy_Auto-Configuration_(PAC)_file) (opens a non-Microsoft site).

- **MAC address randomization**: Use random MAC addresses when needed, such as for network access control (NAC) support. Users can change this setting.

  Your options:

  - **Use device default**: Intune doesn't change or update this setting. By default, when devices connect to a network, the devices present a randomized MAC address instead of the physical MAC address. Any updates made by the user to the setting persist.

  - **Use randomized MAC**: Enables MAC address randomization on devices. When devices connect to a new network, the devices present a randomized MAC address, instead of the physical MAC address. If the user changes this value on their device, it resets to **Use randomized MAC** on the next Intune sync.

  - **Use device MAC**: Forces devices to present their actual Wi-Fi MAC address instead of a random MAC address. With this setting, devices are tracked by their MAC address. Only use this value when necessary, such as for network access control (NAC) support. If the user changes this value on their device, it resets to **Use device MAC** on the next Intune sync.

  This feature applies to:

  - Android 13 and later

### Enterprise

- **Wi-Fi type**: Select **Enterprise**.
- **SSID**: Enter the **service set identifier**, which is the real name of the wireless network that devices connect to. However, users only see the **network name** you configured when they choose the connection.

  > [!IMPORTANT]
  > - You can't target two Wi-Fi profiles with the same SSID to the same device. So, make sure any new Wi-Fi profiles use a different SSID.
  > - If you plan to change the Trusted Root Certificate of a Wi-Fi profile, before you change the certificate, make sure the device connects to another internet connection. The backup internet connection allows the Wi-Fi profile with the updated certificate to be assigned. In a future update (no ETA), Intune will support multiple trusted root certificates in Wi-Fi profile. Then, a second internet connection isn't needed.

- **Connect automatically**: **Enable** automatically connects to your Wi-Fi network when devices are in range. Select **Disable** to prevent or block this automatic connection.

  When devices are connected to another preferred Wi-Fi connection, then they don't automatically connect to this Wi-Fi network. If devices fail to connect automatically when this setting is enabled, then disconnect the devices from any existing Wi-Fi connections.

- **Hidden network**: Select **Enable** to hide this network from the list of available networks on the device. The SSID isn't broadcasted. Select **Disable** to show this network in the list of available networks on the device.
- **EAP type**: Select the Extensible Authentication Protocol (EAP) type used to authenticate secured wireless connections. Your options:

  - **EAP-TLS**: To authenticate, the Extensible Authentication Protocol (EAP) Transport Layer Security (TLS) uses a digital certificate on the server, and a digital certificate on the client. Both certificates are signed by a certificate authority (CA) that the server and client trust.

    Also enter:

    - **Radius server name**: During client authentication to the Wi-Fi access point, the Radius Server presents a certificate. Enter the DNS name of this certificate. For example, enter `Contoso.com`, `uk.contoso.com`, or `jp.contoso.com`.

      If you have multiple Radius servers with the same DNS suffix in their fully qualified domain name, then you can enter only the suffix. For example, you can enter `contoso.com`.

      When you enter this value, user devices can bypass the dynamic trust dialog that can be shown when connecting to the Wi-Fi network.

      - **Android 11 and newer**: New Wi-Fi profiles might require this setting be configured. Otherwise, the devices might not connect to your Wi-Fi network.

      - **Android 14 and newer**: Google doesn't alllow the total content length of all the Radius servers to be greater than 256 characters or to include special characters. If you have multiple Radius servers with the same DNS suffix in their fully qualified domain name, then we recommend you enter only the suffix.

    - **Root certificate for server validation**: Select an existing trusted root certificate profile. When the client connects to the network, this certificate is used to establish a chain of trust with the server. If your authentication server uses a public certificate, then you don't need to include a root certificate.

      > [!NOTE]
      > Depending on your Android OS version and your Wi-Fi authentication infrastructure, the certificate requirements can vary. You might need to add your secure hash algorithm(s) (SHA) from the certificate used by your network policy server (NPS). Or, if your Radius or NPS server has a publicly signed certificate, then a root certificate might not be needed for validation.
      >
      > A good practice is to enter the **Radius server name** and add a **Root certificate for server validation**.

    - **Authentication method**: Select the authentication method used by your device clients. Your options:
      - **Derived credential**: Use a certificate that's derived from a user's smart card. If no derived credential issuer is configured, Intune prompts you to add one. For more information, see [Use derived credentials in Microsoft Intune](../protect/derived-credentials.md).
      - **Certificates**: Select the SCEP or PKCS client certificate profile that is also deployed to the device. This certificate is the identity presented by the device to the server to authenticate the connection.

    - **Identity privacy (outer identity)**: Enter the text sent in the response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent. Then, the real identification is sent in a secure tunnel​​.​

  - **EAP-TTLS**: To authenticate, the Extensible Authentication Protocol (EAP) Tunneled Transport Layer Security (TTLS) uses a digital certificate on the server. When the client makes the authentication request, the server uses the tunnel, which is a secure connection, to complete the authentication request.

    Also enter:

    - **Radius server name**: During client authentication to the Wi-Fi access point, the Radius Server presents a certificate. Enter the DNS name of this certificate. For example, enter `Contoso.com`, `uk.contoso.com`, or `jp.contoso.com`.

      If you have multiple Radius servers with the same DNS suffix in their fully qualified domain name, then you can enter only the suffix. For example, you can enter `contoso.com`.

      When you enter this value, user devices can bypass the dynamic trust dialog that can be shown when connecting to the Wi-Fi network.

      - **Android 11 and newer**: New Wi-Fi profiles might require this setting be configured. Otherwise, the devices might not connect to your Wi-Fi network.

      - **Android 14 and newer**: Google doesn't alllow the total content length of all the Radius servers to be greater than 256 characters or to include special characters. If you have multiple Radius servers with the same DNS suffix in their fully qualified domain name, then we recommend you enter only the suffix.

    - **Root certificate for server validation**: Select one or more existing trusted root certificate profiles. When the client connects to the network, these certificates are used to establish a chain of trust with the server. If your authentication server uses a public certificate, then you don't need to include a root certificate.

    - **Authentication method**: Select the authentication method used by your device clients. Your options:

      - **Derived credential**: Use a certificate that's derived from a user's smart card. If no derived credential issuer is configured, Intune prompts you to add one. For more information, see [Use derived credentials in Microsoft Intune](../protect/derived-credentials.md).
      - **Username and Password**: Prompt the user for a user name and password to authenticate the connection. Also enter:
        - **Non-EAP method (inner identity)**: Choose how you authenticate the connection. Be sure you select the same protocol that's configured on your Wi-Fi network. Your options:

          - **Unencrypted password (PAP)**
          - **Microsoft CHAP (MS-CHAP)**
          - **Microsoft CHAP Version 2 (MS-CHAP v2)**

      - **Certificates**: Select the SCEP or PKCS client certificate profile that is also deployed to the device. This certificate is the identity presented by the device to the server to authenticate the connection.

      - **Identity privacy (outer identity)**: Enter the text sent in the response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent. Then, the real identification is sent in a secure tunnel​​.

  - **PEAP**: Protected Extensible Authentication Protocol (PEAP) encrypts and authenticates using a protected tunnel. Also enter:

    - **Radius server name**: During client authentication to the Wi-Fi access point, the Radius Server presents a certificate. Enter the DNS name of this certificate. For example, enter `Contoso.com`, `uk.contoso.com`, or `jp.contoso.com`.

      If you have multiple Radius servers with the same DNS suffix in their fully qualified domain name, then you can enter only the suffix. For example, you can enter `contoso.com`.

      When you enter this value, user devices can bypass the dynamic trust dialog that can be shown when connecting to the Wi-Fi network.

      - **Android 11 and newer**: New Wi-Fi profiles might require this setting be configured. Otherwise, the devices might not connect to your Wi-Fi network.

      - **Android 14 and newer**: Google doesn't alllow the total content length of all the Radius servers to be greater than 256 characters or to include special characters. If you have multiple Radius servers with the same DNS suffix in their fully qualified domain name, then we recommend you enter only the suffix.

    - **Root certificate for server validation**: Select one or more existing trusted root certificate profiles. When the client connects to the network, these certificates are used to establish a chain of trust with the server. If your authentication server uses a public certificate, then you don't need to include a root certificate.

    - **Authentication method**: Select the authentication method used by your device clients. Your options:

      - **Derived credential**: Use a certificate that's derived from a user's smart card. If no derived credential issuer is configured, Intune prompts you to add one. For more information, see [Use derived credentials in Microsoft Intune](../protect/derived-credentials.md).
      - **Username and Password**: Prompt the user for a user name and password to authenticate the connection. Also enter:
        - **Non-EAP method for authentication (inner identity)**: Choose how you authenticate the connection. Be sure you select the same protocol that's configured on your Wi-Fi network. Your options:

          - **None**
          - **Microsoft CHAP Version 2 (MS-CHAP v2)**

      - **Certificates**: Select the SCEP or PKCS client certificate profile that is also deployed to the device. This certificate is the identity presented by the device to the server to authenticate the connection.

      - **Identity privacy (outer identity)**: Enter the text sent in the response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent. Then, the real identification is sent in a secure tunnel​​.

- **Proxy settings**: Select a proxy configuration. Your options:

  - **None**: No proxy settings are configured.
  - **Manual**: Manually configure the proxy settings:
    - **Proxy server address**: Enter the IP address of the proxy server. For example, enter `10.0.0.22`.
    - **Port number**: Enter the port number of the proxy server. For example, enter `8080`.
    - **Exclusion list**:  Enter a hostname or IP address that won't use the proxy. You can use the `*` wildcard character and enter multiple host names and IP addresses. If you enter multiple host names or IP addresses, they must be on a separate line. For example, you can enter:

      ```string
      *.contoso.com
      test.contoso1.com
      mysite.contoso2.com
      10.0.0.5
      10.0.0.6
      ```

  - **Automatic**: Use a file to configure the proxy server. Enter the **Proxy server URL** that contains the configuration file. For example, enter `http://proxy.contoso.com`, `10.0.0.11`, or `http://proxy.contoso.com/proxy.pac`.

    For more information on PAC files, see [Proxy Auto-Configuration (PAC) file](https://developer.mozilla.org/docs/Web/HTTP/Proxy_servers_and_tunneling/Proxy_Auto-Configuration_(PAC)_file) (opens a non-Microsoft site).

    > [!NOTE]
    > When a device is marked as corporate during enrollment (organization-owned), policies control device features and settings. Users can be prevented from managing features and settings in the policy.
    > When a Wi-Fi policy is assigned to devices, then Wi-Fi is enabled, and users can be prevented from turning off Wi-Fi.

- **MAC address randomization**: Use random MAC addresses when needed, such as for network access control (NAC) support. Users can change this setting.

  Your options:

  - **Use device default**: Intune doesn't change or update this setting. By default, when devices connect to a network, the devices present a randomized MAC address instead of the physical MAC address. Any updates made by the user to the setting persist.

  - **Use randomized MAC**: Enables MAC address randomization on devices. When devices connect to a new network, the devices present a randomized MAC address, instead of the physical MAC address. If the user changes this value on their device, it resets to **Use randomized MAC** on the next Intune sync.

  - **Use device MAC**: Forces devices to present their actual Wi-Fi MAC address instead of a random MAC address. With this setting, devices are tracked by their MAC address. Only use this value when necessary, such as for network access control (NAC) support. If the user changes this value on their device, it resets to **Use device MAC** on the next Intune sync.

  This feature applies to:

  - Android 13 and later

## Personally owned work profile

### Basic (personally owned work profile)

- **Wi-Fi type**: Select **Basic**.
- **SSID**: Enter the **service set identifier**, which is the real name of the wireless network that devices connect to. However, users only see the **network name** you configured when they choose the connection.
- **Hidden network**: Select **Enable** to hide this network from the list of available networks on the device. The SSID isn't broadcasted. Select **Disable** to show this network in the list of available networks on the device.

### Enterprise (personally owned work profile)

- **Wi-Fi type**: Select **Enterprise**.
- **SSID**: Enter the **service set identifier**, which is the real name of the wireless network that devices connect to. However, users only see the **network name** you configured when they choose the connection.
- **Hidden network**: Select **Enable** to hide this network from the list of available networks on the device. The SSID isn't broadcasted. Select **Disable** to show this network in the list of available networks on the device.
- **EAP type**: Select the Extensible Authentication Protocol (EAP) type used to authenticate secured wireless connections. Your options:

  - **EAP-TLS**: Also enter:  
  
    - **Certificate server names**: **Add** one or more common names used in the certificates issued by your trusted certificate authority (CA) to your wireless network access servers. For example, add `mywirelessserver.contoso.com` or `mywirelessserver`. When you enter this information, you can bypass the dynamic trust window displayed on user's devices when they connect to this Wi-Fi network.  

    - **Root certificate for server validation**: Select one or more existing trusted root certificate profiles. When the client connects to the network, these certificates are used to establish a chain of trust with the server. If your authentication server uses a public certificate, then you don't need to include a root certificate.

    - **Certificates**: Select the SCEP or PKCS client certificate profile that is also deployed to the device. This certificate is the identity presented by the device to the server to authenticate the connection.

    - **Identity privacy (outer identity)**: Enter the text sent in the response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent. Then, the real identification is sent in a secure tunnel​​.

  - **EAP-TTLS**: Also enter:

    - **Root certificate for server validation**: Select one or more existing trusted root certificate profiles. When the client connects to the network, these certificates are used to establish a chain of trust with the server. If your authentication server uses a public certificate, then you don't need to include a root certificate.

    - **Authentication method**: Select the authentication method used by your device clients. Your options:

      - **Username and Password**: Prompt the user for a user name and password to authenticate the connection. Also enter:
        - **Non-EAP method (inner identity)**: Choose how you authenticate the connection. Be sure you select the same protocol that's configured on your Wi-Fi network. Your options:

          - **Unencrypted password (PAP)**
          - **Microsoft CHAP (MS-CHAP)**
          - **Microsoft CHAP Version 2 (MS-CHAP v2)**

      - **Certificates**: Select the SCEP or PKCS client certificate profile that is also deployed to the device. This certificate is the identity presented by the device to the server to authenticate the connection.

      - **Identity privacy (outer identity)**: Enter the text sent in the response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent. Then, the real identification is sent in a secure tunnel​​.

  - **PEAP**: Also enter:

    - **Root certificate for server validation**: Select an existing trusted root certificate profile. When the client connects to the network, this certificate is presented to the server, and authenticates the connection.

    - **Authentication method**: Select the authentication method used by your device clients. Your options:

      - **Username and Password**: Prompt the user for a user name and password to authenticate the connection. Also enter:
        - **Non-EAP method for authentication (inner identity)**: Choose how you authenticate the connection. Be sure you select the same protocol that's configured on your Wi-Fi network. Your options:

          - **None**
          - **Microsoft CHAP Version 2 (MS-CHAP v2)**

      - **Certificates**: Select the SCEP or PKCS client certificate profile that is also deployed to the device. This certificate is the identity presented by the device to the server to authenticate the connection.

      - **Identity privacy (outer identity)**: Enter the text sent in the response to an EAP identity request. This text can be any value, such as `anonymous`. During authentication, this anonymous identity is initially sent. Then, the real identification is sent in a secure tunnel​​.

- **Proxy settings**: Select a proxy configuration. Your options:

  - **None**: No proxy settings are configured.
  - **Automatic**: Use a file to configure the proxy server. Enter the **Proxy server URL** that contains the configuration file. For example, enter `http://proxy.contoso.com`, `10.0.0.11`, or `http://proxy.contoso.com/proxy.pac`.

    For more information on PAC files, see [Proxy Auto-Configuration (PAC) file](https://developer.mozilla.org/docs/Web/HTTP/Proxy_servers_and_tunneling/Proxy_Auto-Configuration_(PAC)_file) (opens a non-Microsoft site).

## Related articles

- The profile is created, but might not be doing anything. Be sure to [assign this profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).

- You can also create Wi-Fi profiles for [Android](wi-fi-settings-android.md), [iOS/iPadOS](wi-fi-settings-ios.md), [macOS](wi-fi-settings-macos.md), and [Windows](wi-fi-settings-windows.md).

- [Troubleshoot common issues with Wi-Fi profiles](/troubleshoot/mem/intune/troubleshoot-wi-fi-profiles#common-issues).
