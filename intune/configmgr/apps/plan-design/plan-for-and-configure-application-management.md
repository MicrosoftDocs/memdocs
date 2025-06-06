---
title: Plan for application management
titleSuffix: Configuration Manager
description: Implement and configure the necessary dependencies for deploying applications in Configuration Manager.
ms.date: 08/02/2021
ms.subservice: app-mgt
ms.service: configuration-manager
ms.topic: how-to
author: baladelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart
---

# Plan for and configure application management in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Use the information in this article to help you implement the necessary dependencies to deploy applications in Configuration Manager.

## Dependencies external to Configuration Manager

### Internet Information Services (IIS)

IIS is required on the servers that run the following site system roles:

- Management point
- Distribution point

For more information, see [Site and site system prerequisites](../../core/plan-design/configs/site-and-site-system-prerequisites.md).

### Certificates on code-signed applications for mobile devices

When you code-sign applications to deploy them to mobile devices, don't use a certificate that was generated by using a Version 3 template (**Windows Server 2008, Enterprise Edition**). This certificate template creates a certificate that's incompatible with Configuration Manager applications for mobile devices.

If you use Active Directory Certificate Services to code-sign applications for mobile device applications, don't use a Version 3 certificate template.

### Audit sign-in events for user device affinity

If you want to automatically create user device affinities, configure clients to audit sign-in events.

To determine automatic user device affinities, the Configuration Manager client reads sign-in events of type **Success** from the Windows security event log. Enable these events with the following two audit policies:

- **Audit account logon events**
- **Audit logon events**

To automatically create relationships between users and devices, make sure that these two settings are enabled on client computers. You can use Windows Group Policy to configure these settings.

For more information on user device affinity, see [Link users and devices with user device affinity](../deploy-use/link-users-and-devices-with-user-device-affinity.md).

## Configuration Manager dependencies

### Management point

Clients contact a management point to download client policy and to locate content. Software Center uses the same management point for user-available application deployments.

### Distribution point

Before you can deploy applications to clients, you need at least one distribution point in the hierarchy. By default, the site server has a distribution point site role enabled during a standard installation. The number and location of distribution points vary according to the specific requirements of your environment.

For more information about how to install distribution points and manage content, see [Manage content and content infrastructure](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).

### Reporting services point

To use the reports in Configuration Manager for application management, first install and configure a reporting services point.

For more information, see [Introduction to reporting](../../core/servers/manage/introduction-to-reporting.md).

### Client settings

Many client settings control how the client installs applications and the user experience on the device. These client settings include the following groups:

- Computer agent
- Computer restart
- Software Center
- Software deployment
- User and device affinity

For more information, see the following articles:

- [About client settings](../../core/clients/deploy/about-client-settings.md)
- [How to configure client settings](../../core/clients/deploy/configure-client-settings.md)

### Security permissions for application management

- The **Application Author** security role includes the required permissions to create, change, and retire applications.

- The **Application Deployment Manager** security role includes required permissions to deploy applications.

- The **Application Administrator** security role has all the permissions from both the **Application Author** and the **Application Deployment Manager** security roles.

For more information, see [Configure role-based administration](../../core/servers/deploy/configure/configure-role-based-administration.md).

### App-V 4.6 SP1 or later client to run virtual applications

To create virtual applications in Configuration Manager, install App-V 4.6 SP1 or later on devices.

App-V is included with all supported versions of Windows 10 Enterprise edition. For more information, see [Getting started with App-V for Windows 10](/windows/application-management/app-v/appv-getting-started).

## Remove the application catalog

<!-- SCCMDocs-pr issue 3051 -->

Support ended for the application catalog roles with version 1910. Software Center can deliver all app deployments without the application catalog. For more information, see [Removed and deprecated features](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).

Starting in version 2107, you can't update the site if it has either of the application catalog site system roles. Remove these roles before you update to version 2107.<!-- 10158844 -->

If your site still has an application catalog, use the following process to remove it:

1. Update all Configuration Manager clients to the latest supported version.

1. Set branding for Software Center, instead of in the properties of the application catalog web site role. For more information, see [Software Center client settings](../../core/clients/deploy/about-client-settings.md#software-center).

1. Review the default and any custom client settings. In the **Computer Agent** group, make sure the **Default Application Catalog website point** is `(none)`.

1. Remove the **application catalog website** and **application catalog web service** site system roles from all primary sites. For more information, see [Uninstall a site system role](../../core/servers/deploy/install/uninstall-sites-and-hierarchies.md#bkmk_role).

After you remove the application catalog roles, Software Center starts using the management point for user-targeted, available deployments. To verify this behavior on a specific client, review the `SCClient_<username>.log`, and look for an entry similar to the following line:

`Using endpoint Url: https://mp.contoso.com/CMUserService_WindowsAuth, Windows authentication`

> [!NOTE]
> If you have any tools or automation that used the ApplicationViewService.asmx SOAP endpoint on the application catalog website point, you need to change it. Update the URL in your tool to use the management point user service endpoint. For example, `https://mp.contoso.com/CMUserService_WindowsAuth`<!-- 10158844 -->

## Next steps

[Plan for Software Center](plan-for-software-center.md)

[Understand user notifications](user-notifications.md)

[Security and privacy for application management](security-and-privacy-for-application-management.md)
