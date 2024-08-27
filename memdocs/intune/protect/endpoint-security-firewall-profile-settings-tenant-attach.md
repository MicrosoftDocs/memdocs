---
# required metadata

title: Intune endpoint security firewall settings for Configuration Manager devices| Microsoft Docs
description: Endpoint security firewall policy settings for tenant attached devices you manage with Configuration Manager. You can configure firewall setting after you configure tenant attach for Configuration Manager.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/19/2024
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier3
- M365-identity-device-management
- sub-secure-endpoints
ms.reviewer: laarrizz

---
# Firewall policy settings for tenant attached devices in Microsoft Intune

View the Microsoft Windows Firewall settings you can manage with the **Windows Firewall (ConfigMgr)** profile from Intune. The profile is available when you configure Intune [Firewall policy](../protect/endpoint-security-firewall-policy.md), and the policy deploys to devices you manage with Configuration Manager when you've configured the [tenant attach](../protect/tenant-attach-intune.md) scenario.

## Windows Firewall

- **Certificate revocation list verification (Device)**  
  CSP: [MdmStore/Global/CRLcheck](/windows/client-management/mdm/firewall-csp#crlcheck)

   Specify how certificate revocation list (CRL) verification is enforced.
  - **Not configured** (*default*) - Use the client default, which is to disable CRL verification.
  - **None**
  - **Attempt**
  - **Require**

- **Disable Stateful Ftp (Device)**  
  CSP: [MdmStore/Global/DisableStatefulFtp](/windows/client-management/mdm/firewall-csp#disablestatefulftp)

  - **Not configured** (*default*)
  - **True** - Stateful FTP is disabled
  - **False** - The firewall performs stateful File Transfer Protocol (FTP) filtering to allow secondary connections.

- **Enable Packet Queue (Device)**  
  CSP: [MdmStore/Global/EnablePacketQueue](/windows/client-management/mdm/firewall-csp#enablepacketqueue)

  Select from the following options to configure scaling for the software on the receive side for the encrypted receive and clear text forward for the IPsec tunnel gateway scenario. This ensures the packet order is preserved. By default, no options are selected.

  - **Disabled**
  - **Queue Inbound**
  - **Queue Outbound**

- **IPsec Exceptions (Device)**  
  CSP: [MdmStore/Global/IPsecExempt](/windows/client-management/mdm/firewall-csp#ipsecexempt)

  Select from the following options to configure IPsec exceptions.

  - **Exempt neighbor discover IPv6 ICMP type-codes from IPsec**
  - **Exempt ICMP from IPsec**
  - **Exempt router discover IPv6 ICMP type-codes from IPsec**
  - **Exempt both IPv4 and IPv6 DHCP traffic from IPsec**

- **Opportunistically Match Auth Set Per KM (Device)**  
  CSP: [OpportunisticallyMatchAuthSetPerKM](/windows/client-management/mdm/firewall-csp#opportunisticallymatchauthsetperkm)

  - **Not configured** (*default*)
  - **True**
  - **False**

- **Preshared Key Encoding (Device)**  
  CSP: [MdmStore/Global/PresharedKeyEncoding](/windows/client-management/mdm/firewall-csp#presharedkeyencoding)

  - **Not configured** (*default*)
  - **None**
  - **UTF8**

- **Security association idle time (Device)**  
  CSP: [MdmStore/Global/SaIdleTime](/windows/client-management/mdm/firewall-csp#saidletime)

  Specify a time in seconds between **300** and **3600**, for how long the security associations are kept after network traffic isn't seen.
  If you don't specify any value, the system deletes a security association after it's been idle for *300* seconds.

## Domain Profile

- **Enable Domain Network Firewall (Device)**  
  CSP: [EnableFirewall](/windows/client-management/mdm/firewall-csp#enablefirewall)

  - **Not configured** (*default*) - The client returns to its default, which is to enable the firewall.
  - **True** - The Windows Firewall for the network type of **domain** is turned on and enforced.
  - **False** - Disable the firewall.

  When set to *True*, you can then configure the following settings for this firewall profile type:

  - **Allow Local Ipsec Policy Merge (Device)**  
    CSP: [AllowLocalIpsecPolicyMerge](/windows/client-management/mdm/firewall-csp#allowlocalipsecpolicymerge)

    - **Not configured** (*default*)
    - **True**  
    - **False** - Connection security rules from the local store are ignored and not enforced.

  - **Allow Local Policy Merge (Device)**  
    CSP: [AllowLocalPolicyMerge](/windows/client-management/mdm/firewall-csp#allowlocalpolicymerge)

    - **Not configured** (*default*)  
    - **True**  
    - **False** - Firewall rules from the local store are ignored and not enforced.

  - **Auth Apps Allow User Pref Merge (Device)**  
    CSP: [AuthAppsAllowUserPrefMerge](/windows/client-management/mdm/firewall-csp#authappsallowuserprefmerge)

    - **Not configured** (*default*)  
    - **True**  
    - **False**

  - **Default Inbound Action for Domain Profile (Device)**  
    CSP: [DefaultInboundAction](/windows/client-management/mdm/firewall-csp#defaultinboundaction)

    - **Not configured** (*default*)  
    - **Allow**  
    - **Block**

  - **Default Outbound Action (Device)**  
    CSP: [DefaultOutboundAction](/windows/client-management/mdm/firewall-csp#defaultoutboundaction)

    - **Allow**  
    - **Block**

  - **Disable Inbound Notifications (Device)**  
    CSP: [DisableInboundNotifications](/windows/client-management/mdm/firewall-csp#disableinboundnotifications)

    - **Not configured** (*default*)  
    - **True** - The firewall won't display a notification to the user when an application is blocked from listening on a port.
    - **False** - The firewall might display a notification to the user when an application is blocked from listening on a port.

  - **Disable Stealth Mode (Device)**  
    CSP: [DisableStealthMode](/windows/client-management/mdm/firewall-csp#disablestealthmode)

    - **Not configured** (*default*)  
    - **True**  
    - **False** - The server operates in stealth mode. The firewall rules used to enforce stealth mode are implementation-specific.

  - **Disable Unicast Responses To Multicast Broadcast (Device)**  
    CSP: [DisableUnicastResponsesToMulticastBroadcast](/windows/client-management/mdm/firewall-csp#disableunicastresponsestomulticastbroadcast)

    - **Not configured** (*default*)  
    - **True** - Unicast response to multicast broadcast traffic is blocked.
    - **False**

  - **Global Ports Allow User Pref Merge (Device)**  
    CSP: [GlobalPortsAllowUserPrefMerge](/windows/client-management/mdm/firewall-csp#GlobalPortsAllowUserPrefMerge)

    - **Not configured** (*default*)  
    - **True**  
    - **False** - Global port firewall rules in the local store are ignored and not enforced.

  - **Shielded (Device)**  
    CSP: [Shielded](/windows/client-management/mdm/firewall-csp#shielded)

    - **Not configured** (*default*)  
    - **True** - The server blocks all incoming traffic regardless of other policy settings.
    - **False**

## Private Profile

- **Enable Private Network Firewall (Device)**  
  CSP: [EnableFirewall](/windows/client-management/mdm/firewall-csp#enablefirewall)

  - **Not configured** (*default*) - The client returns to its default, which is to enable the firewall.
  - **True** - The Windows Firewall for the network type of **private** is turned on and enforced.
  - **False** - Disable the firewall.

  When set to *True*, you can then configure the following settings for this firewall profile type:

  - **Allow Local Ipsec Policy Merge (Device)**  
    CSP: [AllowLocalIpsecPolicyMerge](/windows/client-management/mdm/firewall-csp#allowlocalipsecpolicymerge)

    - **Not configured** (*default*)  
    - **True**  
    - **False** - Connection security rules from the local store are ignored and not enforced.

  - **Allow Local Policy Merge (Device)**  
    CSP: [AllowLocalPolicyMerge](/windows/client-management/mdm/firewall-csp#allowlocalpolicymerge)

    - **Not configured** (*default*)  
    - **True**  
    - **False** - Firewall rules from the local store are ignored and not enforced.

  - **Auth Apps Allow User Pref Merge (Device)**  
    CSP: [AuthAppsAllowUserPrefMerge](/windows/client-management/mdm/firewall-csp#authappsallowuserprefmerge)

    - **Not configured** (*default*)  
    - **True**  
    - **False**

  - **Default Inbound Action for Private Profile (Device)**  
    CSP: [DefaultInboundAction](/windows/client-management/mdm/firewall-csp#defaultinboundaction)

    - **Not configured** (*default*)  
    - **Allow**  
    - **Block**

  - **Default Outbound Action (Device)**  
    CSP: [DefaultOutboundAction](/windows/client-management/mdm/firewall-csp#defaultoutboundaction)

    - **Allow**  
    - **Block**

  - **Disable Inbound Notifications (Device)**  
    CSP: [DisableInboundNotifications](/windows/client-management/mdm/firewall-csp#disableinboundnotifications)

    - **Not configured** (*default*)  
    - **True** - The firewall won't display a notification to the user when an application is blocked from listening on a port.
    - **False** - The firewall might display a notification to the user when an application is blocked from listening on a port.

  - **Disable Stealth Mode (Device)**  
    CSP: [DisableStealthMode](/windows/client-management/mdm/firewall-csp#disablestealthmode)

    - **Not configured** (*default*)  
    - **True**  
    - **False** - The server operates in stealth mode. The firewall rules used to enforce stealth mode are implementation-specific.

  - **Disable Unicast Responses To Multicast Broadcast (Device)**  
    CSP: [DisableUnicastResponsesToMulticastBroadcast](/windows/client-management/mdm/firewall-csp#disableunicastresponsestomulticastbroadcast)

    - **Not configured** (*default*)  
    - **True** - Unicast response to multicast broadcast traffic is blocked.
    - **False**

  - **Global Ports Allow User Pref Merge (Device)**  
    CSP: [GlobalPortsAllowUserPrefMerge](/windows/client-management/mdm/firewall-csp#GlobalPortsAllowUserPrefMerge)

    - **Not configured** (*default*)  
    - **True**  
    - **False** - Global port firewall rules in the local store are ignored and not enforced.

  - **Shielded (Device)**  
    CSP: [Shielded](/windows/client-management/mdm/firewall-csp#shielded)

    - **Not configured** (*default*)  
    - **True** - The server blocks all incoming traffic regardless of other policy settings.
    - **False**

## Public Profile

- **Enable Public Network Firewall (Device)**  
  CSP: [EnableFirewall](/windows/client-management/mdm/firewall-csp#enablefirewall)

  - **Not configured** (*default*) - The client returns to its default, which is to enable the firewall.
  - **True** - The Windows Firewall for the network type of **public** is turned on and enforced.
  - **False** - Disable the firewall.

  When set to *True*, you can then configure the following settings for this firewall profile type:

  - **Allow Local Ipsec Policy Merge (Device)**  
    CSP: [AllowLocalIpsecPolicyMerge](/windows/client-management/mdm/firewall-csp#allowlocalipsecpolicymerge)

    - **Not configured** (*default*)  
    - **True**  
    - **False** - Connection security rules from the local store are ignored and not enforced.

  - **Allow Local Policy Merge (Device)**  
    CSP: [AllowLocalPolicyMerge](/windows/client-management/mdm/firewall-csp#allowlocalpolicymerge)

    - **Not configured** (*default*)  
    - **True**  
    - **False** - Firewall rules from the local store are ignored and not enforced.

  - **Auth Apps Allow User Pref Merge (Device)**  
    CSP: [AuthAppsAllowUserPrefMerge](/windows/client-management/mdm/firewall-csp#authappsallowuserprefmerge)

    - **Not configured** (*default*)  
    - **True**  
    - **False**

  - **Default Inbound Action for Public Profile (Device)**  
    CSP: [DefaultInboundAction](/windows/client-management/mdm/firewall-csp#defaultinboundaction)

    - **Not configured** (*default*)  
    - **Allow**  
    - **Block**

  - **Default Outbound Action (Device)**  
    CSP: [DefaultOutboundAction](/windows/client-management/mdm/firewall-csp#defaultoutboundaction)

    - **Allow**  
    - **Block**

  - **Disable Inbound Notifications (Device)**  
    CSP: [DisableInboundNotifications](/windows/client-management/mdm/firewall-csp#disableinboundnotifications)

    - **Not configured** (*default*)  
    - **True** - The firewall won't display a notification to the user when an application is blocked from listening on a port.
    - **False** - The firewall might display a notification to the user when an application is blocked from listening on a port.

  - **Disable Stealth Mode (Device)**  
    CSP: [DisableStealthMode](/windows/client-management/mdm/firewall-csp#disablestealthmode)

    - **Not configured** (*default*)  
    - **True**  
    - **False** - The server operates in stealth mode. The firewall rules used to enforce stealth mode are implementation-specific.

  - **Disable Unicast Responses To Multicast Broadcast (Device)**  
    CSP: [DisableUnicastResponsesToMulticastBroadcast](/windows/client-management/mdm/firewall-csp#disableunicastresponsestomulticastbroadcast)

    - **Not configured** (*default*)  
    - **True** - Unicast response to multicast broadcast traffic is blocked.
    - **False**

  - **Global Ports Allow User Pref Merge (Device)**  
    CSP: [GlobalPortsAllowUserPrefMerge](/windows/client-management/mdm/firewall-csp#GlobalPortsAllowUserPrefMerge)

    - **Not configured** (*default*)  
    - **True**  
    - **False** - Global port firewall rules in the local store are ignored and not enforced.

  - **Shielded (Device)**  
    CSP: [Shielded](/windows/client-management/mdm/firewall-csp#shielded)

    - **Not configured** (*default*)  
    - **True** - The server blocks all incoming traffic regardless of other policy settings.
    - **False**

## Next steps

[Endpoint security policy for firewalls](../protect/endpoint-security-firewall-policy.md)