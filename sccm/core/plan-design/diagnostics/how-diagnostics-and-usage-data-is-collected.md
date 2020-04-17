---
title: Diagnostics data collection
titleSuffix: Configuration Manager
description: Learn about how Configuration Manager collects diagnostics and usage data about itself.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: becfa825-b19f-448c-ab82-bb929255e4ae
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# How Configuration Manager collects diagnostics and usage data

*Applies to: Configuration Manager (current branch)*

To collect diagnostics and usage data for Configuration Manager, each primary site runs SQL Server queries on a weekly basis. In a multi-site hierarchy, the data is replicated to the central administration site.  

At the top-level site of a hierarchy, the service connection point submits this information when it checks for updates. The mode of the service connection point determines how the data is transferred:

- **Online**: Once a week, the service connection point automatically sends diagnostics and usage data to the cloud service.

- **Offline**: You manually transfer diagnostics and usage data with the [service connection tool](../../servers/manage/use-the-service-connection-tool.md).

For more information, see [About the service connection point](../../servers/deploy/configure/about-the-service-connection-point.md).

> [!div class="nextstepaction"]
> [How to view diagnostics and usage data](view-diagnostics-and-usage-data.md)
