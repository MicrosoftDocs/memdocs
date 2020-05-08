---
# required metadata

title: Intune endpoint security firewall settings | Microsoft Docs
description: Endpoint security firewall policy settings for Windows and macOS in Microsoft Intune 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha

---
# Firewall policy settings for endpoint security in Intune

View the settings you can configure in profiles for *Firewall* policy in the endpoint security node of Intune as part of an [Endpoint security policy](../protect/endpoint-security-policy.md).

Supported platforms and profiles:

- **macOS**:
  - Profile: **macOS firewall**

- **Windows 10 and later**:
  - Profile: **Microsoft Defender Firewall**

## macOS firewall profile

### Firewall

The following settings are configured as [Endpoint Security policy for macOS Firewalls](../protect/endpoint-security-firewall-policy.md)

- **Enable Firewall**

  - **Not configured** (*default*)
  - **Yes** - Enable the firewall.
  
  When set to *Yes*, you can configure the following settings.  

  - **Block all incoming connections**

    - **Not configured** (*default*)
    - **Yes** - Block all incoming connections except connections that are required for basic Internet services such as DHCP, Bonjour, and IPSec. This blocks all sharing services.

  - **Enable stealth mode**

    - **Not configured** (*default*)
    - **Yes** - Prevent the computer from responding to probing requests. The computer still answers incoming requests for authorized apps.

  - **Firewall apps**
    Expand the dropdown and then select **Add** to then specify apps and rules for incoming connections for the app.
    - **Allow incoming connections**
      - Not configured
      - Block
      - Allow

    - **Bundle ID** - The ID identifies the app. For example: *com.apple.app*

## Microsoft Defender Firewall profile

### Microsoft Defender Firewall

The following settings are configured as [Endpoint Security policy for Windows 10 Firewalls](../protect/endpoint-security-firewall-policy.md).

- **Disable stateful File Transfer Protocol (FTP)**  
  CSP: [MdmStore/Global/DisableStatefulFtp](https://go.microsoft.com/fwlink/?linkid=872536)

  - **Not configured** (*default*) - The firewall uses FTP to inspect and filter secondary network connections, which could cause your firewall rules to be ignored.
  - **Yes**
  
- **Number of seconds a security association can be idle before it's deleted**  
  CSP: [MdmStore/Global/SaIdleTime](https://go.microsoft.com/fwlink/?linkid=872539)

  Specify a time in seconds between 300 and 3600, for how long the security associations are kept after network traffic isn't seen.
  
  If you don't specify any value, the system deletes a security association after it's been idle for 300 seconds.
  
- **Preshared key encoding**  
  CSP: [MdmStore/Global/PresharedKeyEncoding](https://go.microsoft.com/fwlink/?linkid=872541)

  If you don't require *UTF-8*, preshared keys are initially encoded using UTF-8. After that, device users can choose another encoding method.

  - **Not configured** (*default*)
  - **None**
  - **UTF8**

- **Firewall IP sec exemptions allow neighbor discovery**  
  CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **Not configured** (*default*)
  - **Yes** - Firewall IPsec exemptions allow neighbor discovery.

- **Firewall IP sec exemptions allow ICMP**  
  CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **Not configured** (*default*)
  - **Yes** - Firewall IPsec exemptions allow ICMP.

- **Firewall IP sec exemptions allow router discovery**  
  CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **Not configured** (*default*)
  - **Yes** - Firewall IPsec exemptions allow router discovery.

- **Firewall IP sec exemptions allow DHCP**  
  CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **Not configured** (*default*)
  - **Yes** - Firewall IP sec exemptions allow DHCP

- **Certificate revocation list (CRL) verification**  
  CSP: [MdmStore/Global/CRLcheck](https://go.microsoft.com/fwlink/?linkid=872548)

   Specify how certificate revocation list (CRL) verification is enforced.
  - **Not configured** (*default*) - The client default is to disable CRL verification.
  - **None**
  - **Attempt**
  - **Require**

- **Require keying modules to only ignore the authentication suites they don’t support**  
  CSP: [MdmStore/Global/OpportunisticallyMatchAuthSetPerKM](https://go.microsoft.com/fwlink/?linkid=872550)

  - **Not configured** (*default*)
  - **Yes** - Keying modules ignore unsupported authentication suites.

- **Packet queuing**  
  CSP: [MdmStore/Global/EnablePacketQueue](https://go.microsoft.com/fwlink/?linkid=872551)

  Specify how to enable scaling for the software on the receive side for the encrypted receive and clear text forward for the IPsec tunnel gateway scenario. This ensures the packet order is preserved.
  - **Not configured** (*default*) - Packet queuing will be returned back to client default, which is disabled.
  - **Disabled**
  - **Queue Inbound**
  - **Queue Outbound**
  - **Queue Both**

- **Turn on Microsoft Defender Firewall for domain networks**  
  CSP: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **Not configured** (*default*) - The client returns to default, which is to enable the firewall.
  - **Yes** - The Microsoft Defender Firewall for the network type of **domain** is turned on and enforced.
  - **No** - Disable the firewall.

- **Turn on Microsoft Defender Firewall for private networks**  
  CSP: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **Not configured** (*default*) - The client returns to default, which is to enable the firewall.
  - **Yes** - The Microsoft Defender Firewall for the network type of **private** is turned on and enforced.
  - **No** - Disable the firewall.

- **Turn on Microsoft Defender Firewall for public networks**  
  CSP: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **Not configured** (*default*) - The client returns to default, which is to enable the firewall.
  - **Yes** - The Microsoft Defender Firewall for the network type of **public** is turned on and enforced.
  - **No** - Disable the firewall.

<!-- Microsoft Defender Firewall rules added in 2005  -->

### Microsoft Defender Firewall rules

*(Public preview)*

The following settings are configured as [Endpoint Security policy for Windows 10 Firewalls](../protect/endpoint-security-firewall-policy.md).

#### Windows Firewall Rule

- **Name**  
  Specify a friendly name for your rule. This name will appear in the list of rules to help you identify it.

- **Description**  
  Provide a description of the rule.

- **Direction**  
  - **Not configured** (*default*) - This rule defaults to outbound traffic.
  - **Out** - This rule applies to outbound traffic.
  - **In** -  This rule applies to inbound traffic.

- **Action**  
  - **Not configured** (*default*) - The rule defaults to allow traffic.
  - **Blocked** - Traffic is blocked in the *Direction* you've configured.
  - **Allowed** - Traffic is allowed in the *Direction* you've configured.

- **Network type**  
  Specify the network type to which the rule belongs. You can choose one or more of the following. If you don't select an option, the rule applies to all network types.
  - **Domain**
  - **Private**
  - **Public**
  - **Not configured**

- **Package family name**  
  [Get-AppxPackage](https://docs.microsoft.com/previous-versions//hh856044(v=technet.10))

  Package family names can be retrieved by running the Get-AppxPackage command from PowerShell.

- **File path**  
  CSP: [FirewallRules/FirewallRuleName/App/FilePath](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#filepath)

  To specify the file path of an app, enter the apps location on the client device. For example: `C:\Windows\System\Notepad.exe` or `%WINDIR%\Notepad.exe`

- **Service name**  
  [FirewallRules/FirewallRuleName/App/ServiceName](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#servicename)

  Use a Windows service short name when a service, not an application, is sending or receiving traffic. Service short names are retrieved by running the `Get-Service` command from PowerShell.

- **Protocol**  
  CSP: [FirewallRules/FirewallRuleName/Protocol](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#protocol)

  Specify the protocol for this port rule.
  - Transport layer protocols like *TCP(6)* and *UDP(17)* allow you to specify ports or port ranges.
  - For custom protocols, enter a number between *0* and *255* that represents the IP protocol.
  - When nothing is specified, the rule defaults to **Any**.

- **Interface types**  
  Specify the interface types to which the rule belongs. You can choose one or more of the following. If you don't select an option, the rule applies to all interface types:
  - **Remote access**
  - **Wireless**
  - **Local area network**
  - **Not configured**

- **Authorized users**  
  [FirewallRules/FirewallRuleName/LocalUserAuthorizationList](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#localuserauthorizedlist)

  Specify a list of authorized local users for this rule. A list of authorized users can't be specified if *Service name* in this policy is set as a Windows service. If no authorized user is specified, the default is *all users*.

- **Any local address**  
  **Not configured** (*default*) - Use the following setting, *Local address ranges** to configure a range of addresses to support.
  - **Yes** - Support any local address and don't configure an address range.

- **Local address ranges**  
  CSP: [FirewallRules/FirewallRuleName/LocalAddressRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#localaddressranges)  

  Add one or more addresses as a comma-separated list of local addresses that are covered by the rule. Valid entries (tokens) include the following options:
  - **An asterisk** - An asterisk (\*) indicates any local address. If present, the asterisk must be the only token included.
  - **A subnet** - Specify subnets by using the subnet mask or network prefix notation. If a subnet mask or network prefix isn't specified, the subnet mask defaults to 255.255.255.255.​​
  - **A valid IPv6 address**
  - **An IPv4 address range** - IPv4 ranges must be in the format of *start address - end address* with no spaces included, where the start address is less than the end address.​​
  - **An IPv6 address range** - IPv6 ranges must be in the format of *start address - end address* with no spaces included, where the start address is less than the end address.

  When no value is specified, this setting defaults to use *Any address*.

- **Any remote address**  
  **Not configured** (*default*) - Use the following setting, *Remote address ranges** to configure a range of addresses to support.
  - **Yes** - Support any remote address and don't configure an address range.

- **Remote address ranges**  
  CSP: [FirewallRules/FirewallRuleName/RemoteAddressRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#remoteaddressranges)  

  Add one or more addresses as a comma-separated list of remote addresses that are covered by the rule. Valid entries (tokens) include the following and aren't case-sensitive:
  - **An asterisk** - An asterisk (\*) indicates any remote address. If present, the asterisk must be the only token included.
  - **Defaultgateway**
  - **DHCP**
  - **DNS**
  - **WINS**
  - **Intranet** - Supported on devices that run Windows 1809 or later.
  - **RmtIntranet** - Supported on devices that run Windows 1809 or later.
  - **Ply2Renders** - Supported on devices that run Windows 1809 or later.
  - **LocalSubnet** - Indicates any local address on the local subnet.
  - **A subnet** - Specify subnets by using the subnet mask or network prefix notation. If a subnet mask or a network prefix isn't specified, the subnet mask defaults to 255.255.255.255.​​
  - **A valid IPv6 address**
  - **An IPv4 address range** - IPv4 ranges must be in the format of *start address - end address* with no spaces included, where the start address is less than the end address.​​
  - **An IPv6 address range** - IPv6 ranges must be in the format of *start address - end address* with no spaces included, where the start address is less than the end address.

  When no value is specified, this setting defaults to use *Any address*.

<!-- End of 2005 additions  -->

## Next steps

[Endpoint security policy for firewalls](../protect/endpoint-security-firewall-policy.md)
