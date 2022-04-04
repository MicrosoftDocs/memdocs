---
# required metadata

title: Intune endpoint security firewall settings | Microsoft Docs
description: Endpoint security firewall policy settings for Windows and macOS in Microsoft Intune 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/04/2022
ms.topic: conceptual
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
ms.reviewer: aanavath

---
# Firewall policy settings for endpoint security in Intune

> [!NOTE]  
> Beginning on April 5, 2022, the *Windows 10 and later* platform and profiles for Windows devices were replaced by the *Windows 10, Windows 11, and Windows Server* platform and new instances of those same profiles. Although you can no longer create new instances of the original profile, you can continue to edit and use your existing profiles. The settings details for Windows profiles in this article apply to those deprecated profiles.
 
View the settings you can configure in profiles for *Firewall* policy in the endpoint security node of Intune as part of an [Endpoint security policy](../protect/endpoint-security-policy.md).

Applies to:

- macOS
- Windows 10
- Windows 11

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

The following settings are configured as [Endpoint Security policy for Windows Firewalls](../protect/endpoint-security-firewall-policy.md).

- **Stateful File Transfer Protocol (FTP)**  
  CSP: [MdmStore/Global/DisableStatefulFtp](/windows/client-management/mdm/firewall-csp#disablestatefulftp)

  - **Not configured** (*default*)
  - **Allow** - The firewall performs stateful File Transfer Protocol (FTP) filtering to allow secondary connections. 
  - **Disabled** - Stateful FTP is disabled.

- **Number of seconds a security association can be idle before it's deleted**  
  CSP: [MdmStore/Global/SaIdleTime](/windows/client-management/mdm/firewall-csp#saidletime)

  Specify a time in seconds between 300 and 3600, for how long the security associations are kept after network traffic isn't seen.
  
  If you don't specify any value, the system deletes a security association after it's been idle for 300 seconds.
  
- **Preshared key encoding**  
  CSP: [MdmStore/Global/PresharedKeyEncoding](/windows/client-management/mdm/firewall-csp#presharedkeyencoding)

  If you don't require *UTF-8*, preshared keys are initially encoded using UTF-8. After that, device users can choose another encoding method.

  - **Not configured** (*default*)
  - **None**
  - **UTF8**

- **No exemptions for Firewall IP sec**  
  - **Not configured** (*default*) - When not configured, you'll have access to the following IP sec exemption settings that you can configure individually.
  - **Yes** - Turn off all Firewall IP sec exemptions. The following settings aren't available to configure.

  - **Firewall IP sec exemptions allow neighbor discovery**  
    CSP: [MdmStore/Global/IPsecExempt](/windows/client-management/mdm/firewall-csp#ipsecexempt)

    - **Not configured** (*default*)
    - **Yes** - Firewall IPsec exemptions allow neighbor discovery.

  - **Firewall IP sec exemptions allow ICMP**  
    CSP: [MdmStore/Global/IPsecExempt](/windows/client-management/mdm/firewall-csp#ipsecexempt)

    - **Not configured** (*default*)
    - **Yes** - Firewall IPsec exemptions allow ICMP.

  - **Firewall IP sec exemptions allow router discovery**  
    CSP: [MdmStore/Global/IPsecExempt](/windows/client-management/mdm/firewall-csp#ipsecexempt)

    - **Not configured** (*default*)
    - **Yes** - Firewall IPsec exemptions allow router discovery.

  - **Firewall IP sec exemptions allow DHCP**  
    CSP: [MdmStore/Global/IPsecExempt](/windows/client-management/mdm/firewall-csp#ipsecexempt)

    - **Not configured** (*default*)
    - **Yes** - Firewall IP sec exemptions allow DHCP

- **Certificate revocation list (CRL) verification**  
  CSP: [MdmStore/Global/CRLcheck](/windows/client-management/mdm/firewall-csp#crlcheck)

   Specify how certificate revocation list (CRL) verification is enforced.
  - **Not configured** (*default*) - Use the client default, which is to disable CRL verification.
  - **None**
  - **Attempt**
  - **Require**

- **Require keying modules to only ignore the authentication suites they don’t support**  
  CSP: [MdmStore/Global/OpportunisticallyMatchAuthSetPerKM](/windows/client-management/mdm/firewall-csp#opportunisticallymatchauthsetperkm)

  - **Not configured** (*default*)
  - **Disabled**
  - **Enabled** - Keying modules ignore unsupported authentication suites.

- **Packet queuing**  
  CSP: [MdmStore/Global/EnablePacketQueue](/windows/client-management/mdm/firewall-csp#enablepacketqueue)

  Specify how to enable scaling for the software on the receive side for the encrypted receive and clear text forward for the IPsec tunnel gateway scenario. This ensures the packet order is preserved.
  - **Not configured** (*default*) - Packet queuing is returned to the client default, which is disabled.
  - **Disabled**
  - **Queue Inbound**
  - **Queue Outbound**
  - **Queue Both**

- **Turn on Microsoft Defender Firewall for domain networks**  
  CSP: [EnableFirewall](/windows/client-management/mdm/firewall-csp#enablefirewall)

  - **Not configured** (*default*) - The client returns to its default, which is to enable the firewall.
  - **Yes** - The Microsoft Defender Firewall for the network type of **domain** is turned on and enforced. You also gain access to additional settings for this network.
  - **No** - Disable the firewall.

  Additional settings for this network, when set to *Yes*:

  - **Block stealth mode**  
    CSP: [DisableStealthMode](/windows/client-management/mdm/firewall-csp#disablestealthmode)

    By default, stealth mode is enabled on devices. It helps prevent malicious users from discovering information about network devices and the services they run. Disabling stealth mode can make devices vulnerable to attack.
    - **Not configured** *(default)*
    - **Yes**
    - **No**

  - **Enable shielded mode**  
    CSP: [Shielded](/windows/client-management/mdm/firewall-csp#shielded)

    - **Not configured** *(default)* - Use the client default, which is to disable shielded mode.
    - **Yes** - The machine is put into *shielded mode*, which isolates it from the network. All traffic is blocked.
    - **No**

  - **Block unicast responses to multicast broadcasts**  
      CSP: [DisableUnicastResponsesToMulticastBroadcast](/windows/client-management/mdm/firewall-csp#disableunicastresponsestomulticastbroadcast)

    - **Not configured** *(default)* - The setting returns to the client default, which is to allow unicast responses.
    - **Yes** - Unicast responses to multicast broadcasts are blocked.
    - **No** - Enforce the client default, which is to allow unicast responses.

  - **Disable inbound notifications**  
    CSP [DisableInboundNotifications](/windows/client-management/mdm/firewall-csp#disableinboundnotifications)
    - **Not configured** *(default)* - The setting returns to the client default, which is to allow the user notification.
    - **Yes** - User notification is suppressed when an application is blocked by an inbound rule.
    - **No** - User notifications are allowed.

  - **Block outbound connections**  

    *This setting applies to Windows version 1809 and later*.
    CSP: [DefaultOutboundAction](/windows/client-management/mdm/firewall-csp#defaultoutboundaction)

    This rule is evaluated at the very end of the rule list.
    - **Not configured** *(default)* - The setting returns to the client default, which is to allow connections.
    - **Yes** - All outbound connections that don't match an outbound rule are blocked.
    - **No** - All connections that don't match an outbound rule are allowed.

  - **Block inbound connections**  
    CSP: [DefaultInboundAction](/windows/client-management/mdm/firewall-csp#defaultinboundaction)

    This rule is evaluated at the very end of the rule list.
    - **Not configured** *(default)* - The setting returns to the client default, which is to block connections.
    - **Yes** - All inbound connections that don't match an inbound rule are blocked.
    - **No** - All connections that don't match an inbound rule are allowed.

  - **Ignore authorized application firewall rules**  
    CSP: [AuthAppsAllowUserPrefMerge](/windows/client-management/mdm/firewall-csp#authappsallowuserprefmerge)

    - **Not configured** *(default)* - The setting returns to the client default, which is to honor the local rules.
    - **Yes** - Authorized application firewall rules in the local store are ignored.
    - **No** -  Authorized application firewall rules are honored.

  - **Ignore global port firewall rules**  
    CSP: [GlobalPortsAllowUserPrefMerge](/windows/client-management/mdm/firewall-csp#globalportsallowuserprefmerge)

    - **Not configured** *(default)* - The setting returns to the client default, which is to honor the local rules.
    - **Yes** - Global port firewall rules in the local store are ignored.
    - **No** - The global port firewall rules are honored.

  - **Ignore all local firewall rules**  
    CSP: [IPsecExempt](/windows/client-management/mdm/firewall-csp#allowlocalpolicymerge)

    - **Not configured** *(default)* - The setting returns to the client default, which is to honor the local rules.
    - **Yes** - All firewall rules in the local store are ignored.
    - **No** - The firewall rules in the local store are honored.

  - **Ignore connection security rules**
    CSP: [AllowLocalIpsecPolicyMerge](/windows/client-management/mdm/firewall-csp#allowlocalipsecpolicymerge)

    - **Not configured** *(default)* - The setting returns to the client default, which is to honor the local rules.
    - **Yes** - IPsec firewall rules in the local store are ignored.
    - **No** - IPsec firewall rules in the local store are honored.

- **Turn on Microsoft Defender Firewall for private networks**  
  CSP: [EnableFirewall](/windows/client-management/mdm/firewall-csp#enablefirewall)

  - **Not configured** (*default*) - The client returns to its default, which is to enable the firewall.
  - **Yes** - The Microsoft Defender Firewall for the network type of **private** is turned on and enforced. You also gain access to additional settings for this network.
  - **No** - Disable the firewall.

  Additional settings for this network, when set to *Yes*:

  - **Block stealth mode**  
    CSP: [DisableStealthMode](/windows/client-management/mdm/firewall-csp#disablestealthmode)

    By default, stealth mode is enabled on devices. It helps prevent malicious users from discovering information about network devices and the services they run. Disabling stealth mode can make devices vulnerable to attack.
    - **Not configured** *(default)*
    - **Yes**
    - **No**

  - **Enable shielded mode**  
    CSP: [Shielded](/windows/client-management/mdm/firewall-csp#shielded)

    - **Not configured** *(default)* - Use the client default, which is to disable shielded mode.
    - **Yes** - The machine is put into *shielded mode*, which isolates it from the network. All traffic is blocked.
    - **No**

  - **Block unicast responses to multicast broadcasts**  
      CSP: [DisableUnicastResponsesToMulticastBroadcast](/windows/client-management/mdm/firewall-csp#disableunicastresponsestomulticastbroadcast)

    - **Not configured** *(default)* - The setting returns to the client default, which is to allow unicast responses.
    - **Yes** - Unicast responses to multicast broadcasts are blocked.
    - **No** - Enforce the client default, which is to allow unicast responses.

  - **Disable inbound notifications**  
    CSP [DisableInboundNotifications](/windows/client-management/mdm/firewall-csp#disableinboundnotifications)
    - **Not configured** *(default)* - The setting returns to the client default, which is to allow the user notification.
    - **Yes** - User notification is suppressed when an application is blocked by an inbound rule.
    - **No** - User notifications are allowed.

  - **Block outbound connections**  

    *This setting applies to Windows version 1809 and later*.
    CSP: [DefaultOutboundAction](/windows/client-management/mdm/firewall-csp#defaultoutboundaction)

    This rule is evaluated at the very end of the rule list.
    - **Not configured** *(default)* - The setting returns to the client default, which is to allow connections.
    - **Yes** - All outbound connections that don't match an outbound rule are blocked.
    - **No** - All connections that don't match an outbound rule are allowed.

  - **Block inbound connections**  
    CSP: [DefaultInboundAction](/windows/client-management/mdm/firewall-csp#defaultinboundaction)

    This rule is evaluated at the very end of the rule list.
    - **Not configured** *(default)* - The setting returns to the client default, which is to block connections.
    - **Yes** - All inbound connections that don't match an inbound rule are blocked.
    - **No** - All connections that don't match an inbound rule are allowed.

  - **Ignore authorized application firewall rules**  
    CSP: [AuthAppsAllowUserPrefMerge](/windows/client-management/mdm/firewall-csp#authappsallowuserprefmerge)

    - **Not configured** *(default)* - The setting returns to the client default, which is to honor the local rules.
    - **Yes** - Authorized application firewall rules in the local store are ignored.
    - **No** -  Authorized application firewall rules are honored.

  - **Ignore global port firewall rules**  
    CSP: [GlobalPortsAllowUserPrefMerge](/windows/client-management/mdm/firewall-csp#globalportsallowuserprefmerge)

    - **Not configured** *(default)* - The setting returns to the client default, which is to honor the local rules.
    - **Yes** - Global port firewall rules in the local store are ignored.
    - **No** - The global port firewall rules are honored.

  - **Ignore all local firewall rules**  
    CSP: [IPsecExempt](/windows/client-management/mdm/firewall-csp#allowlocalpolicymerge)

    - **Not configured** *(default)* - The setting returns to the client default, which is to honor the local rules.
    - **Yes** - All firewall rules in the local store are ignored.
    - **No** - The firewall rules in the local store are honored.

  - **Ignore connection security rules**
    CSP: [AllowLocalIpsecPolicyMerge](/windows/client-management/mdm/firewall-csp#allowlocalipsecpolicymerge)

    - **Not configured** *(default)* - The setting returns to the client default, which is to honor the local rules.
    - **Yes** - IPsec firewall rules in the local store are ignored.
    - **No** - IPsec firewall rules in the local store are honored.

- **Turn on Microsoft Defender Firewall for public networks**  
  CSP: [EnableFirewall](/windows/client-management/mdm/firewall-csp#enablefirewall)

  - **Not configured** (*default*) - The client returns to its default, which is to enable the firewall.
  - **Yes** - The Microsoft Defender Firewall for the network type of **public** is turned on and enforced. You also gain access to additional settings for this network.
  - **No** - Disable the firewall.

  Additional settings for this network, when set to *Yes*:

  - **Block stealth mode**  
    CSP: [DisableStealthMode](/windows/client-management/mdm/firewall-csp#disablestealthmode)

    By default, stealth mode is enabled on devices. It helps prevent malicious users from discovering information about network devices and the services they run. Disabling stealth mode can make devices vulnerable to attack.
    - **Not configured** *(default)*
    - **Yes**
    - **No**

  - **Enable shielded mode**  
    CSP: [Shielded](/windows/client-management/mdm/firewall-csp#shielded)

    - **Not configured** *(default)* - Use the client default, which is to disable shielded mode.
    - **Yes** - The machine is put into *shielded mode*, which isolates it from the network. All traffic is blocked.
    - **No**

  - **Block unicast responses to multicast broadcasts**  
      CSP: [DisableUnicastResponsesToMulticastBroadcast](/windows/client-management/mdm/firewall-csp#disableunicastresponsestomulticastbroadcast)

    - **Not configured** *(default)* - The setting returns to the client default, which is to allow unicast responses.
    - **Yes** - Unicast responses to multicast broadcasts are blocked.
    - **No** - Enforce the client default, which is to allow unicast responses.

  - **Disable inbound notifications**  
    CSP [DisableInboundNotifications](/windows/client-management/mdm/firewall-csp#disableinboundnotifications)
    - **Not configured** *(default)* - The setting returns to the client default, which is to allow the user notification.
    - **Yes** - User notification is suppressed when an application is blocked by an inbound rule.
    - **No** - User notifications are allowed.

  - **Block outbound connections**  

    *This setting applies to Windows version 1809 and later*.
    CSP: [DefaultOutboundAction](/windows/client-management/mdm/firewall-csp#defaultoutboundaction)

    This rule is evaluated at the very end of the rule list.
    - **Not configured** *(default)* - The setting returns to the client default, which is to allow connections.
    - **Yes** - All outbound connections that don't match an outbound rule are blocked.
    - **No** - All connections that don't match an outbound rule are allowed.

  - **Block inbound connections**  
    CSP: [DefaultInboundAction](/windows/client-management/mdm/firewall-csp#defaultinboundaction)

    This rule is evaluated at the very end of the rule list.
    - **Not configured** *(default)* - The setting returns to the client default, which is to block connections.
    - **Yes** - All inbound connections that don't match an inbound rule are blocked.
    - **No** - All connections that don't match an inbound rule are allowed.

  - **Ignore authorized application firewall rules**  
    CSP: [AuthAppsAllowUserPrefMerge](/windows/client-management/mdm/firewall-csp#authappsallowuserprefmerge)

    - **Not configured** *(default)* - The setting returns to the client default, which is to honor the local rules.
    - **Yes** - Authorized application firewall rules in the local store are ignored.
    - **No** -  Authorized application firewall rules are honored.

  - **Ignore global port firewall rules**  
    CSP: [GlobalPortsAllowUserPrefMerge](/windows/client-management/mdm/firewall-csp#globalportsallowuserprefmerge)

    - **Not configured** *(default)* - The setting returns to the client default, which is to honor the local rules.
    - **Yes** - Global port firewall rules in the local store are ignored.
    - **No** - The global port firewall rules are honored.

  - **Ignore all local firewall rules**  
    CSP: [IPsecExempt](/windows/client-management/mdm/firewall-csp#allowlocalpolicymerge)

    - **Not configured** *(default)* - The setting returns to the client default, which is to honor the local rules.
    - **Yes** - All firewall rules in the local store are ignored.
    - **No** - The firewall rules in the local store are honored.

  - **Ignore connection security rules**
    CSP: [AllowLocalIpsecPolicyMerge](/windows/client-management/mdm/firewall-csp#allowlocalipsecpolicymerge)

    - **Not configured** *(default)* - The setting returns to the client default, which is to honor the local rules.
    - **Yes** - IPsec firewall rules in the local store are ignored.
    - **No** - IPsec firewall rules in the local store are honored.

### Microsoft Defender Firewall rules

*This profile is in Preview*.

The following settings are configured as [Endpoint Security policy for Windows Firewalls](../protect/endpoint-security-firewall-policy.md).

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

#### Application settings

Applications targeted with this rule:

- **Package family name**  
  [Get-AppxPackage](/previous-versions//hh856044(v=technet.10))

  Package family names can be retrieved by running the Get-AppxPackage command from PowerShell.

- **File path**  
  CSP: [FirewallRules/FirewallRuleName/App/FilePath](/windows/client-management/mdm/firewall-csp#filepath)

  To specify the file path of an app, enter the apps location on the client device. For example: `C:\Windows\System\Notepad.exe` or `%WINDIR%\Notepad.exe`

- **Service name**  
  [FirewallRules/FirewallRuleName/App/ServiceName](/windows/client-management/mdm/firewall-csp#servicename)

  Use a Windows service short name when a service, not an application, is sending or receiving traffic. Service short names are retrieved by running the `Get-Service` command from PowerShell.

#### Port and protocol settings

Specify the local and remote ports to which this rule applies:

- **Protocol**  
  CSP: [FirewallRules/FirewallRuleName/Protocol](/windows/client-management/mdm/firewall-csp#protocol)

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
  [FirewallRules/FirewallRuleName/LocalUserAuthorizationList](/windows/client-management/mdm/firewall-csp#localuserauthorizedlist)

  Specify a list of authorized local users for this rule. A list of authorized users can't be specified if *Service name* in this policy is set as a Windows service. If no authorized user is specified, the default is *all users*.

#### IP address settings

Specifies the local and remote addresses to which this rule applies:

- **Any local address**  
  **Not configured** (*default*) - Use the following setting, *Local address ranges** to configure a range of addresses to support.
  - **Yes** - Support any local address and don't configure an address range.

- **Local address ranges**  
  CSP: [FirewallRules/FirewallRuleName/LocalAddressRanges](/windows/client-management/mdm/firewall-csp#localaddressranges)  

  Manage local address ranges for this rule. You can:
  - **Add** one or more addresses as a comma-separated list of local addresses that are covered by the rule.
  - **Import** a .csv file that contains a list of addresses to use as local address ranges.
  - **Export** your current list of local address ranges as a .csv file.

  Valid entries (tokens) include the following options:
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
  CSP: [FirewallRules/FirewallRuleName/RemoteAddressRanges](/windows/client-management/mdm/firewall-csp#remoteaddressranges)  

  Manage remote address ranges for this rule. You can:
  - **Add** one or more addresses as a comma-separated list of remote addresses that are covered by the rule.
  - **Import** a .csv file that contains a list of addresses to use as remote address ranges.
  - **Export** your current list of remote address ranges as a .csv file.

  Valid entries (tokens) include the following and aren't case-sensitive:
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