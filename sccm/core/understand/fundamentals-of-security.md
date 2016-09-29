---
title: "Fundamentals of security | System Center Configuration Manager"
ms.custom: na
ms.date: 04/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 035b7f73-8b78-4ed1-835e-a31f9a5c4a02
caps.latest.revision: 5
author: Brendunsmanager: angrobe

---
# Fundamentals of security for System Center Configuration Manager
Security for System Center Configuration Manager consists of several layers. The first layer is provided by Windows security features for both the operating system and the network and include:  

-   File sharing to transfer files between Configuration Manager components  

-   Access Control Lists (ACLs) to help secure files and registry keys  

-   IPsec for securing communications  

-   Group Policy for setting security policy  

-   DCOM permissions for distributed applications, such as the Configuration Manager console  

-   Active Directory Domain Services to store security principals  

-   Windows account security, including some groups that are created during Configuration Manager Setup  

Then, additional security components, such as firewalls and intrusion detection, help provide defense in depth for the whole environment. Certificates issued by industry standard PKI implementations help provide authentication, signing, and encryption.  

In addition to security provided by the Windows server and network infrastructure, Configuration Manager controls access to the Configuration Manager console and its resources in several ways. By default, only local Administrators have rights to the files and registry keys required to run the Configuration Manager console on computers where it is installed.  

The next layer of security is based on access through Windows Management Instrumentation (WMI), specifically the **SMS Provider**. The SMS Provider is a Configuration Manager component that grants a user access to query the site database for information. By default, access to the provider is restricted to members of the local **SMS Admins** group. This group at first contains only the user who installed Configuration Manager. To grant other accounts permission to the Common Information Model (CIM) repository and the SMS Provider, add the other accounts to the SMS Admins group.  

The final layer of security is based on permissions to objects in the site database. By default, the Local System account and the user account that you used to install Configuration Manager can administer all objects in the site database. You can grant and restrict permissions to additional administrative users in the Configuration Manager console by using **role-based administration**.  

The remainder of this topic discusses aspects of security related to Configuration Manager.  

## Role-based administration  
 Configuration Manager uses role-based administration to help secure objects such as collections, deployments, and sites. This administration model centrally defines and manages hierarchy-wide security access settings for all sites and site settings. Security roles are assigned to administrative users and group permissions to different Configuration Manager object types, such as the permissions to create or change client settings. Security scopes group specific instances of objects that an administrative user is responsible to manage, such as an application that installs Microsoft Office. The combination of security roles, security scopes, and collections define what objects an administrative user can view and manage. Configuration Manager installs some default security roles for typical management tasks. However, you can create your own security roles to support your specific business requirements.  

 For more information, see [Configure role-based administration for System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md)  

## Securing client endpoints  
 Client communication to site system roles is secured by using either self-signed certificates, or by using public key infrastructure (PKI) certificates. Computer clients that Configuration Manager detects to be on the Internet and mobile device clients must use PKI certificates so that the client endpoints can be secured by using HTTPS. The site system roles that clients connect to can be configured for either HTTPS or HTTP client communication. Client computers always communicate by using the most secure method that is available and only fall back to using the less secure communication method of HTTP on the intranet if you have site systems roles that allow HTTP communication.  

 For more information, see [Cryptographic controls technical reference for System Center Configuration Manager](../../protect/deploy-use/cryptographic-controls-technical-reference.md)  

## Configuration Manager accounts and groups  
 Configuration Manager uses the **Local System** account for most site operations. However, some management tasks might require creating and maintaining additional accounts. Several default groups and SQL Server roles are created during Setup. However, you might have to manually add computer or user accounts to these default groups and roles.  

 For more information, see [Accounts used in System Center Configuration Manager](../../core/plan-design/hierarchy/accounts.md).  

## Privacy  
 Although enterprise management products offer many advantages because they can effectively manage lots of clients, you must also be aware of how this software might affect the privacy of users in your organization. System Center Configuration Manager includes many tools to collect data and monitor devices, some of which could raise privacy concerns.  

 For example, when you install the Configuration Manager client, many management settings are enabled by default. This results in the client software sending information to the Configuration Manager site. Client information is stored in the Configuration Manager database and the information is not sent to Microsoft. Before you implement System Center Configuration Manager, consider your privacy requirements.  
