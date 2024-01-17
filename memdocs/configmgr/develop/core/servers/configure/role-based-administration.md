---
title: Role-Based Administration
titleSuffix: Configuration Manager
description: This section provides topics about programmatically managing role-based administration in Configuration Manager.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: conceptual
ms.assetid: 20486f6b-b4f2-4e4a-9dbb-72fb90067ec0
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Configuration Manager Role-Based Administration
This section provides topics about programmatically managing role-based administration in Configuration Manager.  

> [!NOTE]
> For more information, see [Fundamentals of role-based administration](../../../../core/understand/fundamentals-of-role-based-administration.md).

## About role-based administration  
 Role-based administration security rights are applied to a domain user or a security group. In Configuration Manager security rights are replicated to all sites in the hierarchy. You can use any single site to change the security rights of a user or security group and it will be automatically replicated to all other sites in that same hierarchy.  

 Security consists of two basic concepts: security roles and security scopes.  

### Security Roles  
 A security role in Configuration Manager grants permissions to the types of objects a user can interact with, and the actions they can perform with those objects. Configuration Manager provides multiple built-in security roles.  

### Security Scopes  
 A security scope in Configuration Manager establishes security restrictions between the user and object instances. The permissions the user will have with that object instance are determined by their assigned security roles.  

### Administrative Users and Security Groups  
 Domain users and security groups can be granted access to Configuration Manager. The permissions set on an administrator consist of a combination of a security role and scope. A scope is applied to a role that the administrator has. It can never be applied independently of the role.  

## See also

[Configuration Manager SDK](../../misc/system-center-configuration-manager-sdk.md)
