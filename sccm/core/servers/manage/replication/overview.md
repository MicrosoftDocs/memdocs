---
title: Troubleshoot SQL replication
titleSuffix: Configuration Manager
description: Use these diagrams to help understand and troubleshoot SQL replication between Configuration Manager sites
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
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

![Overview diagram of process for troubleshooting SQL replication](media/overview.svg)
