---
title: Create application groups
titleSuffix: Configuration Manager
description: Create a group of applications that you can send to a user or device collection as a single deployment in Configuration Manager.
ms.date: 04/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: how-to
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Create application groups

*Applies to: Configuration Manager (current branch)*

<!--3555907-->

Create a group of applications that you can send to a user or device collection as a single deployment. The metadata you specify about the app group is seen in Software Center as a single entity. You can order the apps in the group so that the client installs them in a specific order.

> [!NOTE]
> In this version of Configuration Manager, app groups are a pre-release feature. To enable it, see [Pre-release features](../../core/servers/manage/pre-release-features.md).

1. In the Configuration Manager console, go to the **Software Library** workspace. Expand **Application Management** and select the **Application Group** node.

1. In the Create group in the ribbon, select **Create Application Group**.

1. On the **General Information** page, specify information about the app group.

1. On the **Software Center** page, include information that shows in Software Center.

1. On the **Application Group** page, select **Add**. Select one or more apps for this group. Reorder them using the **Move Up** and **Move Down** actions.

1. Complete the wizard.

Deploy the app group using the same process as for an application. For more information, see [Deploy applications](deploy-applications.md). Starting in version 1910, you can deploy an app group to device or user collections.

After you deploy the group:

- If you add a new app to the group, you have to separately distribute the new app content to distribution points.

- If you modify an app in the app group, redistribute the content.

To troubleshoot an app group deployment, use the following log files on the client:

- **AppGroupHandler.log**
- **AppEnforce.log**
- **SettingsAgent.log**

> [!IMPORTANT]
> Don't create or deploy an app group until you update the entire hierarchy and targeted clients to at least version 1906.

## Known issues

- The following deployment options may not work: alerts, approval, phased deployment, repair.
- You can't use application groups with the **Install Application** task sequence step.
- You can't export or import app groups.
- Don't include in the group any apps that require restart, or the group deployment may fail.
- If you delete an app that's a part of an app group, you'll see the following warning when you next view the properties of the app group: "Unable to load information about all applications in the group." Make a small change to the app group and save it. For example, add a space to the **Administrator comments**. When you save the change, it removes the deleted app from the group.<!-- 7099542 -->

## PowerShell

You can create and deploy app groups using Windows PowerShell. For more information, see the following cmdlet articles:

- [Get-CMApplicationGroup](/powershell/module/configurationmanager/get-cmapplicationgroup)
- [New-CMApplicationGroup](/powershell/module/configurationmanager/new-cmapplicationgroup)
- [Remove-CMApplicationGroup](/powershell/module/configurationmanager/remove-cmapplicationgroup)
- [Set-CMApplicationGroup](/powershell/module/configurationmanager/set-cmapplicationgroup)
- [Get-CMApplicationGroupDeployment](/powershell/module/configurationmanager/get-cmapplicationgroupdeployment)
- [New-CMApplicationGroupDeployment](/powershell/module/configurationmanager/new-cmapplicationgroupdeployment)
- [Remove-CMApplicationGroupDeployment](/powershell/module/configurationmanager/remove-cmapplicationgroupdeployment)
- [Set-CMApplicationGroupDeployment](/powershell/module/configurationmanager/set-cmapplicationgroupdeployment)

## Next steps

[Deploy applications](deploy-applications.md)
