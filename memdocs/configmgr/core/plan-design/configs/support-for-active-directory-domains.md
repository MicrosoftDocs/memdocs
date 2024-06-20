---
title: Support for Active Directory domains
titleSuffix: Configuration Manager
description: Learn about the requirements for a Configuration Manager site system in an Active Directory domain.
ms.date: 10/22/2019
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Support for Active Directory domains in Configuration Manager

*Applies to: Configuration Manager (current branch)*

All Configuration Manager site systems must be members of a supported Active Directory domain. Configuration Manager client computers can be domain members or workgroup members.  

## Requirements and limitations

- Domain membership also applies to site systems that support internet-based client management in a perimeter network. (These networks are also known as a DMZ, demilitarized zone, and screened subnet).  

- It's not supported to change the following configurations for a computer that hosts a site system role:  

  - Domain membership, including if you remove a site system from the domain, and then rejoin the same domain.

  - Domain name  

  - Computer name  

  Before making these changes, uninstall the site system role. To make these changes to a site server, uninstall the site first. You can also consider creating a [site server in passive mode](../../servers/deploy/configure/site-server-high-availability.md) to help manage this change on a site server.

- Configuration Manager supports domain and forest functional level of Windows Server 2008 R2 or later.<!-- SCCMDocs#1853 -->

## <a name="bkmk_Disjoint"></a> Disjoint namespace

You can install Configuration Manager site systems and clients in a domain that has a *disjoint namespace*.  

In a disjoint namespace, the primary DNS suffix of a computer doesn't match the Active Directory DNS domain name of that computer. Another disjoint namespace scenario occurs if the NetBIOS domain name of a domain controller doesn't match the Active Directory DNS domain name.  

### Disjoint scenarios

The following sections identify the supported scenarios for a disjoint namespace.  

#### Scenario 1

The primary DNS suffix of the domain controller differs from the Active Directory DNS domain name. Computers that are members of the domain can be either disjoint or not disjoint.

The domain controller is disjoint in this scenario. Computers that are members of the domain, such as site servers and computers, can have a primary DNS suffix that either matches:

- The primary DNS suffix of the domain controller
- The Active Directory DNS domain name

#### Scenario 2

A member computer in an Active Directory domain is disjoint, even though the domain controller isn't disjoint.

In this scenario, the primary DNS suffix of a site system differs from the Active Directory DNS domain name. The primary DNS suffix of the domain controller is the same as the Active Directory DNS domain name. Member computers that are Configuration Manager clients can have a primary DNS suffix that either matches:

- The primary DNS suffix of the disjoint site system server
- The Active Directory DNS domain name

### Configure disjoint namespace

To allow a computer to access domain controllers that are disjoint, change the **msDS-AllowedDNSSuffixes** Active Directory attribute on the domain object container. Add both DNS suffixes to the attribute.  

To make sure that the *DNS suffix search list* contains all the DNS namespaces in the organization, configure the search list for each computer in the disjoint domain. Include the following suffixes in the list of namespaces:

- The primary DNS suffix of the domain controller
- The DNS domain name
- Any additional namespaces for other servers that Configuration Manager might communicate with

You can use group policy to configure the **Domain Name System (DNS) suffix search** list.  

> [!IMPORTANT]  
> When you reference a computer in Configuration Manager, enter the computer by using its primary DNS suffix. This suffix should match the fully qualified domain name that's registered as the **dnsHostName** attribute in the Active Directory domain and the service principal name that's associated with the system.  

## <a name="bkmk_SLD"></a> Single label domains

Configuration Manager supports site systems and clients in a single label domain when the following criteria are met:  

- Configure the single label domain in Active Directory Domain Services with a disjoint DNS namespace that has a valid top-level domain.  

  **For example:** The single label domain of Contoso is configured to have a disjoint namespace in DNS of contoso.com. When you specify the DNS suffix in Configuration Manager for a computer in the Contoso domain, you specify "Contoso.com" and not "Contoso".  

- The distributed component object model (DCOM) connections between site servers in the system context must be successful by using Kerberos authentication.  
