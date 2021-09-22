---
title: Management tasks for applications
titleSuffix: Configuration Manager
description: Manage Configuration Manager applications and deployment types.
ms.date: 04/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: how-to
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.localizationpriority: medium
---

# Management tasks for Configuration Manager applications

*Applies to: Configuration Manager (current branch)*

Use the information in this article to help you manage Configuration Manager applications and deployment types.

For more information on how to create applications and deployment types, see [Create applications](create-applications.md).

> [!IMPORTANT]
> Depending on the type of application or deployment type, some management options might not be available.

## Manage applications

In the **Software Library** workspace, expand **Application Management**, and select the **Applications** node. Select the application to manage, and then choose a management task in the ribbon.

### Manage access accounts

Use this action to control access to the associated content on distribution points.

When you **Add** an account:

1. Specify one of the following account types:

    - **User**: Any account that Windows can authenticate.
    - **Guest**: An unauthenticated user.
    - **Administrator**: An account that Windows recognizes as an administrator.
    - **Windows User**: A specific user account. It can either be from a local machine or Active Directory.

1. Specify one of the following access rights:

    - **No access**: Explicitly block the specified account type from accessing the content associated with this application.
    - **Read**
    - **Change**
    - **Full control**

By default, the **Administrator** type has **Full control** access, and the **User** type has **Read** access.

### Create prestaged content file

Prestaged content files help you to manage the delivery of content to remote distribution points. When scheduling and throttling options don't provide a valid solution for the remote distribution point, you can prestage the content.

For more information, see [Deploy and manage content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).

### Revision history

View and manage the revisions to this application. For more information, see [How to revise and supersede applications](revise-and-supersede-applications.md#revisions).

### Update statistics

Updates the information that's displayed in the **Deployments** node of the **Monitoring** workspace about the deployments of this application. For more information, see [Monitor applications from the Configuration Manager console](monitor-applications-from-the-console.md).

### Create deployment type

Add a new deployment type to the selected application. For more information, see [Create deployment types for the application](create-applications.md#bkmk_create-dt).

### Convert to .MSIX

Convert an existing Windows Installer (.msi) application to the MSIX format. For more information, see [Support for MSIX format](../get-started/creating-windows-applications.md#bkmk_msix).

### Reinstate

If you previously [retired](#retire) an application, use this action to reinstate it. When you reinstate a retired app, you can then deploy it again.

### Retire

When you retire an application, it's no longer available for deployment. Configuration Manager doesn't delete the application and any deployments. If the app was installed on clients, Configuration Manager doesn't remove the app. Configuration Manager deletes any revisions to the app after 60 days in retirement.

Before you delete an application:

1. Retire the application.
1. Delete all deployments.
1. Remove references to the application by other deployments
1. Delete all of the application's revisions.

For more information, see [Revise and supersede applications](revise-and-supersede-applications.md).

### Export

Export the selected applications to a .zip file that you can archive or import to another site. If you choose to export application content, Configuration Manager creates a folder with the content.

You can export:

- Application dependencies
- Supersedence relationships and conditions
- Content for the application and its dependencies

To automate this process, use the following Configuration Manager PowerShell cmdlets:

- [Export-CMApplication](/powershell/module/configurationmanager/export-cmapplication)
- [Import-CMApplication](/powershell/module/configurationmanager/import-cmapplication)

For more information, see [Import and export applications](import-export-applications.md).

### Copy (application)

Duplicate the application to create a new one. This action is useful to test something or when you need to create a similar application. The site creates a new application, and appends **-copy** to the name. While the site copies most of the metadata to the new application, it doesn't copy any deployments.

### Delete (application)

Delete the currently selected applications.

You can't delete an application if any of the following conditions are true:

- Other applications are dependent on it
- It has an active deployment
- It has dependent task sequences

Before you delete an application, [retire it](#retire).

### Simulate deployment

Test the results of an application deployment to computers without installing or uninstalling it. For more information, see [Simulate application deployments](simulate-application-deployments.md).

### Deploy

Deploy the selected application to a collection of computers. For more information, see [Deploy applications](deploy-applications.md).

### Create phased deployment

Phased deployments automate a coordinated, sequenced rollout of software across multiple collections. For example, deploy software to a pilot collection, and then automatically continue the rollout based on success criteria. For more information, see [Create phased deployments](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/apps/toc.json&bc=/mem/configmgr/apps/breadcrumb/toc.json).

### Distribute content

Copy the content for the selected application to distribution points. For more information, see [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### Move

Move the selected application to another folder in the **Applications** node.

### Set security scopes

Select the security scopes for the selected application. For more information, see [Security scopes](../../core/understand/fundamentals-of-role-based-administration.md#security-scopes).

### Categorize

Administrative categories help you organize apps in the Configuration Manager console. You can add the **Administrative categories** column to the **Applications** node.

With this action, you can:

- Quickly add the selected app to an administrative category.

- Clear all categories on the current app.

- Select **Manage categories** to create, rename, or delete categories.

You can also manage categories on the application properties, **General information** tab.

> [!TIP]
> To help users find apps by category in Software Center, define **user categories** for your apps. You can add these categories on the application properties, **Software Center** tab.

### View relationships

Show a graphical diagram of the relationships of the selected applications to other applications. Choose one of the following relationship types:

- **Dependency**: Shows applications that are dependent on the selected application and the applications that the selected application depends on. For more information, see [Deployment type Dependencies](create-applications.md#bkmk_dt-depend).

- **Supersedence**: Shows applications that the selected application supersedes, and applications that the selected application is superseded by. For more information, see [Supersedence](revise-and-supersede-applications.md#supersedence).

- **Global Conditions**: Shows the global conditions that this application references. For more information, see [Create global conditions](create-global-conditions.md).

### Properties

Display and edit the metadata for this application.

## Manage deployment types

In the **Software Library** workspace, expand **Application Management**, and select the **Applications** node. Select the application with the deployment type that you want to manage. In the details pane, switch to the **Deployment Types** tab. Select the deployment type that you want to manage, and then choose a management task from the **Deployment Type** tab of the ribbon.

### Increase priority

Increase the priority of the selected deployment type. The Configuration Manager client evaluates deployment types in order. If the device meets the deployment type's requirements, it runs the deployment type. Then the client doesn't evaluate any further deployment types on the priority list.

### Decrease priority

Lower the priority of the selected deployment type.

### Copy (deployment type)

Duplicate the deployment type to create a new one. This action is useful to test something or when you need to create a similar deployment type. The site creates a new deployment type on the same application, and appends **-copy** to the name.

### Delete (deployment type)

Delete the selected deployment type. You can't delete a deployment type if it's referenced by a deployment type in another application.

To delete a deployment type:

1. Remove all dependencies from other deployment types.

1. Remove previous revisions of all applications that have a deployment type that references this deployment type.

### Update content

Refresh the content for the selected deployment type. When you refresh the content of a deployment type, the site creates a new revision of the application. This behavior might cause client devices to update with the new application content.

## Next steps

[Import and export applications](import-export-applications.md)

[Revise and supersede applications](revise-and-supersede-applications.md)

[Uninstall applications](uninstall-applications.md)
