---
title: Diagnostics and usage data
titleSuffix: Configuration Manager
description: Learn about the diagnostics and usage data that Configuration Manager collects about itself.
ms.date: 07/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 88ac4e55-d47b-4c94-b9c3-704c6a48b845
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---

# Diagnostics and usage data for Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Configuration Manager collects diagnostics and usage data about itself, which is used by Microsoft to improve the installation experience, quality, and security of future releases.  

Diagnostics and usage data is enabled for each Configuration Manager hierarchy. It consists of SQL Server queries that run on a weekly basis on each primary site and at the central administration site. When the hierarchy uses a central administration site, the data from primary sites is then replicated to that site. At the top-level site of your hierarchy, the service connection point submits this information when it checks for updates. If the service connection point is in offline mode, the information is transferred by using the service connection tool.  

> [!NOTE]  
> Configuration Manager collects data only from the site's SQL server database, and it does not collect data directly from clients or site servers.  

For more information, see the [Microsoft privacy statement](https://go.microsoft.com/fwlink/?LinkID=626527).  

## Articles

Learn more about diagnostic and usage data for Configuration Manager in the following articles:  

- [How diagnostics and usage data is used](/sccm/core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-used)  

- Levels of diagnostic usage data collection:

    - [Diagnostic data for 1906](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1906)  

    - [Diagnostic data for 1902](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1902)  

    - [Diagnostic data for 1810](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1810)  

    - [Diagnostic data for 1806](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1806)  

- [How diagnostics and usage data is collected](/sccm/core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-collected)  

- [How to view diagnostics and usage data](/sccm/core/plan-design/diagnostics/view-diagnostics-and-usage-data)  

- [Frequently asked questions about diagnostics and usage data](/sccm/core/understand/frequently-asked-questions-about-diagnostics-and-usage-data)  


## See also

[About the service connection point](/sccm/core/servers/deploy/configure/about-the-service-connection-point)
