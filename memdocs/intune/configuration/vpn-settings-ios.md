---
# required metadata

title: Configure VPN settings to iOS/iPadOS devices in Microsoft Intune
description: Add or create a VPN configuration profile on iOS/iPadOS devices using virtual private network (VPN) configuration settings in Microsoft Intune. Configure the connection details, authentication methods, split tunneling, custom VPN settings with the identifier, key and value pairs, per-app VPN settings that include Safari URLs, and on-demand VPNs with SSIDs or DNS search domains, proxy settings to include a configuration script, IP or FQDN address, and TCP port.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/05/2022
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

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

# Add VPN settings on iOS and iPadOS devices in Microsoft Intune

Microsoft Intune includes many VPN settings that can be deployed to your iOS/iPadOS devices. These settings are used to create and configure VPN connections to your organization's network. This article describes these settings. Some settings are only available for some VPN clients, such as Citrix, Zscaler, and more.

## Before you begin

- Create an [iOS/iPadOS VPN device configuration profile](vpn-settings-configure.md).

- [!INCLUDE [partner-vpns](../includes/partner-vpns.md)]

> [!NOTE]
>
> - These settings are available for all enrollment types except user enrollment. User enrollment is limited to [per-app VPN](./vpn-setting-configure-per-app.md). For more information on the enrollment types, see [iOS/iPadOS enrollment](../enrollment/ios-enroll.md).
>
> - The available settings depend on the VPN client you choose. Some settings are only available for specific VPN clients.
>
> - These settings use the [Apple VPN payload](https://developer.apple.com/documentation/devicemanagement/vpn) (opens Apple's web site).

## Connection type

Select the VPN connection type from the following list of vendors:

- **Check Point Capsule VPN**
- **Cisco Legacy AnyConnect**

  Applies to Cisco Legacy AnyConnect app version 4.0.5x and earlier.

- **Cisco AnyConnect**

  Applies to [Cisco AnyConnect](https://itunes.apple.com/app/cisco-anyconnect/id1135064690) app version 4.0.7x and later.

- **SonicWall Mobile Connect**
- **F5 Access Legacy**

  Applies to F5 Access app version 2.1 and earlier.
- **F5 Access**

  Applies to F5 Access app version 3.0 and later.
- **Palo Alto Networks GlobalProtect (Legacy)**

  Applies to Palo Alto Networks GlobalProtect app version 4.1 and earlier.
- **Palo Alto Networks GlobalProtect**

  Applies to Palo Alto Networks GlobalProtect app version 5.0 and later.
- **Pulse Secure**
- **Cisco (IPSec)**
- **Citrix VPN**
- **Citrix SSO**
- **Zscaler**

  To use Conditional Access, or allow users to bypass the Zscaler sign-in screen, you must integrate Zscaler Private Access (ZPA) with your Azure AD account. For detailed steps, see the [Zscaler documentation](https://help.zscaler.com/zpa/configuration-guide-microsoft-azure-ad).
- **NetMotion Mobility**
- **IKEv2**

  [IKEv2 settings](#ikev2-settings) (in this article) describes the properties.

- **Microsoft Tunnel (standalone client)(preview)**

  Applies to the Microsoft Tunnel client app.

  > [!Important]
  > **Plan for change**. On April 29, 2022 both the *Microsoft Tunnel* connection type and *Microsoft Defender for Endpoint* as the tunnel client app became generally available. With this general availability, the use of the *Microsoft Tunnel (standalone client)(preview)* connection type and the standalone tunnel client app are deprecated and soon will drop from support.  
  > - On July 29, 2022, the  standalone tunnel client app will no longer be available for download. Only the generally available version of *Microsoft Defender for Endpoint* will be available as the tunnel client app.  
  > - On August 1, 2022, the *Microsoft Tunnel (standalone client) (preview)* connection type will cease to connect to Microsoft Tunnel.  
  >
  > To avoid a disruption in service for Microsoft Tunnel, plan to migrate your use of the deprecated tunnel client app and connection type to those that are now generally available.

- **Microsoft Tunnel**

  Applies to the Microsoft Defender for Endpoint app that includes Tunnel client functionality.

  > [!Important]
  > On April 29, 2022, this connection type became generally available and supports Microsoft Defender for Endpoint as a tunnel client app. However, the connection type continues to reflect *preview*.
  
- **Custom VPN**

> [!NOTE]
> Cisco, Citrix, F5, and Palo Alto have announced that their legacy clients don't work on iOS 12 and later. You should migrate to the new apps as soon as possible. For more information, see the [Microsoft Intune Support Team Blog](https://go.microsoft.com/fwlink/?linkid=2013806&clcid=0x409).

## Base VPN settings

- **Connection name**: End users see this name when they browse their device for a list of available VPN connections.
- **Custom domain name** (Zscaler only): Prepopulate the Zscaler app's sign-in field with the domain your users belong to. For example, if a username is `Joe@contoso.net`, then the `contoso.net` domain statically appears in the field when the app opens. If you don't enter a domain name, then the domain portion of the UPN in Azure Active Directory (AD) is used.
- **VPN server address**: The IP address or fully qualified domain name (FQDN) of the VPN server that devices connect with. For example, enter `192.168.1.1` or `vpn.contoso.com`.
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
  - Integrate Citrix Gateway with Intune for NAC. See the [Integrating Microsoft Intune/Enterprise Mobility Suite with NetScaler (LDAP+OTP Scenario)](https://docplayer.net/47400257-Integrating-microsoft-intune-enterprise-mobility-suite-with-netscaler-ldap-otp-scenario.html) Citrix deployment guide.
  - Enable NAC in the VPN profile.

  **When using F5 Access**, be sure to:

  - Confirm you're using F5 BIG-IP 13.1.1.5 or later. 
  - Integrate BIG-IP with Intune for NAC. See the [Overview: Configuring APM for device posture checks with endpoint management systems](https://support.f5.com/kb/en-us/products/big-ip_apm/manuals/product/apm-client-configuration-7-1-6/6.html#guid-0bd12e12-8107-40ec-979d-c44779a8cc89) F5 guide.
  - Enable NAC in the VPN profile.

  For the VPN partners that support device ID, the VPN client, such as Citrix SSO, can get the ID. Then, it can query Intune to confirm the device is enrolled, and if the VPN profile is compliant or not compliant.

  - To remove this setting, recreate the profile, and don't select **I agree**. Then, reassign the profile.

- **Enter key and value pairs for the NetMotion Mobility VPN attributes** (NetMotion Mobility only): Enter or import key and value pairs. These values may be supplied by your VPN provider.

- **Microsoft Tunnel site** (Microsoft Tunnel only): Select an existing site. The VPN client connects to the public IP address or FQDN of this site.

  For more information, see [Microsoft Tunnel for Intune](../protect/microsoft-tunnel-overview.md).

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

  - **Traffic from Captive Websheet app to pass outside VPN**: Captive WebSheet is a built-in web browser that handles captive sign-on. **Enable** allows the browser app traffic to bypass the VPN. **Disable** (default) forces WebSheet traffic to use the always-on VPN. The default value is the most secure option.
  - **Network address translation (NAT) keepalive interval (seconds)**: To stay connected to the VPN, the device sends network packets to remain active. Enter a value in seconds on how often these packets are sent, from 20-1440. For example, enter a value of `60` to send the network packets to the VPN every 60 seconds. By default, this value is set to `110` seconds.
  - **Offload NAT keepalive to hardware when device is asleep**: When a device is asleep, **Enable** (default) has NAT continuously send keep-alive packets so the device stays connected to the VPN. **Disable** turns off this feature.

- **Remote identifier**: Enter the network IP address, FQDN, UserFQDN, or ASN1DN of the IKEv2 server. For example, enter `10.0.0.3` or `vpn.contoso.com`. Typically, you enter the same value as the [**Connection name**](#base-vpn-settings) (in this article). But, it does depend on your IKEv2 server settings.

- **Local identifier**: Enter the device FQDN or subject common name of the IKEv2 VPN client on the device. Or, you can leave this value empty (default). Typically, the local identifier should match the user or device certificate’s identity. The IKEv2 server may require the values to match so it can validate the client’s identity.

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

- **TLS version range minimum**: Enter the minimum TLS version to use. Enter `1.0`, `1.1`, or `1.2`. If left blank, the default value of `1.0` is used. When using user authentication and certificates, you must configure this setting.
- **TLS version range maximum**: Enter the maximum TLS version to use. Enter `1.0`, `1.1`, or `1.2`. If left blank, the default value of `1.2` is used. When using user authentication and certificates, you must configure this setting.
- **Perfect forward secrecy**: Select **Enable** to turn on perfect forward secrecy (PFS). PFS is an IP security feature that reduces the impact if a session key is compromised. **Disable** (default) doesn't use PFS.
- **Certificate revocation check**: Select **Enable** to make sure the certificates aren't revoked before allowing the VPN connection to succeed. This check is best-effort. If the VPN server times out before determining if the certificate is revoked, access is granted. **Disable** (default) doesn't check for revoked certificates.

- **Use IPv4/IPv6 internal subnet attributes**: Some IKEv2 servers use the `INTERNAL_IP4_SUBNET` or `INTERNAL_IP6_SUBNET` attributes. **Enable** forces the VPN connection to use these attributes. **Disable** (default) doesn't force the VPN connection to use these subnet attributes.
- **Mobility and multihoming (MOBIKE)**: MOBIKE allows VPN clients to change their IP address without recreating a security association with the VPN server. **Enable** (default) turns on MOBIKE, which can improve VPN connections when traveling between networks. **Disable** turns off MOBIKE.
- **Redirect**: **Enable** (default) redirects the IKEv2 connection if a redirect request is received from the VPN server.​ **Disable** prevents the IKEv2 connection from redirecting if a redirect request is received from the VPN server.​

- **Maximum transmission unit**: Enter the maximum transmission unit (MTU) in bytes, from 1-65536. When set to **Not configured** or left blank, Intune doesn't change or update this setting. By default, Apple may set this value to 1280.

  This setting applies to:  
  - iOS/iPadOS 14 and newer

- **Security association parameters**: Enter the parameters to use when creating security associations with the VPN server:

  - **Encryption algorithm**: Select the algorithm you want:
    - DES
    - 3DES
    - AES-128
    - AES-256 (default)
    - AES-128-GCM
    - AES-256-GCM

    > [!NOTE]
    > If you set the encryption algorithm to `AES-128-GCM` or `AES-256-GCM`, then the `AES-256` default is used. This is a known issue, and will be fixed in a future release. There is no ETA.

  - **Integrity algorithm**:  Select the algorithm you want:
    - SHA1-96
    - SHA1-160
    - SHA2-256 (default)
    - SHA2-384
    - SHA2-512
  - **Diffie-Hellman group**: Select the group you want. Default is group `2`.
  - **Lifetime** (minutes): Enter how long the security association stays active until the keys are rotated. Enter a whole value between `10` and `1440` (1440 minutes is 24 hours). Default is `1440`.

- **Child security association parameters**: iOS/iPadOS allows you to configure separate parameters for the IKE connection, and any child connections. Enter the parameters used when creating *child* security associations with the VPN server:

  - **Encryption algorithm**: Select the algorithm you want:
    - DES
    - 3DES
    - AES-128
    - AES-256 (default)
    - AES-128-GCM
    - AES-256-GCM

    > [!NOTE]
    > If you set the encryption algorithm to `AES-128-GCM` or `AES-256-GCM`, then the `AES-256` default is used. This is a known issue, and will be fixed in a future release. There is no ETA.

- **Integrity algorithm**:  Select the algorithm you want:
    - SHA1-96
    - SHA1-160
    - SHA2-256 (default)
    - SHA2-384
    - SHA2-512
  - **Diffie-Hellman group**: Select the group you want. Default is group `2`.
  - **Lifetime** (minutes): Enter how long the security association stays active until the keys are rotated. Enter a whole value between `10` and `1440` (1440 minutes is 24 hours). Default is `1440`.

## Automatic VPN

- **Type of automatic VPN**: Select the VPN type you want to configure: On-demand VPN or per-app VPN:

  - **Not configured** (default): Intune doesn't change or update this setting.
  - **On-demand VPN**: On-demand VPN uses rules to automatically connect or disconnect the VPN connection. When your devices attempt to connect to the VPN, it looks for matches in the parameters and rules you create, such as a matching domain name. If there's a match, then the action you choose runs.

    For example, you can create a condition where the VPN connection is only used when a device isn't connected to a company Wi-Fi network. Or, if a device can't access a DNS search domain you enter, then the VPN connection isn't started.

    - **On-demand rules** > **Add**: Select **Add** to add a rule. If there isn't an existing VPN connection, then use these settings to create an on-demand rule. If there's a match to your rule, then the device does the action you select.

      - **I want to do the following**: If there's a match between the device value and your on-demand rule, then select the action you want the device to do. Your options:

        - **Establish VPN**: If there's a match between the device value and your on-demand rule, then the device connects to the VPN.
        - **Disconnect VPN**: If there's a match between the device value and your on-demand rule, then the VPN connection is disconnected.
        - **Evaluate each connection attempt**: If there's a match between the device value and your on-demand rule, then use the **Choose whether to connect** setting to decide what happens for *each* VPN connection attempt:
          - **Connect if needed**: If the device is on an internal network, or if there's already an established VPN connection to the internal network, then the on-demand VPN won't connect. These settings aren't used.

            If there isn't an existing VPN connection, then for *each* VPN connection attempt, decide if users should connect using a DNS domain name. This rule only applies to domains in the **When users try to access these domains** list. All other domains are ignored.

            - **When users try to access these domains**: Enter one or more DNS domains, like `contoso.com`. If users try to connect to a domain in this list, then the device uses DNS to resolve the domains you enter. If the domain doesn't resolve, meaning it doesn't have access to internal resources, then it connects to the VPN on-demand. If the domain does resolve, meaning it already has access to internal resources, then it doesn't connect to the VPN.

              > [!NOTE]
              > 
              > - If the **When users try to access these domains** setting is empty, then the device uses the DNS servers configured on the network connection service (Wi-Fi/ethernet) to resolve the domain. The idea is that these DNS servers are public servers.
              > 
              >   The domains in the **When users try to access these domains** list are internal resources. Internal resources aren’t on public DNS servers and can't be resolved. So, the device connects to the VPN. Now, the domain is resolved using the VPN connection’s DNS servers and the internal resource is available. 
              > 
              >   If the device is on the internal network, then the domain resolves, and a VPN connection isn't created because the internal domain is already available. You don't want to waste VPN resources on devices already on the internal network.
              > 
              > - If the **When users try to access these domains** setting is populated, then the DNS servers on this list are used to resolve the domains in the list.
              > 
              >   The idea is the opposite of the first bullet (**When users try to access these domains** setting is empty). For instance, the **When users try to access these domains** list has internal DNS servers. A device on an external network can't route to the internal DNS servers. The name resolution times out, and the device connects to the VPN on-demand. Now the internal resources are available.
              > 
              >   Remember this information only applies to domains in the **When users try to access these domains** list. All other domains are resolved with public DNS servers. When the device is connected to the internal network, the DNS servers in the list are accessible, and there's no need to connect to the VPN.

            - **Use the following DNS servers to resolve these domains (optional)**: Enter one or more DNS server IP addresses, like `10.0.0.22`. The DNS servers you enter are used to resolve the domains in the **When users try to access these domains** setting.

            - **When this URL is unreachable, force-connect the VPN**: Optional. Enter an HTTP or HTTPS probing URL that the rule uses as a test. For example, enter `https://probe.Contoso.com `. This URL is probed every time a user tries to access a domain in the **When users try to access these domains** setting. The user doesn't see the URL string probe site.

              If the probe fails because the URL is unreachable or doesn't return a 200 HTTP status code, then the device connects to the VPN. 

              The idea is that the URL is only accessible on the internal network. If the URL can be accessed, then a VPN connection isn't needed. If the URL can't be accessed, then the device is on an external network, and it connects to the VPN on-demand. Once the VPN connection is established, internal resources are available.

          - **Never connect**: For each VPN connection attempt, when users try to access the domains you enter, then the device never connects to the VPN.

            - **When users try to access these domains**: Enter one or more DNS domains, like `contoso.com`. If users try to connect to a domain in this list, then a VPN connection isn't created. If they try to connect to a domain not in this list, then the device connects to the VPN.

        - **Ignore**: If there's a match between the device value and your on-demand rule, then a VPN connection is ignored.

      - **I want to restrict to**: In the **I want to do the following** setting, if you select **Establish VPN**, **Disconnect VPN**, or **Ignore**, then select the condition that the rule must meet. Your options:

        - **Specific SSIDs**: Enter one or more wireless network names that the rule will apply. This network name is the Service Set Identifier (SSID). For example, enter `Contoso VPN`.
        - **Specific search domains**: Enter one or more DNS domains that the rule will apply. For example, enter `contoso.com`.
        - **All domains**: Select this option to apply your rule to all domains in your organization.

      - **But only if this URL probe succeeds**: Optional. Enter a URL that the rule uses as a test. For example, enter `https://probe.Contoso.com `. If the device accesses this URL without redirection, then the VPN connection is started. And, the device connects to the target URL. The user doesn't see the URL string probe site.

        For example, the URL tests the VPN's ability to connect to a site before the device connects to the target URL through the VPN.

    - **Block users from disabling automatic VPN**: Your options:

      - **Not configured**: Intune doesn't change or update this setting.
      - **Yes**: Prevents users from turning off automatic VPN. It forces users to keep the automatic VPN enabled and running.
      - **No**: Allows users to turn off automatic VPN.

      This setting applies to:

      - iOS 14 and newer
      - iPadOS 14 and newer

  - **Per-app VPN**: Enables per-app VPN by associating this VPN connection with a specific app. When the app runs, the VPN connection starts. You can associate the VPN profile with an app when you assign the app software or program. For more information, see [How to assign and monitor apps](../apps/apps-deploy.md).

    Per-app VPN isn't supported on an IKEv2 connection. For more information, see [set up per-app VPN for iOS/iPadOS devices](vpn-setting-configure-per-app.md).

    - **Provider Type**: Only available for Pulse Secure and Custom VPN.

      When using **per-app VPN** profiles with Pulse Secure or a Custom VPN, choose app-layer tunneling (app-proxy) or packet-level tunneling (packet-tunnel):

      - **app-proxy**: Select this option for app-layer tunneling.
      - **packet-tunnel**: Select this option for packet-layer tunneling.

      If you're not sure which option to use, then check your VPN provider's documentation.

    - **Safari URLs that will trigger this VPN**: Add one or more web site URLs. When these URLs are visited using the Safari browser on the device, the VPN connection is automatically established. For example, enter `contoso.com`.

    - **Associated Domains**: Enter associated domains in the VPN profile to use with this VPN connection.

      For more information, see [associated domains](device-features-configure.md#associated-domains).

    - **Excluded Domains**: Enter domains that can bypass the VPN connection when per-app VPN is connected. For example, enter `contoso.com`. Traffic to the `contoso.com` domain will use the public Internet even if the VPN is connected.

    - **Block users from disabling automatic VPN**: Your options:

      - **Not configured**: Intune doesn't change or update this setting.
      - **Yes**: Prevents users from turning off the Connect On Demand toggle within the VPN profile settings. It forces users to keep per-app VPN or on-demand rules enabled and running.
      - **No**: Allows users to turn off the Connect On Demand toggle, which disables per-app VPN and on-demand rules.

      This setting applies to:

      - iOS 14 and newer
      - iPadOS 14 and newer

## Per-app VPN

These settings apply to the following VPN connection types:

- **Microsoft Tunnel (standalone client) (preview)**
- **Microsoft Tunnel**

**Settings**:

- **Per-app VPN**: **Enable** associates a specific app to this VPN connection. When the app runs, traffic automatically routes through the VPN connection. You can associate the VPN profile with an app when you assign the software. For more information, see [How to assign and monitor apps](../apps/apps-deploy.md).

  For more information, see [Microsoft Tunnel for Intune](../protect/microsoft-tunnel-overview.md).

- **Safari URLs that will trigger this VPN**: Add one or more web site URLs. When these URLs are visited using the Safari browser on the device, the VPN connection is automatically established. For example, enter `contoso.com`.

- **Associated Domains**: Enter associated domains in the VPN profile to use with this VPN connection.

  For more information, see [associated domains](device-features-configure.md#associated-domains).

- **Excluded Domains**: Enter domains that can bypass the VPN connection when per-app VPN is connected. For example, enter `contoso.com`. Traffic to the `contoso.com` domain will use the public Internet even if the VPN is connected.

## Proxy

If you use a proxy, then configure the following settings.

- **Automatic configuration script**: Use a file to configure the proxy server. Enter the proxy server URL that includes the configuration file. For example, enter `http://proxy.contoso.com/pac`.
- **Address**: Enter the IP address or fully qualified host name of the proxy server. For example, enter `10.0.0.3` or `vpn.contoso.com`.
- **Port number**: Enter the port number associated with the proxy server. For example, enter `8080`.

## Next steps

The profile is created, but may not be doing anything yet. Be sure to [assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).

Configure VPN settings on [Android](vpn-settings-android.md), [Android Enterprise](vpn-settings-android-enterprise.md), [macOS](vpn-settings-macos.md), and [Windows 10](vpn-settings-windows-10.md) devices.
