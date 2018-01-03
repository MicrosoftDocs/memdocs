---
title: "Fundamentals of security"
titleSuffix: "Configuration Manager"
description: "Learn about the layers of security for System Center Configuration Manager."
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 035b7f73-8b78-4ed1-835e-a31f9a5c4a02
caps.latest.revision: 5
author: aczechowski
ms.author: aaroncz
manager: angrobe

---
# Fundamentals of security for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Security for System Center Configuration Manager consists of several layers. The first layer is provided by Windows security features for both the operating system and the network and includes:  

-   File sharing to transfer files between Configuration Manager components.  

-   Access Control Lists (ACLs) to help secure files and registry keys.  

-   Internet Protocol Security (IPsec) to help secure communications.  

-   Group Policy to set security policy.  

-   Distributed Component Object Model (DCOM) permissions for distributed applications, like the Configuration Manager console.  

-   Active Directory Domain Services to store security principals.  

-   Windows account security, including some groups that are created during Configuration Manager setup.  

Then, additional security components, like firewalls and intrusion detection, help provide defense for the whole environment. Certificates issued by industry standard public key infrastructure (PKI) implementations help provide authentication, signing, and encryption.  

In addition to security provided by the Windows server and network infrastructure, Configuration Manager controls access to the Configuration Manager console and its resources in several ways. By default, only local administrators have rights to the files and registry keys that are required to run the Configuration Manager console on computers where it is installed.  

The next layer of security is based on access through Windows Management Instrumentation (WMI), specifically the SMS Provider. The SMS Provider is a Configuration Manager component that grants a user access to query the site database for information. By default, access to the provider is restricted to members of the local SMS Admins group. This group at first contains only the user who installed Configuration Manager. To grant other accounts permission to the Common Information Model (CIM) repository and the SMS Provider, add the other accounts to the SMS Admins group.  

The final layer of security is based on permissions to objects in the site database. By default, the Local System account and the user account that you used to install Configuration Manager can administer all objects in the site database. You can grant and restrict permissions to additional administrative users in the Configuration Manager console by using role-based administration.  



## Role-based administration  
 Configuration Manager uses role-based administration to help secure objects like collections, deployments, and sites. This administration model centrally defines and manages hierarchy-wide security access settings for all sites and site settings. Security roles are assigned to administrative users and group permissions. The permissions are connected to different Configuration Manager object types, like the permissions that are used to create or change client settings. Security scopes the group specific instances of objects that an administrative user is responsible to manage, like an application that installs Microsoft Office. The combination of security roles, security scopes, and collections define the objects that an administrative user can view and manage. Configuration Manager installs some default security roles for typical management tasks. But, you can create your own security roles to support your specific business requirements.  

 For more information, see [Configure role-based administration for System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).  

## Securing client endpoints  
 Client communication to site system roles is secured by using either self-signed certificates, or by using PKI certificates. You'll need to use a PKI certificate for computer clients that Configuration Manager detects to be on the Internet, and for mobile device clients. The PKI certificate uses HTTPS to secure the client endpoints. The site system roles that clients connect to can be configured for either HTTPS or HTTP client communication. Client computers always communicate by using the most secure method that is available. Client computers only fall back to using the less secure communication method of HTTP on the intranet if you have site systems roles that allow HTTP communication.  

 For more information, see [Cryptographic controls technical reference for System Center Configuration Manager](../../protect/deploy-use/cryptographic-controls-technical-reference.md).  

## Configuration Manager accounts and groups  
 Configuration Manager uses the Local System account for most site operations. Some management tasks might require you to create and maintain additional accounts. Several default groups and SQL Server roles are created during setup. You might have to manually add computer or user accounts to the default groups and SQL Server roles.  

 For more information, see [Accounts used in System Center Configuration Manager](../../core/plan-design/hierarchy/accounts.md).  

## Privacy  
 Although enterprise management products offer many advantages because they can effectively manage lots of clients, you must also be aware of how this software might affect the privacy of users in your organization. System Center Configuration Manager includes many tools to collect data and monitor devices. Some tools might raise privacy concerns.  

 For example, when you install the Configuration Manager client, many management settings are enabled by default. This causes the client software to send information to the Configuration Manager site. Client information is stored in the Configuration Manager database, and the information is not sent to Microsoft. Before you implement System Center Configuration Manager, consider your privacy requirements.  
