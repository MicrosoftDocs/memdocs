---
title: Diagnostics data collection
titleSuffix: Configuration Manager
description: Learn about how Configuration Manager collects diagnostics and usage data about itself.
ms.date: 08/10/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# How Configuration Manager collects diagnostics and usage data

*Applies to: Configuration Manager (current branch)*

To collect diagnostics and usage data for Configuration Manager, each primary site runs SQL Server queries on a weekly basis. In a multi-site hierarchy, the data is replicated to the central administration site.

At the top-level site of a hierarchy, the service connection point submits this information when it checks for updates. The mode of the service connection point determines how the data is transferred:

- **Online**: Once a week, the service connection point automatically sends diagnostics and usage data to the cloud service.

- **Offline**: You manually transfer diagnostics and usage data with the [service connection tool](../../servers/manage/use-the-service-connection-tool.md).

For more information, see [About the service connection point](../../servers/deploy/configure/about-the-service-connection-point.md).

Next, you can view diagnostic and usage data to confirm that your Configuration Manager hierarchy contains no sensitive information:

> [!div class="nextstepaction"]
> [How to view diagnostics and usage data](view-diagnostics-and-usage-data.md)

> [!TIP]
> The **ConfigurationManager** PowerShell module also collects usage data. For more information, see [Configuration Manager cmdlet library privacy statement](/powershell/sccm/privacy-statement).
>
> Some of the tools that are included with Configuration Manager collect usage data. For more information, see [Diagnostic usage data for tools](tools.md).
