---
# required metadata

title: Intune endpoint security firewall settings | Microsoft Docs
description: Endpoint security firewall policy settings for Windows and macOS in Microsoft Intune 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
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

    - **Bundle id** - The ID identifies the app. For example: *com.apple.app*

## Microsoft Defender Firewall profile

### Microsoft Defender Firewall

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

- **rn on Microsoft Defender Firewall for domain networks**  
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

## Next steps

[Endpoint security policy for firewalls](../protect/endpoint-security-policy.md#firewall-policy)
