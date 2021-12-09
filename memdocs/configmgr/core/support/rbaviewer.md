---
title: Role-based administration tool
titleSuffix: Configuration Manager
description: Use the role-based administration and auditing tool to model and audit security roles and scopes in Configuration Manager.
ms.date: 04/16/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# Role-based administration and auditing tool

*Applies to: Configuration Manager (current branch)*

The role-based administration and auditing tool is one of the [Configuration Manager tools](tools.md). Use this tool for the following tasks:

- Model security roles with specific permissions

- Audit the security scopes and security roles that other users have

## Requirements

- Run it on the same computer as the Configuration Manager site server

- You have the **Full Administrator**, **Read-only Analyst**, or **Security Administrator** role

- Assign your account to the **All** security scope and all collections

- (*Optional*) To analyze report folder security, you need SQL Server access

- (*Optional*) To analyze report drill-through, run this tool on the site system server with the reporting services point role

## Procedures

### Model permissions for a new role

Use the following procedure to model permissions for a new role that you want to create:

1. Run **RBAViewer.exe**.

1. Select the base security roles you want to build on, or start from an empty permission set. Select the necessary permissions.

1. Select **Analyze** to see the user interface this custom role will see.

    > [!NOTE]
    > To see whether there's an existing security role that meets your requirements, switch to the **Similarity** tab.

1. Select **Export** to save the role as an XML file. Then import it to the Configuration Manager console. For more information, see [Create custom security roles](../servers/deploy/configure/configure-role-based-administration.md#create-custom-security-roles).

### Audit existing security scopes

Use the following procedure to audit all existing administrative users, collections, and security scopes in Configuration Manager:

1. Run **RBAViewer.exe**.

1. Select the **Audit RBA** button in the toolbar.

    1. To view the collection-limited relationships in a tree view, switch to the **Collection Summary** tab.

    1. To view objects assigned to a security role, switch to the **Scope Summary** tab.

### Audit a specific user

Use the following procedure to audit the role-based administration configuration for a specific user:

1. Run **RBAViewer.exe**.

1. Select the **Run As** button in the toolbar.

1. Input the specific user name to check the permissions for that account.

1. The tool displays the security roles assigned to the user or the security group the user belongs to. It also displays the objects this user can see and the actions they can take in the console.

## See also

- [Fundamentals of role-based administration](../understand/fundamentals-of-role-based-administration.md)

- [Configure role-based administration](../servers/deploy/configure/configure-role-based-administration.md)
