---
title: Revise and supersede applications
titleSuffix: Configuration Manager
description: Learn how to work with Configuration Manager application versions and supersede applications.
ms.date: 12/16/2021
ms.subservice: app-mgt
ms.service: configuration-manager
ms.topic: how-to
author: baladelli
manager: apoorvseth
ms.author: baladell
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Revise and supersede applications in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Learn how to work with Configuration Manager application versions and how to supersede applications with a new version.

## Revisions

When you make revisions to an application or a deployment type, Configuration Manager creates a new revision of the application. You can display the history of each application revision. You can also view its properties, restore a previous revision of an application, or delete an old revision.

### Display the history of application revisions

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Application Management**, and select the **Applications** node. Then choose the application that you want.

1. On the **Home** tab of the ribbon, in the **Application** group, select **Revision History**. This action opens the **Application Revision History** window.

### View an application revision

1. In the **Application Revision History** window, select an application revision, and then select **View**.

1. In the **Properties** dialog box, examine the properties of the selected application.

    > [!NOTE]
    > This view of application properties is read-only.

### Restore an application revision

1. In the **Application Revision History** window, select an application revision, and then select **Restore**.

1. Select **Yes** to restore the selected application revision.

### Delete an application revision

1. In the **Application Revision History** window, select an application revision, and then select **Delete**.

1. Select **Yes** to confirm.

> [!IMPORTANT]
> You can only delete the current application revision after you retire the application and it has no references.

## Supersedence

Application management in Configuration Manager lets you upgrade or replace existing applications by using a supersedence relationship. When you supersede an application, you specify a new deployment type to replace the deployment type of the superseded application. You can also decide whether to upgrade or uninstall the superseded application before the client installs the superseding application. It's best to limit supersedence chains to five levels deep at a maximum.

> [!IMPORTANT]
> When you choose the option to uninstall the superseded deployment type, a deployment type can't be superseded by a deployment type that was deployed to a different type of collection. For example, a deployment type that was deployed to a device collection can't be superseded by a deployment type that was deployed to a user collection.

### Decide whether to upgrade or replace an application

The type of supersedence depends on whether you select the **Uninstall** option:

- If you want to update to a newer version of the same application with the same application ID, _don't_ select **Uninstall**.

- If you want to change to a different application with a different application ID, select **Uninstall**. You need to remove the superseded version of the application.

### Supersede dependent applications

In this example, _main application_ refers to the app that you're deploying that has the dependencies.

You can create a supersedence relationship that updates the dependent application to a new version.

1. Make sure that the new dependent application and the original dependent application are in the same dependency group of the main application.

1. Create a supersedence relationship that supersedes the original dependent application with the new dependent application.

During new installations of the main application, the client installs the new dependent application. Configuration Manager updates existing installations of the main application with the new dependent application.

The end result is that all deployments of the main application use the new dependent application.

### Further considerations

- You can specify multiple supersedence relationships for dependent applications. Configuration Manager installs the highest dependent application in the supersedence chain.

- Deploy dependent applications to the device where the main application is installed. Otherwise Configuration Manager won't install the dependent application.

- For new installations of the main application, when you have multiple dependencies, the dependency order determines which version of the dependent application gets installed.

### Specify a supersedence relationship

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Application Management**, and select the **Applications** node. Then choose the application that supersedes another application.

1. On the **Home** tab of the ribbon, in the **Properties** group, select **Properties**.

1. Switch to the **Supersedence** tab, and select **Add**.

1. For the **Superseded Application**, select **Browse**.

1. Choose the application that you want to supersede, and then select **OK**.

1. In the **Specify Supersedence Relationship** window, select the deployment type that replaces the deployment type of the superseded application.

    > [!NOTE]
    > By default, the new deployment type doesn't uninstall the deployment type of the superseded application. This scenario is commonly used when you want to deploy an upgrade to an existing application. To remove the existing deployment type before the new deployment type is installed, select **Uninstall**. If you decide to upgrade an application, make sure that you test this in a lab environment first.

1. If you want users to still see in Software Center deployments for both applications, select the option to **Allow users to see deployments for this application and all applications that it supersedes in Software Center.**. With this option, you give users the choice to still install an older version of the app if needed. By default, this option isn't selected, so only the superseding application displays in Software Center. This option is only for available deployments to user collections.<!-- MEMDocs#977 -->

1. Select **OK** to save your changes and close the windows.

### Display applications that supersede the current application

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Application Management**, and select the **Applications** node. Then choose the application that you want.

1. On the **Home** tab of the ribbon, in the **Properties** group, select **Properties**.

1. Switch to the **References** tab.

1. For the **Relationship type**, choose **Applications that supersede this application**.

### View supersedence relationships

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Application Management**, and select the **Applications** node. Then choose the application that you want.

1. On the **Home** tab of the ribbon, in the **Relationships** group, select **View relationships**, and then select **Supersedence**.

This action shows a graphical diagram of the relationships of the selected application to other applications. For the supersedence relationships, it shows applications that the selected application supersedes, and applications that the selected application is superseded by.

### Manage supersedence with PowerShell

You can add, view, and remove supersedence relationships using the following PowerShell cmdlets:

- [Get-CMDeploymentTypeSupersedence](/powershell/module/configurationmanager/get-cmdeploymenttypesupersedence)
- [Set-CMApplicationSupersedence](/powershell/module/configurationmanager/set-cmapplicationsupersedence)

## Next steps

[Uninstall applications](uninstall-applications.md)
