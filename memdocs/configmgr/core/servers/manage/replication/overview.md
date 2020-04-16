---
title: Troubleshoot SQL replication
titleSuffix: Configuration Manager
description: Use these diagrams to help understand and troubleshoot SQL replication between Configuration Manager sites
ms.date: 02/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 71d7430e-c5aa-485b-8dc0-c80fd8f29f17
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Troubleshoot SQL replication

In a multi-site hierarchy, Configuration Manager uses SQL replication to transfer data between sites. For more information, see [Database replication](/sccm/core/plan-design/hierarchy/database-replication).

To better understand and help troubleshoot issues with SQL replication, use these diagrams.

- [SQL replication](/sccm/core/servers/manage/replication/sql-replication)
- [SQL configuration](/sccm/core/servers/manage/replication/sql-configuration)
- [SQL performance](/sccm/core/servers/manage/replication/sql-performance)
- [SQL replication reinitialization (reinit)](/sccm/core/servers/manage/replication/sql-replication-reinit)
- [Global data reinit](/sccm/core/servers/manage/replication/global-data-reinit)
- [Site data reinit](/sccm/core/servers/manage/replication/site-data-reinit)
- [Reinit missing message](/sccm/core/servers/manage/replication/reinit-missing-message)

These troubleshooting diagrams are interconnected. Use the following diagram to understand their relationships:

![Overview diagram of process for troubleshooting SQL replication](media/overview.png)

<!-- PNG used instead of SVG because of weird blankspace in the SVG. The SVG file exists in the same location. -->

For more information, see the following series of blogs from Microsoft Support:

- [ConfigMgr DRS Synchronization Internals](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-drs-synchronization-internals/ba-p/1154317)
- [ConfigMgr 2012 Data Replication Service (DRS) Unleashed](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-data-replication-service-drs-unleashed/ba-p/339916)
- [ConfigMgr 2012 DRS – Troubleshooting FAQs](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-troubleshooting-faqs/ba-p/339934)
- [ConfigMgr 2012 DRS Initialization Internals](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-initialization-internals/ba-p/339948)
- [ConfigMgr 2012: DRS and SQL service broker certificate issues](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-and-sql-service-broker-certificate-issues/ba-p/339910)
