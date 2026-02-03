---
title: Role-based access control (RBAC) with Microsoft Intune
description: Learn how RBAC lets you control who can perform actions and make changes in Microsoft Intune.
author: brenduns
ms.author: brenduns
ms.date: 08/20/2025
ms.topic: article
ms.reviewer: davidra
ms.collection:
- M365-identity-device-management
- highpri
- essentials-security
---

# Role-based access control (RBAC) with Microsoft Intune

Securing access to your organization is an essential security step. This article introduces foundational details for using Microsoft Intune role-based access controls (RBAC), which are an extension of Microsoft Entra ID RBAC controls. Subsequent articles can help you deploy Intune RBAC in your organization.

With Intune RBAC, you can grant granular permissions to your admins to control who has access to your organization's resources, and what they can do with those resources. When you assign Intune RBAC roles and follow the principles of least privilege access, your admins can perform their assigned tasks on only those users and devices that they should be empowered to manage.

## RBAC Roles

Each Intune RBAC role specifies a set of permissions that are available to users assigned to that role. Permissions are composed of one or more management categories like *Device configuration* or *Audit data*, and sets of actions that can be taken like *Read*, *Write*, *Update*, and *Delete*. Together, they define the scope of administrative access and permissions within Intune.

Intune includes both built-in and custom roles. Built-in roles are the same in all tenants and are provided to address common administrative scenarios, while [custom roles you create](create-custom-role.md) allow for specific permissions as needed by an admin. In addition, several Microsoft Entra roles include permissions within Intune.

To view a role in the **Intune admin center**, go to **Tenant administration** > **Roles** > **All roles** > and select a role. You can then manage that role through the following pages:

- **Properties**: The name, description, permissions, and scope tags for the role. You can also view the name, description, and permissions of built-in roles in this documentation at [Built-in role permissions](../fundamentals/role-based-access-control-reference.md).
- **Assignments**: Select an [assignment for a role](assign-role.md) to view details about it including the groups and scopes that the assignment includes. A role can have multiple assignments, and a user can receive multiple assignments.

> [!NOTE]
> In June 2021, Intune began supporting [unlicensed admins](../fundamentals/unlicensed-admins.md). User accounts created after this change can administer Intune without an assigned license. Accounts created before this change and administrator accounts in a nested security group assigned to a role still require a license to manage Intune.

### Built-in roles

An Intune admin with sufficient permissions can assign any of the Intune roles to groups of users. Built-in roles grant specific permissions necessary for performing administrative tasks that align with the role's purpose. Intune doesn't support edits to description, type, or permissions of a built-in role.

- **Application Manager**: Manages mobile and managed applications, can read device information and can view device configuration profiles.
- **Endpoint Privilege Manager**: Manages Endpoint Privilege Management policies in the Intune console.
- **Endpoint Privilege Reader**: Endpoint Privilege Readers can view Endpoint Privilege Management policies in the Intune console.
- **Endpoint Security Manager**: Manages security and compliance features, such as security baselines, device compliance, Conditional Access, and Microsoft Defender for Endpoint.
- **Help Desk Operator**: Performs remote tasks on users and devices, and can assign applications or policies to users or devices.
- **Intune Role Administrator**: Manages custom Intune roles and adds assignments for built-in Intune roles. It's the only Intune role that can assign permissions to Administrators.
- **Policy and Profile Manager**: Manages compliance policy, configuration profiles, Apple enrollment, corporate device identifiers, and security baselines.
- **Read Only Operator**: Views user, device, enrollment, configuration, and application information. Can't make changes to Intune.
- **School Administrator**: School Administrators manage apps, settings, and devices for their groups in [Intune for Education](../industry/education/introduction-intune-education.md). They can take remote actions on devices, including remotely locking them, restarting them, and retiring them from management.

When your tenant includes a subscription to Windows 365 to support Cloud PCs, you also see the following Cloud PC roles in the Intune admin center. These roles aren't available by default and include permissions within Intune for tasks related to Cloud PCs. For more information about these roles, see [Cloud PC built-in roles](/windows-365/enterprise/role-based-access#cloud-pc-built-in-roles) in the Windows 365 documentation.

- **Cloud PC Administrator**: A Cloud PC Administrator has *Read* and *Write* access to all Cloud PC features located within the Cloud PC area.
- **Cloud PC Reader**: A Cloud PC Reader has *Read* access to all Cloud PC features located within the Cloud PC area.

### Custom roles

You can create your own custom Intune roles to grant admins only the specific permissions needed for their tasks. These custom roles can include any Intune RBAC permission, allowing for refined admin access and support for the principle of least-privileged access within the organization.

See [Create a custom role](create-custom-role.md).

### Microsoft Entra roles with Intune access

Intune RBAC permissions are a subset of Microsoft Entra RBAC permissions. As a subset, there are some Microsoft Entra roles that include permissions within Intune. Most Entra ID roles that have access to Intune are considered [privileged roles](/entra/identity/role-based-access-control/privileged-roles-permissions). The use and assignment of privileged roles should be limited and not used for daily administrative tasks within Intune.

Microsoft recommends following the principle of least-permissions by only assigning the minimum required permissions for an administrator to perform their duties. To support this principle, use Intune's built-in RBAC roles for daily Intune administrative tasks and avoid using Microsoft Entra roles that have access to Intune.

The following table identifies the Microsoft Entra roles that have access to Intune, and the Intune permissions they include.

| Microsoft Entra role | All Intune data | Intune audit data |
| --- | :---: | :---: |
| Global Administrator [![Privileged label icon](../media/privileged-lable.png)](/entra/identity/role-based-access-control/privileged-roles-permissions?tabs=admin-center) | Read/write | Read/write |
| Intune Service Administrator [![Privileged label icon](../media/privileged-lable.png)](/entra/identity/role-based-access-control/privileged-roles-permissions?tabs=admin-center) | Read/write | Read/write |
| Conditional Access Administrator [![Privileged label icon](../media/privileged-lable.png)](/entra/identity/role-based-access-control/privileged-roles-permissions?tabs=admin-center) | None | None |
| Security Administrator [![Privileged label icon](../media/privileged-lable.png)](/entra/identity/role-based-access-control/privileged-roles-permissions?tabs=admin-center) | Read only (full administrative permissions for Endpoint Security node) | Read only |
| Security Operator [![Privileged label icon](../media/privileged-lable.png)](/entra/identity/role-based-access-control/privileged-roles-permissions?tabs=admin-center) | Read only | Read only |
| Security Reader [![Privileged label icon](../media/privileged-lable.png)](/entra/identity/role-based-access-control/privileged-roles-permissions?tabs=admin-center) | Read only | Read only |
| Compliance Administrator | None | Read only |
| Compliance Data Administrator | None | Read only |
| Global Reader [![Privileged label icon](../media/privileged-lable.png)](/entra/identity/role-based-access-control/privileged-roles-permissions?tabs=admin-center) | Read Only | Read Only |
| Helpdesk administrator [![Privileged label icon](../media/privileged-lable.png)](/entra/identity/role-based-access-control/privileged-roles-permissions?tabs=admin-center) (This role is equivalent to the Intune *Help Desk Operator* role) | Read Only | Read Only |
| Reports Reader | None | Read Only|

In addition to the Microsoft Entra roles with permission within Intune, the following three areas of Intune are direct extensions of Microsoft Entra: **Users**, **Groups**, and **Conditional Access**. Instances of these objects and configurations made from within Intune exist in Microsoft Entra. As Microsoft Entra objects, they can be managed by Microsoft Entra administrators with sufficient permissions granted by an Microsoft Entra role. Similarly, Intune admins with sufficient permissions for Intune can view and manage these object types that are created in Microsoft Entra.

## Global Administrator and Intune Administrator roles

The **Global Administrator** role is a built-in role in Microsoft Entra, and has full access to Microsoft Intune. Global admins have access to administrative features in Microsoft Entra ID, and services that use Microsoft Entra identities, including Microsoft Intune.

**To reduce risk**:

- Don't use the Global Administrator role in Intune. Microsoft doesn't recommend using the Global Administrator role to administer or manage Intune.

  There are some features in Intune that require the Global Administrator role, like some mobile threat defense (MTD) connectors. In these cases, use the Global Administrator role only when necessary, and then remove it when the task is complete.

- Use the [Intune built-in roles](#rbac-roles) or create [custom roles](create-custom-role.md) to administer and manage Intune.
- Assign the least privileged Intune role necessary for the admin to do their tasks.

To learn more about the Microsoft Entra Global Administrator role, see [Microsoft Entra built-in roles - Global Administrator](/entra/identity/role-based-access-control/permissions-reference#global-administrator).

The **Intune Administrator** role is a built-in role in Microsoft Entra, and is also known as the **Intune Service Administrator** role. It has a limited scope of permissions to administer and manage Intune, and manage related features, like user and group management. This role is suitable for admins who only need to administer Intune.

**To reduce risk**:

- Assign the Intune Administrator role only as needed. If there's a [built-in Intune role](#rbac-roles) that meets the needs of the admin, then assign that role instead of the Intune Administrator role. Always assign the least privileged Intune role necessary for the admin to do their tasks.
- Create [custom roles](create-custom-role.md) to further limit the scope of permissions for your admins.

**Enhanced Security Controls**:

[!INCLUDE [multi-admin-approval-rbac](../includes/multi-admin-approval-rbac.md)]

To learn more about the Microsoft Entra Intune Administrator role, see [Microsoft Entra built-in roles - Intune Administrator](/entra/identity/role-based-access-control/permissions-reference#intune-administrator).

## Privileged Identity Management for Intune

When you use Entra ID Privileged Identity Management (PIM), you can manage when a user can use the privileges provided by an Intune RBAC role or the Intune Administrator role from Entra ID.

Intune supports two methods of role elevation. There are performance and least privilege differences between the two methods.

- **Method 1**: Create a just-in-time (JIT) policy with [Microsoft Entra Privileged Identity Management (PIM)](/entra/id-governance/privileged-identity-management/pim-configure) for the Microsoft Entra built-in **Intune Administrator** role and assign it an administrator account.

- **Method 2**: Utilize [Privileged Identity Management (PIM) for Groups](/entra/id-governance/privileged-identity-management/concept-pim-for-groups) with an Intune RBAC role assignment. For more information about using PIM for Groups with Intune RBAC roles, see: [Configuring Microsoft Intune just-in-time admin access with Microsoft Entra PIM for Groups | Microsoft Community Hub](https://techcommunity.microsoft.com/blog/intunecustomersuccess/configuring-microsoft-intune-just-in-time-admin-access-with-azure-ad-pim-for-gro/3843972)

When you use PIM elevation for the Intune Administrator role from Entra ID, elevation typically happens within 10 seconds. PIM Groups-based elevation for Intune's built-in or custom roles typically take up to 15 minutes to apply.

## About Intune role assignments

Both Intune custom and built-in roles are assigned to groups of users. An assigned role applies to each user in the group and defines:

- which users are assigned to the role
- what resources they can see
- what resources they can change.

Each group that is assigned an Intune role should include only users authorized to perform the administrative tasks for that role.

- If a least privileged built-in role grants excessive privileges or permissions, consider using a custom role to limit the scope of administrative access.
- When planning role assignments, consider the results of a user with [multiple role assignments](#multiple-role-assignments).

For a user to be assigned an Intune role and have access to administer Intune, they don't require an Intune license *if* their account was created in Entra after June 2021. Accounts created before June 2021 do require being assigned a license to use Intune.

To view an existing role assignment, choose **Intune** > **Tenant administration** > **Roles** > **All roles** > choose a role > **Assignments** > choose an assignment. On the assignments **Properties** page, you can edit:

- **Basics**: The assignments name and description.

- **Members**: Members are the groups that are configured on the *Admin Groups* page when creating a role assignment. All users in the listed Azure security groups have permission to manage the users and devices that are listed in *Scope (Groups)*.

- **Scope (Groups)**: Use Scope (Groups) to define the groups of users and devices that an admin with this role assignment can manage. Administrative users with this role assignment can use the permissions granted by the role to manage every user or device within the role assignments defined scope groups.

  > [!TIP]
  > When you configure a scope group, limit access by selecting only the security groups that include the user and devices that an admin with this role assignment should manage. To ensure admins with this role can't target all users or all devices, don't select *Add all users* or *Add all devices*.
  >
   > If you specify an exclude group for an assignment such as a policy or app assignment, it needs to either be nested in one of the RBAC assignment scope groups, or it needs to be separately listed as a scope group in the RBAC role assignment.

- [**Scope Tags**](scope-tags.md): Administrative users who are assigned this role assignment can see the resources that have the same scope tags.

> [!NOTE]
> Scope Tags are freeform text values that an administrator defines and then adds to a role assignment. The scope tag added on a role controls visibility of the role itself. The scope tag added in role assignment limits the visibility of Intune objects, like policies, apps, or devices to only administrators in that role assignment because the role assignment contains one or more matching scope tags.

### Multiple role assignments

If a user has multiple role assignments, permissions, and scope tags, those role assignments extend to different objects as follows:

- Permissions are incremental in the case where two or more roles grant permissions to the same object. A user with Read permissions from one role and Read/write from another role, for example, has an effective permission of Read/write (assuming the assignments for both roles target the same scope tags).
- Assign permissions and scope tags only apply to the objects (like policies or apps) in that role's assignment Scope (Groups). Assign permissions and scope tags don't apply to objects in other role assignments unless the other assignment specifically grants them.
- Other permissions (such as Create, Read, Update, Delete) and scope tags apply to all objects of the same type (like all policies or all apps) in any of the user's assignments.
- Permissions and scope tags for objects of different types (like policies or apps), don't apply to each other. A Read permission for a policy, for example, doesn't provide a Read permission to apps in the user's assignments.
- When there aren't any scope tags or some scope tags are assigned from different assignments, a user can only see devices that are part of some scope tags and can't see all devices.

## Monitor RBAC assignments
*This and the three subsections are in progress*

Within the Intune admin center, you can go to **Tenant admin** > **Roles** and expand **Monitor** to find several views that can help you identify the permissions different users have within your Intune tenant. For example, in a complex administrative environment, you can use the **Admin permissions** view to specify an account so you can see its current scope of administrative privileges.

:::image type="content" source="./media/role-based-access-control/rbac-monitor-node.png" alt-text="A screen capture of the options for monitoring RBAC from within the Intune admin center.":::

### My permissions
When you select this node, you see a combined list of the current Intune RBAC categories and permissions that your account is granted. This combined list includes all the permissions from all role assignments, but not which role assignments provide them or by which group membership they're assigned.

### Roles by permission
With this view, you can see details about a specific Intune RBAC [permission](../fundamentals/create-custom-role.md#custom-role-permissions), and through which role assignments, and to which groups that combination is made available.

To get started, select an Intune permission and then a specific action from that permission. The admin center then displays a list of instances that lead to that permission being assigned that includes:

- **Role display name** – The name of the built-in or custom RBAC role that grants the permission.
- **Role assignment display name** – The name of the role assignment that assigns the role to groups of users.
- **Group name** – The name of the group that receives that role assignment.

### Admin permissions
Use the Admin permissions node to identify the specific permissions that an account is currently granted.

Start by specifying a **User** account. So long as the user has Intune permissions assigned to their account, Intune displays the complete list of those permissions identified by *Permission* and *Action*.

:::image type="content" source="./media/role-based-access-control/admin-permission-view.png" alt-text="A screen capture that shows an example of the Admin permissions view in the Intune admin center.":::
## Next steps

- [Assign a role to a user](assign-role.md)
- [Create a custom role](create-custom-role.md)
