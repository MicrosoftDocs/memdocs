---
title: Data transfers between sites
titleSuffix: Configuration Manager
description: Learn how Configuration Manager moves data between sites, and how you can manage the transfer of the data across your network.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: dc526e8d-fac3-4bb5-b206-03ad29b0ae11
author: mestew
ms.author: mstewart
manager: dougeby


---

# Data transfers between sites

*Applies to: Configuration Manager (current branch)*

Configuration Manager uses *file-based replication* and *database replication* to transfer different types of information between sites. Learn about how Configuration Manager moves data between sites, and how you can manage the transfer of data across your network.  

## Types of replication

### <a name="bkmk_fileroute" /> File-based replication

Configuration Manager uses file-based replication to transfer file-based data between sites in your hierarchy. This data includes applications and packages that you want to deploy to distribution points in child sites. It also handles unprocessed discovery data records that the site transfers to its parent site and then processes.  

For more information, see [File-based replication](file-based-replication.md).

### <a name="bkmk_dbrep" /> Database replication

Configuration Manager database replication uses SQL Server to transfer data. It uses this method to merge changes in its site database with the information from the database at other sites in the hierarchy.

For more information, see [Database replication](database-replication.md).

For help with troubleshooting SQL replication, see [Troubleshoot SQL replication](../../servers/manage/replication/overview.md).

## See also

[Monitor replication](../../servers/manage/monitor-replication.md)
