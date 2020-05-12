---
title: Create application groups
titleSuffix: Configuration Manager
description: Create a group of applications that you can send to a user or device collection as a single deployment in Configuration Manager.
ms.date: 04/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual


ms.assetid: e67c691e-62ef-4f43-9cfb-0e957d1e7a5f
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Create application groups

*Applies to: Configuration Manager (current branch)*

<!--3555907-->

Starting in version 1906, create a group of applications that you can send to a user or device collection as a single deployment. The metadata you specify about the app group is seen in Software Center as a single entity. You can order the apps in the group so that the client installs them in a specific order.

> [!Note]  
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

> [!Important]  
> Don't create or deploy an app group until you update the entire hierarchy and targeted clients to at least version 1906.

### Known issues

- *Version 1906*: Apps in the group can only contain **Windows Installer** or **Script** deployment types.
  - *Version 1906*: Set the deployment type installation behavior to **Install for system**.
- The following deployment options may not work: alerts, approval, phased deployment, repair.
- You can't export or import app groups.
- Don't include in the group any apps that require restart, or the group deployment may fail.
- *Version 1906*: You can't deploy the app group to a user collection.
- *Version 1906*: Users can't **Uninstall** the app group in Software Center.
- If you delete an app that's a part of an app group, you'll see the following warning when you next view the properties of the app group: "Unable to load information about all applications in the group." Make a simple change to the app group and save it. For example, add a space to the **Administrator comments**. When you save the change, it removes the deleted app from the group.<!-- 7099542 -->
