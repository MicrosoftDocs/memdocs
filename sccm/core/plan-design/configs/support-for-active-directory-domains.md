---
title: "Supported Active Directory domains"
titleSuffix: "Configuration Manager"
description: "Get requirements for the membership of a System Center Configuration Manager site system in an Active Directory domain."
ms.custom: na
ms.date: 9/18/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8c5a13f8-42d5-4898-b7b6-e594dae8b335
caps.latest.revision: 7
caps.handback.revision: 0
author: mstewart
ms.author: mstewart
manager: angrobe

---
# Supported Active Directory domains for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

All System Center Configuration Manager site systems must be members of a supported Windows Server Active Directory domain. Configuration Manager client computers can be domain members or workgroup members.  

 **Requirements and limitations:**  

-   Domain membership applies to site systems that support Internet-based client management in a perimeter network (also known as a DMZ, demilitarized zone, and screened subnet).  

-   It's not supported to change the following for a computer that hosts a site system role:  

    -   Domain membership *(This includes removing a site system from the domain, and then rejoining the same domain.)*

    -   Domain name  

    -   Computer name  

You must uninstall the site system role (including the site if it's a site server) before making these changes.  

**Domains with the following domain functional levels are supported:**  
- Windows Server 2016

- Windows Server 2012 R2  

- Windows Server 2012

- Windows Server 2008 R2

- Windows Server 2008  







##  <a name="bkmk_Disjoint"></a> Disjoint namespace  
Configuration Manager supports installing site systems and clients in a domain that has a disjoint namespace.  

A disjoint namespace scenario is one in which the primary Domain Name System (DNS) suffix of a computer doesn't match the Active Directory DNS domain name where that computer resides. The computer that uses the primary DNS suffix that doesn't match is said to be disjoint. Another disjoint namespace scenario occurs if the NetBIOS domain name of a domain controller doesn't match the Active Directory DNS domain name.  

The following table identifies the supported scenarios for a disjoint namespace.  

|Scenario|More information|  
|--------------|----------------------|  
|**Scenario 1:**<br /><br /> The primary DNS suffix of the domain controller differs from the Active Directory DNS domain name. Computers that are members of the domain can be either disjoint or not disjoint.|In this scenario, the primary DNS suffix of the domain controller differs from the Active Directory DNS domain name. The domain controller is disjoint in this scenario. Computers that are members of the domain, such as site servers and computers, can have a primary DNS suffix that either matches the primary DNS suffix of the domain controller or matches the Active Directory DNS domain name.|  
|**Scenario 2:**<br /><br /> A member computer in an Active Directory domain is disjoint, even though the domain controller is not disjoint.|In this scenario, the primary DNS suffix of a member computer on which a site system is installed differs from the Active Directory DNS domain name, even though the primary DNS suffix of the domain controller is the same as the Active Directory DNS domain name. In this scenario, you have a domain controller that is not disjoint and a member computer that is disjoint. Member computers that are running the Configuration Manager client can have a primary DNS suffix that either matches the primary DNS suffix of the disjoint site system server or matches the Active Directory DNS domain name.|  

 To allow a computer to access domain controllers that are disjoint, you must change the **msDS-AllowedDNSSuffixes** Active Directory attribute on the domain object container. You must add both DNS suffixes to the attribute.  

 In addition, to make sure that the DNS suffix search list contains all the DNS namespaces that are deployed within the organization, you must configure the search list for each computer in the domain that is disjoint. Make sure that you include the following in the list of namespaces: the primary DNS suffix of the domain controller, the DNS domain name, and any additional namespaces for other servers that Configuration Manager might interoperate with. You can use the Group Policy Management console to configure the **Domain Name System (DNS) suffix search** list.  

> [!IMPORTANT]  
>  When you reference a computer in Configuration Manager, enter the computer by using its Primary DNS suffix. This suffix should match the Fully Qualified Domain Name that is registered as the **dnsHostName** attribute in the Active Directory domain and the Service Principal Name that is associated with the system.  

##  <a name="bkmk_SLD"></a> Single label domains  
 Configuration Manager supports site systems and clients in a single label domain when the following criteria are met:  

-   The single label domain in Active Directory Domain Services must be configured with a disjoint DNS namespace that has a valid top-level domain.  

     **For example:** The single label domain of Contoso is configured to have a disjoint namespace in DNS of contoso.com. Therefore, when you specify the DNS suffix in Configuration Manager for a computer in the Contoso domain, you specify "Contoso.com" and not "Contoso".  

-   The Distributed Component Object Model (DCOM) connections between site servers in the system context must be successful by using Kerberos authentication.  
