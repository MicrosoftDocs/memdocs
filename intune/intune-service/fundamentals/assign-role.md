---
# required metadata

title: Assign a role to an Intune user
description: Learn how to assign a built-in or custom role to a user in Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/20/2025
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- tier2
- M365-identity-device-management
---

# Assign a role to an Intune user

The information in this article can help you assign users Microsoft Intune [built-in](role-based-access-control.md#built-in-roles) or [custom](create-custom-role.md) role-based access control (RBAC) roles to users who will administer your Intune subscription. RBAC roles are assigned to groups, and not individual users.

Before you assign roles to groups, ensure you have sufficient groups for the different Intune administrative tasks, and review the membership of those groups. Each member of a group that is assigned an RBAC role receives the permissions granted by that role. Permissions from multiple groups are cumulative for a user and there are no options to deny specific permissions. However, you can [use Scope Tags with RBAC](../fundamentals/scope-tags.md) to limit the scope of what different groups of individuals can view and manage.

> [!IMPORTANT]  
> Microsoft advises against using accounts with Intune Administrator-level permissions for daily management when lesser-privileged roles suffice. However, Intune Administrator permissions are necessary during initial Intune setup for tasks such as:  
>
> - Add users to Intune who will be your Intune administrators. *(See [Add users](../fundamentals/users-add. ))*
> - Create groups of users who will share similar administrative duties. *(See [Add groups](../fundamentals/groups-add.md))*
> - Assign RBAC roles to groups of users, providing each group with only the permissions required to carry out their daily tasks. *(This article)*  
>
> After completing these steps, switch to accounts with only the permissions needed for ongoing administration to uphold the principle of least privilege.

## Required RBAC permissions

To manage RBAC roles and assignements in Intune, your account must be assigned one of the following permission sets:

- The Intune built-in role of [**Intune Role Administrator**](../protect/role-based-access-control.md#built-in-roles). *Least privileged built-in role*
- A custom role that includes the following categories and category permissions:

  **Roles**:  
  - Assign
  - Create
  - Delete
  - Read
  - Update

  **Organization**:  
  - Read

## Assign Intune RBAC roles to groups

1. Sign in to the Microsoft Intune admin center and go to **Tenant administration** > **Roles** > **All roles**.

2. On the **Intune roles - All roles** page, you can find all Intune roles that are available to assign in your Tenant. These are identified by the *Type* column as a Built-in Role provided by Intune or a Custom Intune role for roles created by your organization. 

   Select the role you want to assign and then select **Assignments** > **+ Assign**.

3. On the **Basics** page, enter an **Name** and optional **Description**, and then select  **Next**.

4. On the **Admin Groups** page, select **Add groups** and then choose a group that contains the users you want to give the permissions to.

   > [!TIP]  
   > When you assign a role to a group, every member of that group receives the permissions granted by that role. Only assign roles to groups for which you know the membership, and which do not contain users that should not receive the administrative privileges provided by the role.

   Select **Next**.

5. On the **Scope (Groups)** page, add groups that contain only the users or devices that the members of the Admnin Groups you selected in the previous step should be allowed to manage. Select **Next**.

   > [!NOTE]  
   > The *All users* and *All devices* groups are [Intune virtual groups](groups-add.md#intune-all-users-and-all-devices-groups), not Microsoft Entra security groups. Therefore, you cannot use them as parents for Microsoft Entra security groups in Scope (Groups) assignments. To assign  *All users* and *All devices* as well as specific Microsoft Entra security groups, add them separately. Otherwise, admins won't have access to specific Microsoft Entra user groups even if the role’s Scope (Groups) is set to *All Users*.
   >
   > Nesting is supported for Microsoft Entra security groups.

6. On the **Scope (Tags)** page, choose tags where this role assignment is applied. Select **Next**.

7. On the **Review + Create** page, when you're done, select **Create**. The new assignment is displayed in the list of assignments.

   > [!NOTE]  
   > When you create scope groups and assign a scope tag, admins can only target groups that are listed in the Scope (Groups) of the role assignment.

## Next steps

- [Learn more about role-based access control in Intune](role-based-access-control.md)
- [Create a custom role](create-custom-role.md)
