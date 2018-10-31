---
title: Fundamentals of security
titleSuffix: Configuration Manager
description: Learn about the layers of security in Configuration Manager.
ms.date: 10/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 035b7f73-8b78-4ed1-835e-a31f9a5c4a02
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Fundamentals of security for Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

This article summarizes the following fundamental security components of any Configuration Manager environment:
- [Security layers](#bkmk_layers)
- [Role-based administration](#bkmk_rba)
- [Securing client endpoints](#bkmk_endpoints)
- [Configuration Manager accounts and groups](#bkmk_accounts)
- [Privacy](#bkmk_privacy)

## <a name="bkmk_layers"></a> Security layers

Security for Configuration Manager consists of the following layers: 
- [Windows OS and network security](#bkmk_layer-windows)
- [Network infrastructure: firewalls, intrusion detection, public key infrastructure (PKI)](#bkmk_layer-network)
- [Configuration Manager security controls](#bkmk_layer-cm)
- [SMS Provider](#bkmk_layer-provider)
- [Site database permissions](#bkmk_layer-db)

#### <a name="bkmk_layer-windows"></a> Windows OS and network security
The first layer is provided by Windows security features for both the OS and the network. This layer includes the following components:  

-   File sharing to transfer files between Configuration Manager components  

-   Access Control Lists (ACLs) to help secure files and registry keys  

-   Internet Protocol Security (IPsec) to help secure communications  

-   Group Policy to set security policy  

-   Distributed Component Object Model (DCOM) permissions for distributed applications, like the Configuration Manager console  

-   Active Directory Domain Services to store security principals  

-   Windows account security, including some groups that Configuration Manager creates during setup  

#### <a name="bkmk_layer-network"></a> Network infrastructure

Additional security components, like firewalls and intrusion detection, help provide defense for the whole environment. Certificates issued by industry standard public key infrastructure (PKI) implementations help provide authentication, signing, and encryption.  

#### <a name="bkmk_layer-cm"></a> Configuration Manager security controls

In addition to security provided by the Windows server and network infrastructure, Configuration Manager controls access to its console and resources in several ways. By default, only local administrators have rights to the files and registry keys that the Configuration Manager console requires on computers where you install it.  

#### <a name="bkmk_layer-provider"></a> SMS Provider

The next layer of security is based on access through Windows Management Instrumentation (WMI), specifically the SMS Provider. The SMS Provider is a Configuration Manager component that grants a user access to query the site database for information. By default, access to the provider is restricted to members of the local SMS Admins group. This group at first contains only the user who installed Configuration Manager. To grant other accounts permission to the Common Information Model (CIM) repository and the SMS Provider, add the other accounts to the SMS Admins group.  

For more information, see [Plan for the SMS Provider](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider).

#### <a name="bkmk_layer-db"></a> Site database permissions

The final layer of security is based on permissions to objects in the site database. By default, the Local System account and the user account that you used to install Configuration Manager can administer all objects in the site database. Grant and restrict permissions to additional administrative users in the Configuration Manager console by using role-based administration.  



## <a name="bkmk_rba"></a> Role-based administration  

 Configuration Manager uses role-based administration to help secure objects like collections, deployments, and sites. This administration model centrally defines and manages hierarchy-wide security access settings for all sites and site settings. 

 An administrator assigns *security roles* to administrative users and group permissions. The permissions are connected to different Configuration Manager object types, for example, to create or change client settings. 

 *Security scopes* group specific instances of objects that an administrative user is responsible to manage, like an application that installs Microsoft Office. 

 The combination of security roles, security scopes, and collections define the objects that an administrative user can view and manage. Configuration Manager installs some default security roles for typical management tasks. Create your own security roles to support your specific business requirements.  

 For more information, see [Configure role-based administration](/sccm/core/servers/deploy/configure/configure-role-based-administration).  



## <a name="bkmk_endpoints"></a> Securing client endpoints  

 Configuration Manager secures client communication to site system roles by using either self-signed or PKI certificates, or Azure Active Directory (Azure AD) tokens. Some scenarios require the use of PKI certificates. For example, [internet-based client management](/sccm/core/clients/manage/plan-internet-based-client-management), and for [mobile device clients](/sccm/mdm/plan-design/plan-on-premises-mdm).  

 You can configure the site system roles to which clients connect for either HTTPS or HTTP client communication. Client computers always communicate by using the most secure method that's available. Client computers only fall back to using the less secure communication method if you have site systems roles that allow HTTP communication.  

 For more information, see [Plan for security](/sccm/core/plan-design/security/plan-for-security).



## <a name="bkmk_accounts"></a> Configuration Manager accounts and groups  

 Configuration Manager uses the Local System account for most site operations. Some management tasks might require you to create and maintain additional accounts. Configuration Manager creates several default groups and SQL Server roles during setup. You might have to manually add computer or user accounts to the default groups and SQL Server roles.  

 For more information, see [Accounts used in Configuration Manager](/sccm/core/plan-design/hierarchy/accounts).  



## <a name="bkmk_privacy"></a> Privacy  

 Before you implement Configuration Manager, consider your privacy requirements. Although enterprise management products offer many advantages because they can effectively manage lots of clients, this software might affect the privacy of users in your organization. Configuration Manager includes many tools to collect data and monitor devices. Some tools might raise privacy concerns in your organization.  

 For example, when you install the Configuration Manager client, it enables many management settings by default. This configuration causes the client software to send information to the Configuration Manager site. The site stores client information in the site database. The client information isn't directly sent to Microsoft. For more information, see [Diagnostics and usage data](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).



## See also

- [Plan for security](/sccm/core/plan-design/security/plan-for-security)  

- [Security and privacy for Configuration Manager clients](/sccm/core/clients/deploy/plan/security-and-privacy-for-clients)  

- [Configure security](/sccm/core/plan-design/security/configure-security)   

- [Communication between endpoints](/sccm/core/plan-design/hierarchy/communications-between-endpoints)  

- [Cryptographic controls technical reference](/sccm/core/plan-design/security/cryptographic-controls-tehnical-reference)  
