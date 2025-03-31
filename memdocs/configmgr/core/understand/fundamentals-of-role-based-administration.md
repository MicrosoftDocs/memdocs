---
title: Role-based administration fundamentals
titleSuffix: Configuration Manager
description: Use role-based administration to control administrative access to Configuration Manager and objects that you manage.
ms.date: 04/15/2021
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: article
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Fundamentals of role-based administration for Configuration Manager

*Applies to: Configuration Manager (current branch)*

With Configuration Manager, you use role-based administration to secure the access that administrative users need to use Configuration Manager. You also secure access to the objects that you manage, like collections, deployments, and sites.

The role-based administration model centrally defines and manages hierarchy-wide security access. This model is for all sites and site settings by using the following items:

- _Security roles_ are assigned to administrative users to give them permission to Configuration Manager objects. For example, permission to create or change client settings.

- _Security scopes_ are used to group specific instances of objects that an administrative user is responsible to manage. For example, an application that installs the Configuration Manager console.

- _Collections_ are used to specify groups of users and devices that the administrative user can manage in Configuration Manager.

With the combination of roles, scopes, and collections, you segregate the administrative assignments that meet your organization's requirements. Used together, they define the _administrative scope_ of a user. This administrative scope controls the objects that an administrative user views in the Configuration Manager console, and it controls the permissions that a user has on those objects.

## Benefits

The following items are benefits of role-based administration in Configuration Manager:

- Sites aren't used as administrative boundaries. In other words, don't expand a standalone primary site to a hierarchy with a central administration site to separate administrative users.

- You create administrative users for a hierarchy and only need to assign security to them one time.

- All security assignments are replicated and available throughout the hierarchy. Role-based administration configurations replicate to each site in the hierarchy as global data, and then are applied to all administrative connections.

  > [!IMPORTANT]
  > Intersite replication delays can prevent a site from receiving changes for role-based administration. For more information about how to monitor intersite database replication, see [Data transfers between sites](../plan-design/hierarchy/data-transfers-between-sites.md).

- There are built-in security roles that are used to assign the typical administration tasks. Create your own custom security roles to support your specific business requirements.

- Administrative users see only the objects that they have permissions to manage.

- You can audit administrative security actions.

## Security roles

Use security roles to grant security permissions to administrative users. Security roles are groups of security permissions that you assign to administrative users so that they can do their administrative tasks. These security permissions define the actions that an administrative user can do and the permissions that are granted for particular object types. As a security best practice, assign the security roles that provide the least permissions that are required for the task.

Configuration Manager has several built-in security roles to support typical groupings of administrative tasks. You can create your own custom security roles to support your specific business requirements.

The following table summarizes all of the built-in roles:

| Name | Description |
| ---- | ----------- |
| **Application administrator** | Combines the permissions of the **Application deployment manager** and the **Application author** roles. Administrative users in this role can also manage queries, view site settings, manage collections, edit settings for user device affinity, and manage App-V virtual environments. |
| **Application author** | Can create, modify, and retire applications. Administrative users in this role can also manage applications, packages, and App-V virtual environments. |
| **Application deployment manager** | Can deploy applications. Administrative users in this role can view a list of applications. They can manage deployments for applications, alerts, and packages. They can view collections and their members, status messages, queries, conditional delivery rules, and App-V virtual environments. |
| **Asset manager** | Grants permissions to manage the Asset Intelligence synchronization point, Asset Intelligence reporting classes, software inventory, hardware inventory, and metering rules. |
| **Company resource access manager** | Grants permissions to create, manage, and deploy company resource access profiles. For example, Wi-Fi, VPN, Exchange ActiveSync email, and certificate profiles. |
| **Compliance settings manager** | Grants permissions to define and monitor compliance settings. Administrative users in this role can create, modify, and delete configuration items and baselines. They can also deploy configuration baselines to collections, start compliance evaluation, and start remediation for non-compliant computers. |
| **Endpoint protection manager** | Grants permissions to create, modify, and delete endpoint protection policies. They can deploy these policies to collections, create and modify alerts, and monitor endpoint protection status. |
| **Full administrator** | Grants all permissions in Configuration Manager. The administrative user who installs Configuration Manager is automatically granted this security role, all scopes, and all collections. |
| **Infrastructure administrator** | Grants permissions to create, delete, and modify the Configuration Manager server infrastructure and to run migration tasks. |
| **Operating system deployment manager** | Grants permissions to create OS images and deploy them to computers, manage OS upgrade packages and images, task sequences, drivers, boot images, and state migration settings. |
| **Operations administrator** | Grants permissions for all actions in Configuration Manager except for the permissions to manage security. This role can't manage administrative users, security roles, and security scopes. |
| **Read-only analyst** | Grants permissions to view all Configuration Manager objects. |
| **Remote tools operator** | Grants permissions to run and audit the remote administration tools that help users resolve computer issues. Administrative users in this role can run remote control, remote assistance, and remote desktop from the Configuration Manager console. |
| **Security administrator** | Grants permissions to add and remove administrative users and to associate administrative users with security roles, collections, and security scopes. Administrative users in this role can also create, modify, and delete security roles and their assigned security scopes and collections. |
| **Software update manager** | Grants permissions to define and deploy software updates. Administrative users in this role can manage software update groups, deployments, and deployment templates. |

> [!TIP]
> If you have permissions, you can view the list of all security roles in the Configuration Manager console. To view the roles, go to the **Administration** workspace, expand **Security**, and then select the **Security Roles** node.

You can't modify the built-in security roles, other than add administrative users. You can copy the role, make changes, and then save these changes as a new custom security role. You can also import security roles that you've exported from another hierarchy like a lab environment. For more information, see [Configure role-based administration](../../core/servers/deploy/configure/configure-role-based-administration.md#how-to-create-custom-security-roles).

Review the security roles and their permissions to determine whether you'll use the built-in security roles, or whether you have to create your own custom security roles.  

### Role permissions

Each security role has specific permissions for different object types. For example, the _application author_ role has the following permissions for _applications_:

- Approve
- Create
- Delete
- Modify
- Modify folder
- Move object
- Read
- Run report
- Set security scope

This role also has permissions for other objects.

:::image type="content" source="media/application-author-role-permissions.png" alt-text="Permissions tab for the application author built-in role":::

For more information on how to view the permissions for a role, or change the permissions for a custom role, see [Configure role-based administration](../../core/servers/deploy/configure/configure-role-based-administration.md#configure-security-roles).

### Plan for security roles

Use this process to plan for Configuration Manager security roles in your environment:

1. Identify the tasks that administrative users need to do in Configuration Manager. These tasks might relate to one or more groups of management tasks. For example, deploying operating systems and settings for compliance.

1. Map these administrative tasks to one or more of the built-in roles.

1. If some of the administrative users do the tasks of multiple roles, assign the users to the multiple roles. Don't create a custom role that combines the permissions.

1. If the tasks that you identified don't map to the built-in security roles, create and test custom roles.

For more information, see [Create custom security roles](../../core/servers/deploy/configure/configure-role-based-administration.md#create-custom-security-roles) and [Configure security roles](../../core/servers/deploy/configure/configure-role-based-administration.md#configure-security-roles).

## Collections

Collections specify the users and devices that an administrative user can view or manage. For example, to deploy an application to a device, the administrative user needs to be in a security role that grants access to a collection that contains the device.

For more information about collections, see [Introduction to collections](../../core/clients/manage/collections/introduction-to-collections.md).

Before you configure role-based administration, decide whether you have to create new collections for any of the following reasons:

- Functional organization. For example, separate collections of servers and workstations.
- Geographic alignment. For example, separate collections for North America and Europe.
- Security requirements and business processes. For example, separate collections for production and test computers.
- Organization alignment. For example, separate collections for each business unit.

For more information, see [Configure collections to manage security](../../core/servers/deploy/configure/configure-role-based-administration.md#configure-collections-to-manage-security).

## Security scopes

Use security scopes to provide administrative users with access to securable objects. A security scope is a named set of securable objects that are assigned to administrator users as a group. All securable objects are assigned to one or more security scopes. Configuration Manager has two built-in security scopes:

- **All**: Grants access to all scopes. You can't assign objects to this security scope.

- **Default**: This scope is used for all objects by default. When you install Configuration Manager, it assigns all objects to this security scope.

If you want to restrict the objects that administrative users can see and manage, create your own custom security scopes. Security scopes don't support a hierarchical structure and can't be nested. Security scopes can contain one or more object types, which include the following items:

- Alert subscriptions
- Applications and application groups
- App-V virtual environments
- Boot images
- Boundary groups
- Configuration items and baselines
- Custom client settings
- Distribution points and distribution point groups
- Driver packages
- Endpoint protection policies (all)
- Folders <!--3600867-->
- Global conditions
- Migration jobs
- OneDrive for Business profiles
- OS images
- OS upgrade packages
- Packages
- Queries
- Remote connection profiles
- Scripts
- Sites
- Software metering rules
- Software update groups
- Software updates packages
- Task sequences
- User data and profiles configuration items
- Windows Update client policies

There are also some objects that you can't include in security scopes because they're only secured by security roles. Administrative access to these objects can't be limited to a subset of the available objects. For example, you might have an administrative user who creates boundary groups that are used for a specific site. Because the boundary object doesn't support security scopes, you can't assign this user a security scope that provides access to only the boundaries that might be associated with that site. Because a boundary object can't be associated to a security scope, when you assign a security role that includes access to boundary objects to a user, that user can access every boundary in the hierarchy.

Objects that don't support security scopes include but aren't limited to the following items:

- Active Directory forests
- Administrative users
- Alerts
- Boundaries
- Computer associations
- Default client settings
- Deployment templates
- Device drivers
- Migration site-to-site mappings
- Security roles
- Security scopes
- Site addresses
- Site system roles
- Software updates
- Status messages
- User device affinities

Create security scopes when you have to limit access to separate instances of objects. For example:

- You have a group of administrative users who need to see production applications and not test applications. Create one security scope for production applications and another for test applications.

- One group of administrative users requires Read permission to specific software update groups. Another group of administrative users requires Modify and Delete permissions for other software update groups. Create different security scopes for these software update groups.

For more information, see [Configure security scopes for an object](../../core/servers/deploy/configure/configure-role-based-administration.md#configure-security-scopes-for-an-object).

## Next steps

[Configure role-based administration for Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md)
