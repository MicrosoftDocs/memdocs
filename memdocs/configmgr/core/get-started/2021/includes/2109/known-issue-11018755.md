---
author: Banreet
ms.author: banreetkaur
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 09/27/2021
ms.localizationpriority: medium
---

### Configuration Manager console won't automatically update

<!--11018755-->

If you update a technical preview site from version 2108 to a later version, the Configuration Manager console fails to update. This problem is because of a known issue in the extension installer.

To work around this issue, manually update the console. After you update the site from version 2108 to a later version, run **ConsoleSetup.exe**. For more information, see [Install the Configuration Manager console](../../../../servers/deploy/install/install-consoles.md).
