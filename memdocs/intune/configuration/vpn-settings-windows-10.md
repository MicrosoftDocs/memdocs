---
# required metadata

title: Windows 10 VPN settings in Microsoft Intune - Azure | Microsoft Docs
description: Learn and read about all the available VPN settings in Microsoft Intune, what they are used for, and what they do, including traffic rules, Conditional Access, and DNS and proxy settings for Windows 10 and Windows Holographic for Business devices.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
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
ms.reviewer: tycast
#ms.tgt_pltfrm:
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
---

# Windows 10 and Windows Holographic device settings to add VPN connections using Intune



You can add and configure VPN connections for devices using Microsoft Intune. This article lists and describes commonly used settings and features when creating virtual private networks (VPNs). These VPN settings and features are used in device configuration profiles in Intune that are pushed or deployed to devices.

As part of your mobile device management (MDM) solution, use these settings to allow or disable features, including using a VPN vendor, enabling always on, using DNS, adding a proxy, and more.

These settings apply to devices running:

- Windows 10
- Windows Holographic for Business

Depending on the settings you choose, not all values may be configurable.

## Before you begin

[Create a VPN device configuration profile](vpn-settings-configure.md).

## Base VPN settings

- **Connection name**: Enter a name for this connection. End users see this name when they browse their device for the list of available VPN connections.
- **Servers**: Add one or more VPN servers that devices connect to. When you add a server, you enter the following information:
  - **Description**: Enter a descriptive name for the server, such as **Contoso VPN server**
  - **IP address or FQDN**: Enter the IP address or fully qualified domain name (FQDN) of the VPN server that devices connect to, such as **192.168.1.1** or **vpn.contoso.com**
  - **Default server**: Enables this server as the default server that devices use to establish the connection. Set only one server as the default.
  - **Import**: Browse to a comma-separated file that includes a list of servers in the format: description, IP address or FQDN, Default server. Choose **OK** to import these servers into the **Servers** list.
  - **Export**: Exports the list of servers to a comma-separated-values (csv) file

- **Register IP addresses with internal DNS**: Select **Enable** to configure the Windows 10 VPN profile to dynamically register the IP addresses assigned to the VPN interface with the internal DNS. Select **Disable** to not dynamically register the IP addresses.

- **Connection type**: Select the VPN connection type from the following list of vendors:

  - **Pulse Secure**
  - **F5 Edge Client**
  - **SonicWALL Mobile Connect**
  - **Check Point Capsule VPN**
  - **Citrix**
  - **Palo Alto Networks GlobalProtect**
  - **Automatic**
  - **IKEv2**
  - **L2TP**
  - **PPTP**

  When you choose a VPN connection type, you may also be asked for the following settings:  
  - **Always On**: Choose **Enable** to automatically connect to the VPN connection when the following events happen: 
    - Users sign into their devices
    - The network on the device changes
    - The screen on the device turns back on after being turned off 

  - **Authentication method**: Select how you want users to authenticate to the VPN server. Using **certificates** provides enhanced features, such as zero-touch experience, on-demand VPN, and per-app VPN.
  - **Remember credentials at each logon**: Choose to cache the authentication credentials.
  - **Custom XML**: Enter any custom XML commands that configure the VPN connection.
  - **EAP Xml**: Enter any EAP XML commands that configure the VPN connection

### Pulse Secure example

```
<pulse-schema><isSingleSignOnCredential>true</isSingleSignOnCredential></pulse-schema>
```

### F5 Edge Client example

```
<f5-vpn-conf><single-sign-on-credential /></f5-vpn-conf>
```

### SonicWALL Mobile Connect example
**Login group or domain**: This property can't be set in the VPN profile. Instead, Mobile Connect parses this value when the user name and domain are entered in the `username@domain` or `DOMAIN\username` formats.

Example:

```
<MobileConnect><Compression>false</Compression><debugLogging>True</debugLogging><packetCapture>False</packetCapture></MobileConnect>
```

### CheckPoint Mobile VPN example

```
<CheckPointVPN port="443" name="CheckPointSelfhost" sso="true" debug="3" />
```

### Writing custom XML
For more information about writing custom XML commands, see each manufacturer's VPN documentation.

For more information about creating custom EAP XML, see [EAP configuration](https://docs.microsoft.com/windows/client-management/mdm/eap-configuration).

## Apps and Traffic Rules

- **Associate WIP or apps with this VPN**: Enable this setting if you only want some apps to use the VPN connection. Your options:

  - **Associate a WIP with this connection**: Enter a **WIP domain for this connection**
  - **Associate apps with this connection**: You can **Restrict VPN connection to these apps**, and then add **Associated Apps**. The apps you enter automatically use the VPN connection. The type of app determines the app identifier. For a universal app, enter the package family name. For a desktop app, enter the file path of the app.
  >[!IMPORTANT]
  >We recommend that you secure all app lists created for per-app VPNs. If an unauthorized user changes this list, and you import it into the per-app VPN app list, then you potentially authorize VPN access to apps that shouldn't have access. One way you can secure app lists is using an access control list (ACL).

- **Network traffic rules for this VPN connection**: Select which protocols, and which local & remote port and address ranges, are enabled for the VPN connection. If you don't create a network traffic rule, then all protocols, ports, and address ranges are enabled. After you create a rule, the VPN connection uses only the protocols, ports, and address ranges that you enter in that rule.

## Conditional Access

- **Conditional Access for this VPN connection**: Enables device compliance flow from the client. When enabled, the VPN client communicates with Azure Active Directory (AD) to get a certificate to use for authentication. The VPN should be set up to use certificate authentication, and the VPN server must trust the server returned by Azure AD.

- **Single sign-on (SSO) with alternate certificate**: For device compliance, use a certificate different from the VPN authentication certificate for Kerberos authentication. Enter the certificate with the following settings:

  - **Name**: Name for extended key usage (EKU)
  - **Object Identifier**: Object identifier for EKU
  - **Issuer hash**: Thumbprint for SSO certificate

## DNS Settings

- **DNS suffix search list**: In **DNS suffixes**, enter a DNS suffix, and **Add**. You can add many suffixes.

  When using DNS suffixes, you can search for a network resource using its short name, instead of the fully qualified domain name (FQDN). When searching using the short name, the suffix is automatically determined by the DNS server. For example, `utah.contoso.com` is in the DNS suffix list. You ping `DEV-comp`. In this scenario, it resolves to `DEV-comp.utah.contoso.com`.

  DNS suffixes are resolved in the order listed, and the order can be changed. For example, `colorado.contoso.com` and `utah.contoso.com` are in the DNS suffix list, and both have a resource called `DEV-comp`. Since `colorado.contoso.com` is first in the list, it resolves as `DEV-comp.colorado.contoso.com`.
  
  To change the order, click the dots to the left of the DNS suffix, and then drag the suffix to the top:

  ![Select the three dots, and click-and-drag to move the dns suffix](./media/vpn-settings-windows-10/vpn-settings-windows10-move-dns-suffix.png)

- **Name Resolution Policy table (NRPT) rules**: Name Resolution Policy table (NRPT) rules define how DNS resolves names when connected to the VPN. After the VPN connection is established, you choose which DNS servers the VPN connection uses.

  You can add rules to the table that include the domain, DNS server, proxy, and other details to resolve the domain you enter. The VPN connection uses these rules when users connect to the domains you enter.

  Select **Add** to add a new rule. For each server, enter:

  - **Domain**: Enter the fully qualified domain name (FQDN) or a DNS suffix to apply the rule. You can also enter a period (.) at the beginning for a DNS suffix. For example, enter `contoso.com` or `.allcontososubdomains.com`.
  - **DNS servers**: Enter the IP address or DNS server that resolves the domain. For example, enter `10.0.0.3` or `vpn.contoso.com`.
  - **Proxy**: Enter the web proxy server that resolves the domain. For example, enter `http://proxy.com`.
  - **Automatically connect**: When **Enabled**, the device automatically connects to the VPN when a device connects to a domain you enter, such as `contoso.com`. When **Not configured** (default), the device doesn't automatically connect to the VPN
  - **Persistent**: When set to **Enabled**, the rule stays in the Name Resolution Policy table (NRPT) until the rule is manually removed from the device, even after the VPN disconnects. When set to **Not configured** (default), NRPT rules in the VPN profile are removed from the device when the VPN disconnects.

## Proxy settings

- **Automatic configuration script**: Use a file to configure the proxy server. Enter the **Proxy server URL**, such as `http://proxy.contoso.com`, that includes the configuration file.
- **Address**: Enter the proxy server address, such as an IP address or `vpn.contoso.com`
- **Port number**: Enter the TCP port number used by your proxy server
- **Bypass proxy for local addresses**: If you don't want to use a proxy server for local addresses, then choose Enable. This setting applies if your VPN server requires a proxy server for the connection.

## Split Tunneling

- **Split tunneling**: **Enable** or **Disable** to let devices decide which connection to use depending on the traffic. For example, a user in a hotel uses the VPN connection to access work files, but uses the hotel's standard network for regular web browsing.
- **Split tunneling routes for this VPN connection**: Add optional routes for third-party VPN providers. Enter a destination prefix, and a prefix size for each connection.

## Trusted Network Detection

**Trusted network DNS suffixes**: When users are already connected to a trusted network, you can prevent devices from automatically connecting to other VPN connections.

In **DNS suffixes**, enter a DNS suffix that you want to trust, such as contoso.com, and select **Add**. You can add as many suffixes as you want.

If a user is connected to a DNS suffix in the list, then the user won't automatically connect to another VPN connection. The user continues to use the trusted list of DNS suffixes you enter. The trusted network is still used, even if any autotriggers are set.

For example, if the user is already connected to a trusted DNS suffix, then the following autotriggers are ignored. Specifically, the DNS suffixes in the list cancel all other connection autotriggers, including:

- Always on
- App-based trigger
- DNS autotrigger

## Next steps

The profile is created, but it's not doing anything yet. Next, [assign the profile](device-profile-assign.md), and [monitor its status](device-profile-monitor.md).

Configure VPN settings on [Android](vpn-settings-android.md), [iOS/iPadOS](vpn-settings-ios.md), and [macOS](vpn-settings-macos.md) devices.
