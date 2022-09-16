---
# required metadata

title: Role-based access control (RBAC) with Microsoft Intune
description: Learn how RBAC lets you control who can perform actions and make changes in Microsoft Intune.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 08/24/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: pjain
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: 
  - M365-identity-device-management
  - highpri
---

# Role-based access control (RBAC) with Microsoft Intune

Role-based access control (RBAC) helps you manage who has access to your organization's resources and what they can do with those resources.  By [assigning roles](assign-role.md) to your Intune users, you can limit what they can see and change. Each role has a set of permissions that determine what users with that role can access and change within your organization.

To create, edit, or assign roles, your account must have one of the following permissions in Azure AD:
- **Global Administrator**
- **Intune Service Administrator** (also known as **Intune Administrator**)

## Roles
A role defines the set of permissions granted to users assigned to that role.
You can use both the built-in and custom roles. Built-in roles cover some common Intune scenarios. You can [create your own custom roles](create-custom-role.md) with the exact set of permissions you need. Several Azure Active Directory roles have permissions to Intune.
To see a role, choose **Endpoint Manager** > **Tenant administration** > **Roles** > **All roles** > choose a role. You can manage the role on the following pages:

- **Properties**: The name, description, permissions, and scope tags for the role. 
- **Assignments**: A list of [role assignments](assign-role.md) defining which users have access to which users/devices. A role can have multiple assignments, and a user can be in multiple assignments.

> [!NOTE]
> To be able to administer Intune you must have an Intune license assigned. Alternatively, you can allow non-licensed users to administer Intune by setting [Allow access to unlicensed admins to Yes](unlicensed-admins.md).

### Built-in roles
You can assign built-in roles to groups without further configuration. You can't delete or edit the name, description, type, or permissions of a built-in role.

- **Application Manager**: Manages mobile and managed applications, can read device information and can view device configuration profiles.
- **Endpoint Security Manager**: Manages security and compliance features, such as security baselines, device compliance, conditional access, and Microsoft Defender for Endpoint.
- **Read Only Operator**: Views user, device, enrollment, configuration, and application information. Can't make changes to Intune.
- **School Administrator**: Manages Windows 10 devices in [Intune for Education](introduction-intune-education.md).
- **Policy and Profile Manager**: Manages compliance policy, configuration profiles, Apple enrollment, corporate device identifiers, and security baselines.
- **Help Desk Operator**: Performs remote tasks on users and devices, and can assign applications or policies to users or devices.
- **Intune Role Administrator**: Manages custom Intune roles and adds assignments for built-in Intune roles. It's the only Intune role that can assign permissions to Administrators.
- **Cloud PC Administrator**: A Cloud PC Administrator has read and write access to all Cloud PC features located within the Cloud PC blade.
- **Cloud PC Reader**: A Cloud PC Reader has read access to all Cloud PC features located within the Cloud PC blade.


### Custom roles
You can create your own roles with custom permissions. For more information about custom roles, see [Create a custom role](create-custom-role.md).

### Azure Active Directory roles with Intune access
| Azure Active Directory role | All Intune data | Intune audit data |
| --- | :---: | :---: |
| Global Administrator | Read/write | Read/write |
| Intune Service Administrator | Read/write | Read/write |
| Conditional Access Administrator | None | None |
| Security Administrator | Read only (full administrative permissions for Endpoint Security node) | Read only |
| Security Operator | Read only | Read only |
| Security Reader | Read only | Read only |
| Compliance Administrator | None | Read only |
| Compliance Data Administrator | None | Read only |
| Global Reader | Read Only | Read Only |
| Reports Reader | Read Only| None |

> [!TIP]
> Intune also shows three Azure AD extensions: **Users**, **Groups**, and **Conditional Access**, which are controlled using Azure AD RBAC. Additionally, the **User Account Administrator** only performs AAD user/group activities and does not have full permissions to perform all activities in Intune. For more information, see [RBAC with Azure AD](/azure/active-directory/active-directory-assign-admin-roles).

## Role assignments
A role assignment defines:

- which users are assigned to the role
- what resources they can see
- what resources they can change.

You can assign both custom and built-in roles to your users. To be assigned an Intune role, the user must have an Intune license.
To see a role assignment, choose **Intune** > **Tenant administration** > **Roles** > **All roles** > choose a role > **Assignments** > choose an assignment. On the **Properties** page you can edit:

- **Basics**: The assignments name and description.
- **Members**: All users in the listed Azure security groups have permission to manage the users/devices that are listed in Scope (Groups).
- **Scope (Groups)**: Scope Groups are Azure AD security groups of users or devices or both for which administrators in that role assignment are limited to performing operations on. For example deployment of a policy or application to a user or remotely locking a device. All users and devices in these Azure AD security groups can be managed by the users in Members.
- **[Scope (Tags)](scope-tags.md)**: Users in Members can see the resources that have the same scope tags.

> [!NOTE]
> Scope Tags are freeform text values that an administrator defines and then adds to a Role Assignment. The scope tag added on a role controls visibility of the role itself, while the scope tag added in role assignment limits the visibility of Intune objects (such as policies and apps) or devices to only administrators in that role assignment because the role assignment contains one or more matching scope tags.

### Multiple role assignments
If a user has multiple role assignments, permissions, and scope tags, those role assignments extend to different objects as follows:

- Assign permissions and scope tags only apply to the objects (like policies or apps) in that role's assignment Scope (Groups). Assign permissions and scope tags don't apply to objects in other role assignments unless the other assignment specifically grants them.
- Other permissions (such as Create, Read, Update, Delete) and scope tags apply to all objects of the same type (like all policies or all apps) in any of the user's assignments.
- Permissions and scope tags for objects of different types (like policies or apps), don't apply to each other. A Read permission for a policy, for example, doesn't provide a Read permission to apps in the user's assignments.

## Next steps
- [Assign a role to a user](assign-role.md)
- [Create a custom role](create-custom-role.md)
