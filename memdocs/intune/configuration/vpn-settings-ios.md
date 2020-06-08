---
# required metadata

title: Configure VPN settings to iOS/iPadOS devices in Microsoft Intune - Azure | Microsoft Docs
description: Add or create a VPN configuration profile on iOS/iPadOS devices using virtual private network (VPN) configuration settings. Configure the connection details, authentication methods, split tunneling, custom VPN settings with the identifier, key and value pairs, per-app VPN settings that include Safari URLs, and on-demand VPNs with SSIDs or DNS search domains, proxy settings to include a configuration script, IP or FQDN address, and TCP port in Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/08/2020
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

# Add VPN settings on iOS and iPadOS devices in Microsoft Intune

Microsoft Intune includes many VPN settings that can be deployed to your iOS/iPadOS devices. These settings are used to create and configure VPN connections to your organization's network. This article describes these settings. Some settings are only available for some VPN clients, such as Citrix, Zscaler, and more.

## Before you begin

[Create a device configuration profile](vpn-settings-configure.md).

> [!NOTE]
> These settings are available for all enrollment types. For more information on the enrollment types, see [iOS/iPadOS enrollment](../enrollment/ios-enroll.md).

## Connection type

Select the VPN connection type from the following list of vendors:

- **Check Point Capsule VPN**
- **Cisco Legacy AnyConnect**: Applicable to [Cisco Legacy AnyConnect](https://itunes.apple.com/app/cisco-legacy-anyconnect/id392790924) app version 4.0.5x and earlier.
- **Cisco AnyConnect**: Applicable to [Cisco AnyConnect](https://itunes.apple.com/app/cisco-anyconnect/id1135064690) app version 4.0.7x and later.
- **SonicWall Mobile Connect**
- **F5 Access Legacy**: Applicable to F5 Access app version 2.1 and earlier.
- **F5 Access**: Applicable to F5 Access app version 3.0 and later.
- **Palo Alto Networks GlobalProtect (Legacy)**: Applicable to Palo Alto Networks GlobalProtect app version 4.1 and earlier.
- **Palo Alto Networks GlobalProtect**: Applicable to Palo Alto Networks GlobalProtect app version 5.0 and later.
- **Pulse Secure**
- **Cisco (IPSec)**
- **Citrix VPN**
- **Citrix SSO**
- **Zscaler**: To use Conditional Access, or allow users to bypass the Zscaler sign in screen, then you must integrate Zscaler Private Access (ZPA) with your Azure AD account. For detailed steps, see the [Zscaler documentation](https://help.zscaler.com/zpa/configuration-guide-microsoft-azure-ad).
- **IKEv2**: [IKEv2 settings](#ikev2-settings) (in this article) describes the properties.
- **Custom VPN**

> [!NOTE]
> Cisco, Citrix, F5, and Palo Alto have announced that their legacy clients don't work on iOS 12. You should migrate to the new apps as soon as possible. For more information, see the [Microsoft Intune Support Team Blog](https://go.microsoft.com/fwlink/?linkid=2013806&clcid=0x409).

## Base VPN settings

The settings shown in the following list are determined by the VPN connection type you choose.  

- **Connection name**: End users see this name when they browse their device for a list of available VPN connections.
- **Custom domain name** (Zscaler only): Prepopulate the Zscaler app's sign in field with the domain your users belong to. For example, if a username is `Joe@contoso.net`, then the `contoso.net` domain statically appears in the field when the app opens. If you don't enter a domain name, then the domain portion of the UPN in Azure Active Directory (AD) is used.
- **IP address or FQDN**: The IP address or fully qualified domain name (FQDN) of the VPN server that devices connect with. For example, enter `192.168.1.1` or `vpn.contoso.com`.
- **Organization's cloud name** (Zscaler only): Enter the cloud name where your organization is provisioned. The URL you use to sign in to Zscaler has the name.  
- **Authentication method**: Choose how devices authenticate to the VPN server. 
  - **Certificates**: Under **Authentication certificate**, select an existing SCEP or PKCS certificate profile to authenticate the connection. [Configure certificates](../protect/certificates-configure.md) provides some guidance about certificate profiles.
  - **Username and password**: End users must enter a username and password to sign in to the VPN server.  

    > [!NOTE]
    > If username and password are used as the authentication method for Cisco IPsec VPN, they must deliver the SharedSecret through a custom Apple Configurator profile.

  - **Derived credential**: Use a certificate that's derived from a user's smart card. If no derived credential issuer is configured, Intune prompts you to add one. For more information, see [Use derived credentials in Microsoft Intune](../protect/derived-credentials.md).

- **Excluded URLs** (Zscaler only): When connected to the Zscaler VPN, the listed URLs are accessible outside the Zscaler cloud. 

- **Split tunneling**: **Enable** or **Disable** to let devices decide which connection to use, depending on the traffic. For example, a user in a hotel uses the VPN connection to access work files, but uses the hotel's standard network for regular web browsing.

- **VPN identifier** (Custom VPN, Zscaler, and Citrix): An identifier for the VPN app you're using, and is supplied by your VPN provider.
- **Enter key/value pairs for your organization's custom VPN attributes** (Custom VPN, Zscaler, and Citrix): Add or import **Keys** and **Values** that customize your VPN connection. Remember, these values are typically supplied by your VPN provider.

- **Enable network access control (NAC)** (Cisco AnyConnect, Citrix SSO, F5 Access): When you choose **I agree**, the device ID is included in the VPN profile. This ID can be used for authentication to the VPN to allow or prevent network access.

  **When using Cisco AnyConnect with ISE**, be sure to:

  - If you haven't already, integrate ISE with Intune for NAC as described at **Configure Microsoft Intune as an MDM Server** in the [Cisco Identity Services Engine Administrator Guide](https://www.cisco.com/c/en/us/td/docs/security/ise/2-1/admin_guide/b_ise_admin_guide_21/b_ise_admin_guide_20_chapter_01000.html).
  - Enable NAC in the VPN profile.

  **When using Citrix SSO with Gateway**, be sure to:

  - Confirm you're using Citrix Gateway 12.0.59 or higher.
  - Confirm your users have Citrix SSO 1.1.6 or later installed on their devices.
  - Integrate Citrix Gateway with Intune for NAC. See the [Integrating Microsoft Intune/Enterprise Mobility Suite with NetScaler (LDAP+OTP Scenario)](https://www.citrix.com/content/dam/citrix/en_us/documents/guide/integrating-microsoft-intune-enterprise-mobility-suite-with-netscaler.pdf) Citrix deployment guide.
  - Enable NAC in the VPN profile.

  **When using F5 Access**, be sure to:

  - Confirm you're using F5 BIG-IP 13.1.1.5 or later. 
  - Integrate BIG-IP with Intune for NAC. See the [Overview: Configuring APM for device posture checks with endpoint management systems](https://support.f5.com/kb/en-us/products/big-ip_apm/manuals/product/apm-client-configuration-7-1-6/6.html#guid-0bd12e12-8107-40ec-979d-c44779a8cc89) F5 guide.
  - Enable NAC in the VPN profile.

  For the VPN partners that support device ID, the VPN client, such as Citrix SSO, can get the ID. Then, it can query Intune to confirm the device is enrolled, and if the VPN profile is compliant or not compliant.

  - To remove this setting, recreate the profile, and don't select **I agree**. Then, reassign the profile.

## IKEv2 settings

These settings apply when you choose **Connection type** > **IKEv2**.

- **Always-on VPN**: **Enable** sets a VPN client to automatically connect and reconnect to the VPN. Always-on VPN connections stay connected or immediately connect when the user locks their device, the device restarts, or the wireless network changes. When set to **Disable** (default), always-on VPN for all VPN clients is disabled. When enabled, also configure:

  - **Network interface**: All IKEv2 settings only apply to the network interface you choose. Your options:
    - **Wi-Fi and Cellular** (default): The IKEv2 settings apply to the Wi-Fi and cellular interfaces on the device.
    - **Cellular**: The IKEv2 settings only apply to the cellular interface on the device. Select this option if you're deploying to devices with the Wi-Fi interface disabled or removed.
    - **Wi-Fi**: The IKEv2 settings only apply to the Wi-Fi interface on the device.
  - **User to disable VPN configuration**: **Enable** lets users turn off always-on VPN. **Disable** (default) prevents users from turning it off.​ The default value for this setting is the most secure option.
  - **Voicemail**: Choose what happens with voicemail traffic when always-on VPN is enabled. Your options:
    - **Force network traffic through VPN** (default): This setting is the most secure option.
    - **Allow network traffic to pass outside VPN**
    - **Drop network traffic**
  - **AirPrint**: Choose what happens with AirPrint traffic when always-on VPN is enabled. Your options:
    - **Force network traffic through VPN** (default): This setting is the most secure option.
    - **Allow network traffic to pass outside VPN**
    - **Drop network traffic**
  - **Cellular services**: On iOS 13.0+, choose what happens with cellular traffic when always-on VPN is enabled. Your options:
    - **Force network traffic through VPN** (default): This setting is the most secure option.
    - **Allow network traffic to pass outside VPN**
    - **Drop network traffic**
  - **Allow traffic from non-native captive networking apps to pass outside VPN**: A captive network refers to Wi-Fi hotspots typically found in restaurants and hotels. Your options:
    - **No**: Forces all Captive Networking (CN) app traffic through the VPN tunnel​.
    - **Yes, all apps**: Allows all CN app traffic to bypass the VPN​.
    - **Yes, specific apps**: **Add** a list of CN apps whose traffic can bypass the VPN​. Enter the bundle identifiers of CN app. For example, enter `com.contoso.app.id.package`.

  - **Traffic from Captive Websheet app to pass outside VPN**: Captive WebSheet is a built-in web browser that handles captive sign on. **Enable** allows the browser app traffic to bypass the VPN. **Disable** (default) forces WebSheet traffic to use the always-on VPN. The default value is the most secure option.
  - **Network address translation (NAT) keepalive interval (seconds)**: To stay connected to the VPN, the device sends network packets to remain active. Enter a value in seconds on how often these packets are sent, from 20-1440. For example, enter a value of `60` to send the network packets to the VPN every 60 seconds. By default, this value is set to `110` seconds.
  - **Offload NAT keepalive to hardware when device is asleep**: When a device is asleep, **Enable** (default) has NAT continuously send keep-alive packets so the device stays connected to the VPN. **Disable** turns off this feature.

- **Remote identifier**: Enter the network IP address, FQDN, UserFQDN, or ASN1DN of the IKEv2 server. For example, enter `10.0.0.3` or `vpn.contoso.com`. Typically, you enter the same value as the [**Connection name**](#base-vpn-settings) (in this article). But, it does depend on your IKEv2 server settings.

- **Client Authentication type**: Choose how the VPN client authenticates to the VPN. Your options:
  - **User authentication** (default): User credentials authenticate to the VPN.
  - **Machine authentication**: Device credentials authenticate to the VPN.

- **Authentication method**: Choose the type of client credentials to send to the server. Your options:
  - **Certificates**: Uses an existing certificate profile to authenticate to the VPN. Be sure this certificate profile is already assigned to the user or device. Otherwise, the VPN connection fails.
    - **Certificate type**: Select the type of encryption used by the certificate. Be sure the VPN server is configured to accept this type of certificate. Your options:
      - **RSA** (default)
      - **ECDSA256**
      - **ECDSA384**
      - **ECDSA521**

  - **Username and password** (User authentication only): When users connect to the VPN, they're prompted for their username and password.
  - **Shared secret** (Machine authentication only): Allows you to enter a shared secret to send to the VPN server.
    - **Shared secret**: Enter the shared secret, also known as the pre-shared key (PSK). Be sure the value matches the shared secret configured on the VPN server.

- **Server certificate issuer common name**: Allows the VPN server to authenticate to the VPN client. Enter the certificate issuer common name (CN) of the VPN server certificate that's sent to the VPN client on the device. Be sure the CN value matches the configuration on the VPN server. Otherwise, the VPN connection fails.
- **Server certificate common name**: Enter the CN for the certificate itself. If left blank, the remote identifier value is used.

- **Dead peer detection rate**: Choose how often the VPN client checks if the VPN tunnel is active. Your options:
  - **Not configured**: Uses the iOS/iPadOS system default, which may be the same as choosing **Medium**.
  - **None**: Disables dead peer detection.
  - **Low**: Sends a keepalive message every 30 minutes.
  - **Medium** (default): Sends a keepalive message every 10 minutes.
  - **High**: Sends a keepalive message every 60 seconds.

- **TLS version range minimum**: Enter the minimum TLS version to use. Enter `1.0`, `1.1`, or `1.2`. If left blank, the default value of `1.0` is used.
- **TLS version range maximum**: Enter the maximum TLS version to use. Enter `1.0`, `1.1`, or `1.2`. If left blank, the default value of `1.2` is used.

> [!NOTE]
> TLS version range minimum and maximum must be set when using user authentication and certificates.

- **Perfect forward secrecy**: Select **Enable** to turn on perfect forward secrecy (PFS). PFS is an IP security feature that reduces the impact if a session key is compromised. **Disable** (default) doesn't use PFS.
- **Certificate revocation check**: Select **Enable** to make sure the certificates aren't revoked before allowing the VPN connection to succeed. This check is best-effort. If the VPN server times out before determining if the certificate is revoked, access is granted. **Disable** (default) doesn't check for revoked certificates.

- **Configure security association parameters**: **Not configured** (default) uses the iOS/iPadOS system default. Select **Enable** to enter the parameters used when creating security associations with the VPN server:
  - **Encryption algorithm**: Select the algorithm you want:
    - DES
    - 3DES
    - AES-128
    - AES-256 (default)
    - AES-128-GCM
    - AES-256-GCM
  - **Integrity algorithm**:  Select the algorithm you want:
    - SHA1-96
    - SHA1-160
    - SHA2-256 (default)
    - SHA2-384
    - SHA2-512
  - **Diffie-Hellman group**: Select the group you want. Default is group `2`.
  - **Lifetime** (minutes): Choose how long the security association stays active until the keys are rotated. Enter a whole value between `10` and `1440` (1440 minutes is 24 hours). Default is `1440`.

- **Configure a separate set of parameters for child security associations**: iOS/iPadOS allows you to configure separate parameters for the IKE connection, and any child connections. 

  **Not configured** (default) uses the values you enter in the previous **Configure security association parameters** setting. Select **Enable** to enter the parameters used when creating *child* security associations with the VPN server:
  - **Encryption algorithm**: Select the algorithm you want:
    - DES
    - 3DES
    - AES-128
    - AES-256 (default)
    - AES-128-GCM
    - AES-256-GCM
  - **Integrity algorithm**:  Select the algorithm you want:
    - SHA1-96
    - SHA1-160
    - SHA2-256 (default)
    - SHA2-384
    - SHA2-512
  - **Diffie-Hellman group**: Select the group you want. Default is group `2`.
  - **Lifetime** (minutes): Choose how long the security association stays active until the keys are rotated. Enter a whole value between `10` and `1440` (1440 minutes is 24 hours). Default is `1440`.

## Automatic VPN settings

- **Per-app VPN**: Enables per-app VPN. Allows the VPN connection to trigger automatically when certain apps are opened. Also associate the apps with this VPN profile. Per-app VPN isn't supported on IKEv2. For more information, see [instructions for setting up per-app VPN for iOS/iPadOS](vpn-setting-configure-per-app.md). 
  - **Provider Type**: Only available for Pulse Secure and Custom VPN.
  - When using iOS/iPadOS **per-app VPN** profiles with Pulse Secure or a Custom VPN, choose app-layer tunneling (app-proxy) or packet-level tunneling (packet-tunnel). Set the **ProviderType** value to **app-proxy** for app-layer tunneling, or **packet-tunnel** for packet-layer tunneling. If you're not sure which value to use, check your VPN provider's documentation.
  - **Safari URLs that will trigger this VPN**: Add one or more web site URLs. When these URLs are visited using the Safari browser on the device, the VPN connection is automatically established.

- **On-demand VPN**: Configure conditional rules that control when the VPN connection is started. For example, create a condition where the VPN connection is only used when a device isn't connected to a company Wi-Fi network. Or, create a condition. For example, if a device can't access a DNS search domain you enter, then the VPN connection isn't started.

  - **SSIDs or DNS search domains**: Select whether this condition uses wireless network **SSIDs**, or **DNS search domains**. Choose **Add** to configure one or more SSIDs or search domains.
  - **URL string probe**: Optional. Enter a URL that the rule uses as a test. If the device accesses this URL without redirection, then the VPN connection is started. And, the device connects to the target URL. The user doesn't see the URL string probe site.

    For example, a URL string probe is an auditing Web server URL that checks device compliance before connecting the VPN. Or, the URL tests the VPN's ability to connect to a site before the device connects to the target URL through the VPN.

  - **Domain action**: Choose one of the following items:
    - Connect if needed
    - Never connect
  - **Action**: Choose one of the following items:
    - Connect
    - Evaluate connection
    - Ignore
    - Disconnect

## Proxy settings

If you're using a proxy, configure the following settings. Proxy settings aren't available for Zscaler VPN connections.  

- **Automatic configuration script**: Use a file to configure the proxy server. Enter the **Proxy server URL** (for example `http://proxy.contoso.com`) that includes the configuration file.
- **Address**: Enter the IP address of fully qualified host name of the proxy server.
- **Port number**: Enter the port number associated with the proxy server.

## Next steps

The profile is created, but it's not doing anything yet. Next, [assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).

Configure VPN settings on [Android](vpn-settings-android.md), [Android Enterprise](vpn-settings-android-enterprise.md), [macOS](vpn-settings-macos.md), and [Windows 10](vpn-settings-windows-10.md) devices.
