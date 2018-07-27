---
title: Role-based Administration Tool
titleSuffix: Configuration Manager
description: Use the Role-based Administration and Auditing Tool to model and audit security roles and scopes in Configuration Manager.
ms.date: 07/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6372ff17-7f56-4d7b-a21b-87fb8bdd6d3a
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Role-based Administration and Auditing Tool

*Applies to: System Center Configuration Manager (Current Branch)*

The Role-based Administration and Auditing Tool is one of the [Configuration Manager tools](/sccm/core/support/tools). Use this tool for the following tasks:

- Model security roles with specific permissions  

- Audit the security scopes and security roles that other users have



## Requirements

- Run it on the same computer as the Configuration Manager console  

- You have the **Full Administrator**, **Read-only Analyst**, or **Security Administrator** role  

- Assign your account to the **All** security scope and all collections  

- (*Optional*) To analyze report folder security, you must have SQL access  

- (*Optional*) To analyze report drill-through, run this tool on the site system server with the reporting point role



## Procedures


### Model permissions for a new role

Use the following procedure to model permissions for a new role that you want to create: 

1. Run **RBAViewer.exe**.  

2. Select the base security roles you want to build on, or start from an empty permission set. Select the necessary permissions.  

3. Click **Analyze** to see the user interface this custom role will see.  

    > [!Note]  
    > To see whether there's an existing security role that meets your requirements, switch to the **Similarity** tab.  

4. Click **Export** to save the role as an XML file. Then import it to the Configuration Manager console. For more information, see [Create custom security roles](/sccm/core/servers/deploy/configure/configure-role-based-administration#BKMK_CreateSecRole).


### Audit existing security scopes

Use the following procedure to audit all existing administrative users, collections, and security scopes in Configuration Manager:

1. Run **RBAViewer.exe**.  

2. Select the **Audit RBA** button in the toolbar.  

    1. To view the collection-limited relationships in a tree view, switch to the **Collection Summary** tab.  

    2. To view objects assigned to a security role, switch to the **Scope Summary** tab.  


### Audit a specific user

Use the following procedure to audit the role-based administration configuration for a specific user:

1. Run **RBAViewer.exe**.  

2. Select the **Run As** button in the toolbar.  

3. Input the specific user name to check the permissions for that account.  

4. The tool displays the security roles assigned to the user or the security group the user belongs to. It also displays the objects this user can see and the actions they can take in the console.  



## See also

- [Fundamentals of role-based administration](/sccm/core/understand/fundamentals-of-role-based-administration)
- [Configure role-based administration](/sccm/core/servers/deploy/configure/configure-role-based-administration)