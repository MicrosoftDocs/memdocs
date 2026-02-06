---
title: Assign a role to an Intune administrator
description: Learn how to assign a built-in or custom role to a user in Microsoft Intune.
author: brenduns
ms.author: brenduns
ms.date: 09/23/2025
ms.topic: article
ms.collection:
- M365-identity-device-management
---

# Assign  Microsoft Intune roles for role-based access control

The information in this article can help you assign users Microsoft Intune [built-in](role-based-access-control.md#built-in-roles) or [custom](create-custom-role.md) role-based access control (RBAC) roles to users who administer your Intune subscription. RBAC roles are assigned to groups, and not individual users.

Before you assign roles to groups, ensure you have sufficient groups for the different Intune administrative tasks, and review the membership of those groups. Each member of a group that is assigned an RBAC role receives the permissions granted by that role. Permissions from multiple groups are cumulative for a user and there are no options to deny specific permissions. However, you can [use Scope Tags with RBAC](../fundamentals/scope-tags.md) to limit the scope of what different groups of individuals can view and manage.

> [!IMPORTANT]
> Microsoft advises against using accounts with Intune Administrator-level permissions for daily management when lesser-privileged roles suffice. However, Intune Administrator permissions are necessary during initial Intune setup for tasks such as:
>
> - Add users to Intune who serve as your Intune administrators. *(See [Add users](../fundamentals/users-add.md))*
> - Create groups of users that share similar administrative duties. *(See [Add groups](../fundamentals/groups-add.md))*
> - Assign RBAC roles to groups of users, providing each group with only the permissions required to carry out their daily tasks. *(This article)*
>
> After you complete these steps, switch to an account with only the permissions needed for ongoing administration to uphold the principle of least privilege.

## RBAC permissions required to assign roles

To manage RBAC roles and assignments in Intune, your account must have one of the following permission sets:

- The Intune built-in role of [**Intune Role Administrator**](../fundamentals/role-based-access-control.md#built-in-roles). *Least privileged built-in role*
- A custom role that includes the following permissions and actions:

  **Roles**:
  - Assign
  - Create
  - Delete
  - Read
  - Update

  **Organization**:
  - Read

> [!NOTE]
> **Enhanced Security**: [!INCLUDE [multi-admin-approval-rbac](../includes/multi-admin-approval-rbac.md)]

## Deploy Intune role assignments

Before you deploy Intune roles, be familiar with [About Intune role assignments](../fundamentals/role-based-access-control.md#about-intune-role-assignments) which provides details about several aspects of Intune role assignements.

1. Sign in to the Microsoft Intune admin center and go to **Tenant administration** > **Roles** > **All roles**.

2. On the **Intune roles - All roles** page, you can find all Intune roles that are available to assign in your Tenant. Each role has a *Type* that identifies it as either a Built-in Role provided by Intune or a Custom Intune role created by your organization.

   Select the role you want to assign and then select **Assignments** > **+ Assign**.

3. On the **Basics** page, enter an **Name** and optional **Description**, and then select  **Next**.

4. On the **Admin Groups** page, select **Add groups** and then choose a group that contains the users you want to assign the roles permissions to.

   > [!TIP]
   > When you assign a role to a group, every member of that group receives the permissions granted by that role. Only assign roles to groups for which you know the membership, and which don't include users that shouldn't receive the administrative privileges provided by the role.

   > [!NOTE]
   > If your tenant allows [unlicensed admins](../fundamentals/unlicensed-admins.md), Intune role assignments only apply to direct members of the assigned security group. Members of nested groups do not receive these assignments by default. However, if a user in a nested group has an Intune license, that user will receive the Intune role.

   Select **Next**.

5. On the **Scope (Groups)** page, add groups that contain only the users or devices that the members of the Admin Groups you selected in the previous step should be allowed to manage. Then, select **Next**.

   > [!NOTE]
   > The *All users* and *All devices* groups are [Intune virtual groups](groups-add.md#the-intune-all-users-and-all-devices-groups), not Microsoft Entra security groups. Therefore, you can't use them as parents for Microsoft Entra security groups in Scope (Groups) assignments. To assign  *All users* and *All devices* and specific Microsoft Entra security groups, add them separately. Otherwise, admins won't have access to specific Microsoft Entra user groups even if the role's Scope (Groups) is set to *All Users*.
   >
   > Nesting is supported for Microsoft Entra security groups.

6. On the **Scope (Tags)** page, choose tags where this role assignment is applied. Select **Next**.

   > [!NOTE]
   > When you define scope groups and then assign a scope tag, admins can only target groups that are listed in the Scope (Groups) of the role assignment.

7. On the **Review + Create** page, when you're done, select **Create**.

   The new assignment is displayed in the list of assignments.

## Related content

- [Create a custom role](../fundamentals/create-custom-role.md)
- [Set the MDM authority](../fundamentals/mdm-authority-set.md)

