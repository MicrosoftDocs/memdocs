---
title: Fundamentals of security
titleSuffix: Configuration Manager
description: Learn about the layers of security in Configuration Manager.
ms.date: 04/15/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Fundamentals of security for Configuration Manager

*Applies to: Configuration Manager (current branch)*

This article summarizes the following fundamental security components of any Configuration Manager environment:

- [Security layers](#security-layers)
- [Role-based administration](#role-based-administration)
- [Securing client endpoints](#securing-client-endpoints)
- [Configuration Manager accounts and groups](#configuration-manager-accounts-and-groups)
- [Privacy](#privacy)

## Security layers

Security for Configuration Manager consists of the following layers:

- [Windows OS and network security](#windows-os-and-network-security)
- [Network infrastructure: firewalls, intrusion detection, public key infrastructure (PKI)](#network-infrastructure)
- [Configuration Manager security controls](#configuration-manager-security-controls)
- [SMS Provider](#sms-provider)
- [Site database permissions](#site-database-permissions)

### Windows OS and network security

The first layer is provided by Windows security features for both the OS and the network. This layer includes the following components:

- File sharing to transfer files between Configuration Manager components.

- Access Control Lists (ACLs) to help secure files and registry keys.

- Internet Protocol Security (IPsec) to help secure communications.

- Group policy to set security policy.

- Distributed Component Object Model (DCOM) permissions for distributed applications, like the Configuration Manager console.

- Active Directory Domain Services to store security principals.

- Windows account security, including some groups that Configuration Manager creates during setup.

### Network infrastructure

Network security components, like firewalls and intrusion detection, help provide defense for the whole environment. Certificates issued by industry standard public key infrastructure (PKI) implementations help provide authentication, signing, and encryption.

### Configuration Manager security controls

By default, only local administrators have rights to the files and registry keys that the Configuration Manager console requires on computers where you install it.

### SMS Provider

The next layer of security is based on access to the SMS Provider. The SMS Provider is a Configuration Manager component that grants a user access to query the site database for information. The SMS Provider primarily exposes access through Windows Management Instrumentation (WMI), but also a REST API called the [administration service](../../develop/adminservice/overview.md).

By default, access to the provider is restricted to members of the local **SMS Admins** group. This group at first contains only the user who installed Configuration Manager. To grant other accounts permission to the Common Information Model (CIM) repository and the SMS Provider, add the other accounts to the SMS Admins group.

You can specify the minimum authentication level for administrators to access Configuration Manager sites. This feature enforces administrators to sign in to Windows with the required level. <!--1357013--> For more information, see [Plan for the SMS Provider](../plan-design/hierarchy/plan-for-the-sms-provider.md#authentication).

### Site database permissions

The final layer of security is based on permissions to objects in the site database. By default, the Local System account and the user account that you used to install Configuration Manager can administer all objects in the site database. Grant and restrict permissions to other administrative users in the Configuration Manager console by using [role-based administration](#role-based-administration).

## Role-based administration

Configuration Manager uses role-based administration to help secure objects like collections, deployments, and sites. This administration model centrally defines and manages hierarchy-wide security access settings for all sites and site settings.

An administrator assigns *security roles* to administrative users and group permissions. The permissions are connected to different Configuration Manager object types, for example, to create or change client settings.

*Security scopes* include specific instances of objects that an administrative user is responsible to manage. For example, an application that installs the Configuration Manager console.

The combination of security roles, security scopes, and collections define the objects that an administrative user can view and manage. Configuration Manager installs some default security roles for typical management tasks. Create your own security roles to support your specific business requirements.

For more information, see [Fundamentals of role-based administration](fundamentals-of-role-based-administration.md).

## Securing client endpoints

Configuration Manager secures client communication to site system roles by using either self-signed or PKI certificates, or Azure Active Directory (Azure AD) tokens. Some scenarios require the use of PKI certificates. For example, [internet-based client management](../clients/manage/plan-internet-based-client-management.md), and for [mobile device clients](../../mdm/plan-design/plan-on-premises-mdm.md).

You can configure the site system roles to which clients connect for either HTTPS or HTTP client communication. Client computers always communicate by using the most secure method that's available. Client computers only fall back to using the less secure communication method if you have site systems roles that allow HTTP communication.

> [!IMPORTANT]
> Starting in Configuration Manager version 2103, sites that allow HTTP client communication are deprecated. Configure the site for HTTPS or Enhanced HTTP. For more information, see [Enable the site for HTTPS-only or enhanced HTTP](../servers/deploy/install/list-of-prerequisite-checks.md#enable-site-system-roles-for-https-or-enhanced-http).<!-- 9390933,9572265 -->

For more information, see [Plan for security](../plan-design/security/plan-for-security.md).

## Configuration Manager accounts and groups

Configuration Manager uses the Local System account for most site operations. Some site operations allow the use of a service account, instead of using the domain computer account of the site server. Some management tasks might require you to create and maintain other accounts. For example, to join the domain during an OS deployment task sequence.

Configuration Manager creates several default groups and SQL Server roles during setup. You might have to manually add computer or user accounts to the default groups and SQL Server roles.

For more information, see [Accounts used in Configuration Manager](../plan-design/hierarchy/accounts.md).

## Privacy

Before you implement Configuration Manager, consider your privacy requirements. Although enterprise management products offer many advantages because they can effectively manage lots of clients, this software might affect the privacy of users in your organization. Configuration Manager includes many tools to collect data and monitor devices. Some tools might raise privacy concerns in your organization.

For example, when you install the Configuration Manager client, it enables many management settings by default. This configuration causes the client software to send information to the Configuration Manager site. The site stores client information in the site database. The client information isn't directly sent to Microsoft. For more information, see [Diagnostics and usage data](../plan-design/diagnostics/diagnostics-and-usage-data.md).

## Next steps

[Fundamentals of role-based administration](fundamentals-of-role-based-administration.md)

[Plan for security](../plan-design/security/plan-for-security.md)
