---
title: Update registration tool
titleSuffix: Configuration Manager
description: Find out when and how to use the update registration tool to manually import an update to the Configuration Manager console.
ms.date: 08/02/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# Use the update registration tool to import hotfixes

*Applies to: Configuration Manager (current branch)*

Some updates for Configuration Manager aren't available from the Microsoft cloud service and are only obtained out-of-band. An example is a limited release hotfix to address a specific issue.

When you must install an out-of-band release, and the update or hotfix file name ends with the extension **update.exe**, you use the update registration tool. This tool imports the update to the Configuration Manager console. It enables you to extract and transfer the update package to the site server, and register the update with the Configuration Manager console.

If the hotfix file only has the **.exe** file extension (not **update.exe**), [use the hotfix installer to install the update](use-the-hotfix-installer-to-install-updates.md).

> [!NOTE]
> This article provides general guidance about how to install hotfixes that update Configuration Manager. For details about a specific hotfix or update, refer to the corresponding hotfix article.

## Prerequisites

- This tool only installs out-of-band updates that end with the full **.update.exe** file extension.

- It is self-contained with the individual updates that you get directly from Microsoft.

- The service connection point can be in either online or offline mode.

- Run it on the server with the service connection point site system role.

- Starting in version 2107, the service connection point requires .NET version 4.6.2, and version 4.8 is recommended.<!--10402814--> In version 2103 and earlier, this role requires .NET 4.5.2 or later. For more information, [Site and site system prerequisites](../../plan-design/configs/site-and-site-system-prerequisites.md).

- When you run the tool on the service connection point, the account that you use needs the following configurations:

  - A local **Administrator**

  - **Write** permissions to the following folder: `<Configuration Manager installation directory>\EasySetupPayload\offline`

## Process

1. On the computer that hosts the service connection point, open a command prompt with administrative privileges. Then change directories to the location that contains the update file. The update file name uses the following format: `<Product>-<product version>-<KB article ID>-ConfigMgr.Update.exe`

1. Run the following command to start the update registration tool: `<Product>-<product version>-<KB article ID>-ConfigMgr.Update.exe`

    After the hotfix is registered, it appears as a new update in the console within 24 hours. To accelerate this process: in the Configuration Manager console, go to **Administration** workspace, and select the **Updates and Servicing** node. In the ribbon, select **Check for Updates**.

    The update registration tool logs its actions to a .log file on the local computer. The log file has the same name as the hotfix file and is in the `%SystemRoot%/Temp` folder.

    After the update is registered, you can close the update registration tool.

1. In the Configuration Manager console, go to the **Administration** workspace, and select the **Updates and Servicing** node. Hotfixes that you've imported are now available to install.

## Next steps

[Install in-console updates](install-in-console-updates.md)
