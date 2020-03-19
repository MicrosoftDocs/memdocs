---
# required metadata

title: Wi-Fi settings for Windows 10 devices in Microsoft Intune - Azure | Microsoft Docs
description: Add or create Wi-Fi configuration profile using Wi-Fi settings for Windows 10 and later devices in Microsoft Intune. You can configure Basic settings, or enterprise-level settings. 
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.reviewer: tycast
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

# Add Wi-Fi settings for Windows 10 and later devices in Intune

You can create a profile with specific WiFi settings, and then deploy this profile to your Windows 10 and later devices. Microsoft Intune offers many features, including authenticating to your network, using a pre-shared key, and more.

This article describes these settings.

## Before you begin

[Create a device profile](wi-fi-settings-configure.md).

## Basic profile

- **Wi-Fi type**: Choose **Basic**. 

- **Wi-Fi name (SSID)**: Short for service set identifier. This value is the real name of the wireless network that devices connect to. However, users only see the **Connection name** you configure when they choose the connection.

- **Connection name**: Enter a user-friendly name for this Wi-Fi connection. The text you enter is the name users see when they browse the available connections on their device.

- **Connect automatically when in range**: When **Yes**, devices connect automatically when they're in range of this network. When **No**, devices don't automatically connect.

  - **Connect to more preferred network if available**: If the devices are in range of a more preferred network, then choose **Yes** to use the preferred network. Choose **No** to use the Wi-Fi network in this configuration profile.

    For example, you create a **ContosoCorp** Wi-Fi network, and use **ContosoCorp** within this configuration profile. You also have a **ContosoGuest** Wi-Fi network within range. When your corporate devices are within range, you want them to automatically connect to **ContosoCorp**. In this scenario, set the **Connect to more preferred network if available** property to **No**.

  - **Connect to this network, even when it is not broadcasting its SSID**: Choose **Yes** for the configuration profile to automatically connect to your network, even when the network is hidden (meaning, its SSID isn't broadcast publicly). Choose **No** if you don't want this configuration profile to connect to your hidden network.

- **Metered Connection Limit**: An administrator can choose how the network's traffic is metered. Applications can then adjust their network traffic behavior based on this setting. Your options:

  - **Unrestricted**: Default. The connection isn't metered and there are no restrictions on traffic.
  - **Fixed**: Use this option if the network is configured with fixed limit for network traffic. After this limit is reached, network access is prohibited.
  - **Variable**: Used this option if network traffic is charged per byte (cost per byte).

- **Wireless Security Type**: Enter the security protocol used to authenticate devices on your network. Your options are:
  - **Open (no authentication)**: Only use this option if the network is unsecured.
  - **WPA/WPA2-Personal**: A more secure option, and is commonly used for Wi-Fi connectivity. For more security, you can also enter a pre-shared key password or network key.

    - **Pre-shared key** (PSK): Optional. Shown when you choose **WPA/WPA2-Personal** as the security type. When your organization's network is set up or configured, a password or network key is also configured. Enter this password or network key for the PSK value. Enter a string between 8-64 characters. If your password or network key is 64 characters, enter hexadecimal characters.

      > [!NOTE]
      > When you save the Wi-Fi profile, the PSK value you entered isn't shown for security reasons. The pre-shared key watermark still shows **Not configured** even though the PSK is saved in the profile. To change the PSK, enter a new key, and save the profile. If you save a PSK, edit the policy, and leave the PSK blank, then the existing PSK is still used.
      > [!IMPORTANT]
      > The PSK is the same for all devices you target the profile to. If the key is compromised, it can be used by any device to connect to the Wi-Fi network. Keep your PSKs secure to avoid unauthorized access.

- **Company Proxy settings**: Choose to use the proxy settings within your organization. Your options:
  - **None**: No proxy settings are configured.
  - **Manually configure**: Enter the **Proxy server IPaddress** and its **Port number**.
  - **Automatically configure**: Enter the URL pointing to a proxy autoconfiguration (PAC) script. For example, enter `http://proxy.contoso.com/proxy.pac`.

Select **OK** > **Create** to save your changes. The profile is created and is shown in the profiles list.

## Enterprise profile

- **Wi-Fi type**: Choose **Enterprise**.

- **Wi-Fi name (SSID)**: Short for service set identifier. This value is the real name of the wireless network that devices connect to. However, users only see the **Connection name** you configure when they choose the connection.

- **Connection name**: Enter a user-friendly name for this Wi-Fi connection. The text you enter is the name users see when they browse the available connections on their device.

- **Connect automatically when in range**: When **Yes**, devices connect automatically when they're in range of this network. When **No**, devices don't automatically connect.
  - **Connect to more preferred network if available**: If the devices are in range of a more preferred network, then choose **Yes** to use the preferred network. Choose **No** to use the Wi-Fi network in this configuration profile.

    For example, you create a **ContosoCorp** Wi-Fi network, and use **ContosoCorp** within this configuration profile. You also have a **ContosoGuest** Wi-Fi network within range. When your corporate devices are within range, you want them to automatically connect to **ContosoCorp**. In this scenario, set the **Connect to more preferred network if available** property to **No**.

  - **Connect to this network, even when it is not broadcasting its SSID**: Choose **Yes** for the configuration profile to automatically connect to your network, even when the network is hidden (meaning, its SSID isn't broadcast publicly). Choose **No** if you don't want this configuration profile to connect to your hidden network.

- **Metered Connection Limit**: An administrator can choose how the network's traffic is metered. Applications can then adjust their network traffic behavior based on this setting. Your options:

  - **Unrestricted**: Default. The connection isn't metered and there are no restrictions on traffic.
  - **Fixed**: Use this option if the network is configured with fixed limit for network traffic. After this limit is reached, network access is prohibited.
  - **Variable**: Used this option if network traffic is costed per byte.

- **Single sign-on (SSO)**: Allows you to configure single sign-on (SSO), where credentials are shared for computer and Wi-Fi network sign-in. Your options are:
  - **Disable**: Disables SSO behavior. The user needs to authenticate to the network separately.
  - **Enable before user signs into device**: Use SSO to authenticate to the network just before the user sign-in process.
  - **Enable after user signs into device**: Use SSO to authenticate to the network immediately after the user sign-in process completes.
  - **Maximum time to authenticate before timeout**: Enter the maximum number of seconds to wait before authenticating to the network, from 1-120 seconds.
  - **Allow Windows to prompt user for additional authentication credentials**: Choosing **Yes** allows the Windows system to prompt the user for additional credentials if the authentication method requires it. Choose **No** to hide these prompts.

- **Enable pairwise master key (PMK) caching**: Select **Yes** to cache the PMK used in authentication. This caching typically allows authentication to the network to complete faster. Choose **No** to force the authentication handshake when connecting to the Wi-Fi network every time.

  - **Maximum time a PMK is stored in cache**: Enter the number of minutes a pairwise master key (PMK) is stored in the cache, from 5-1440 minutes.
  - **Maximum number of PMKs stored in cache**: Enter the number of keys stored in cache, from 1-255.

- **Enable pre-authentication**: Pre-authentication allows the profile to authenticate to all access points for the network in the profile before connecting. When moving between access points, pre-authentication reconnects the user or devices more quickly. Choose **Yes** for the profile to authenticate to all access points for this network that are within range. Choose **No** to require the user or device to authenticate to each access point separately.

  - **Maximum pre-authentication attempts**: Enter the number of tries to preauthenticate, from 1-16.

- **EAP type**: Choose the Extensible Authentication Protocol (EAP) type to authenticate secured wireless connections. Your options:

  - **EAP-SIM**
  - **EAP-TLS**
  - **EAP-TTLS**
  - **Protected PEAP** (PEAP)

    **EAP-TLS, EAP-TTLS, and PEAP additional settings**:
    
    > [!NOTE]
    > Currently, only SCEP certificate profiles are supported when using an EAP type. PKCS certificate profiles are not supported. Anytime a user is asked to enter a certificate, be sure to choose an SCEP certificate.

    - **Server Trust**  

      **Certificate server names**: Use with **EAP-TLS**, **EAP-TTLS**, or **PEAP** EAP types. Enter one or more common names used in the certificates issued by your trusted certificate authority (CA). If you enter this information, you can bypass the dynamic trust dialog shown on user devices when they connect to this Wi-Fi network.  

      **Root certificate for server validation**: Use with **EAP-TLS**, **EAP-TTLS**, or **PEAP** EAP types. Choose the trusted root certificate profile used to authenticate the connection.  

      **Identity privacy (outer identity)**: Use with **PEAP** EAP type. Enter the text sent in response to an EAP identity request. This text can be any value. During authentication, this anonymous identity is initially sent, and then followed by the real identification sent in a secure tunnel.  

    - **Client Authentication**

      **Client certificate for client authentication (Identity certificate)**: Use with **EAP-TLS** EAP type. Choose the certificate profile used to authenticate the connection.

      **Authentication method**: Use with **EAP-TTLS** EAP type. Select the authentication method for the connection:  

      - **Certificates**: Select the client certificate that is the identity certificate presented to the server.
      - **Username and Password**: Enter a **Non-EAP method (inner identity)** method for authentication. Your options:

        - **Unencrypted password (PAP)**
        - **Challenge Handshake (CHAP)**
        - **Microsoft CHAP (MS-CHAP)**
        - **Microsoft CHAP Version 2 (MS-CHAP v2)**

      **Identity privacy (outer identity)**: Use with **EAP-TTLS** EAP type. Enter the text sent in response to an EAP identity request. This text can be any value. During authentication, this anonymous identity is initially sent, and then followed by the real identification sent in a secure tunnel.

- **Company Proxy settings**: Choose to use the proxy settings within your organization. Your options:
  - **None**: No proxy settings are configured.
  - **Manually configure**: Enter the **Proxy server IPaddress** and its **Port number**.
  - **Automatically configure**: Enter the URL pointing to a proxy auto-configuration (PAC) script. For example, enter `http://proxy.contoso.com/proxy.pac`.

- **Force Wi-Fi profile to be compliant with the Federal Information Processing Standard (FIPS)**: Choose **Yes** when validating against the FIPS 140-2 standard. This standard is required for all US federal government agencies that use cryptography-based security systems to protect sensitive but unclassified information stored digitally. Choose **No** to not be FIPS-compliant.

Select **OK** > **Create** to save your changes. The profile is created and is shown in the profiles list.

## Use an imported settings file

For any settings not available in Intune, you can export Wi-Fi settings from another Windows device. This export creates an XML file with all the settings. Then, import this file in to Intune, and use it as the Wi-Fi profile. See [Export and import Wi-Fi settings for Windows devices](wi-fi-settings-import-windows-8-1.md).

## Next steps

The profile is created, but it's not doing anything. Next, [assign this profile](device-profile-assign.md).

## More resources

- See the settings available for [Windows 8.1](wi-fi-settings-import-windows-8-1.md).
- [Wi-Fi settings overview](wi-fi-settings-configure.md), including other platforms.
