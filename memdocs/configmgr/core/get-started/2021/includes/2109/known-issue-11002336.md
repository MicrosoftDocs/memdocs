---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 09/27/2021
ms.localizationpriority: medium
---

### Reports on SQL Server Reporting Services won't display

<!--11002336-->

If you use Configuration Manager technical preview branch with SQL Server version 2012 or version 2014, when you update to Configuration Manager version 2109, reports aren't shown in the console. You'll see an error similar to the following string in the **srsrp.log**:

`System.Web.Services.Protocols.SoapException: Error while loading code module: ...SrsResources, culture=neutral.... Details: Could not load file or assembly 'SrsResources, Culture=neutral' or one of its dependencies. This assembly is built by a runtime newer than the currently loaded runtime and cannot be loaded.`

To work around this issue, update SQL Server Reporting Services to version 2016 or later. For more information, see [Supported SQL Server versions](../../../../plan-design/configs/support-for-sql-server-versions.md).
