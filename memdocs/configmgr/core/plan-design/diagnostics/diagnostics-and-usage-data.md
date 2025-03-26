---
title: Diagnostics and usage data
titleSuffix: Configuration Manager
description: Learn about the diagnostics and usage data that Configuration Manager collects about itself.
ms.date: 08/10/2021
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: article
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Diagnostics and usage data for Configuration Manager

*Applies to: Configuration Manager (current branch)*

Configuration Manager collects diagnostics and usage data about itself, which is used by Microsoft to improve the installation experience, quality, and security of future releases.

Each Configuration Manager hierarchy enables diagnostics and usage data. It consists of SQL Server queries that run on a weekly basis on each primary site and at the central administration site (CAS). When the hierarchy uses a CAS, child primary sites replicate their data to that CAS. At the top-level site of your hierarchy, the [service connection point](../../servers/deploy/configure/about-the-service-connection-point.md) submits this information when it checks for updates. If the service connection point is in offline mode, you transfer the information by using the [service connection tool](../../servers/manage/use-the-service-connection-tool.md).

> [!NOTE]
> Configuration Manager collects data only from the site's SQL Server database, and it doesn't collect data directly from clients or site servers.

For more information, see the [Microsoft privacy statement](https://privacy.microsoft.com/privacystatement).

Next, learn about how Microsoft uses the diagnostics and usage data that Configuration Manager collects:

> [!div class="nextstepaction"]
> [How Microsoft uses diagnostics and usage data](how-diagnostics-and-usage-data-is-used.md)

> [!TIP]
> The **ConfigurationManager** PowerShell module also collects usage data. For more information, see [Configuration Manager cmdlet library privacy statement](/powershell/sccm/privacy-statement).
>
> Some of the tools that are included with Configuration Manager collect usage data. For more information, see [Diagnostic usage data for tools](tools.md).
