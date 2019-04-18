---
title: Sample Queries for Client Status
titleSuffix: Configuration Manager
description: Sample queries that show how to join common client status views to other views.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other #app client compliance hybrid osd protect sum
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: fe4dafee-8ea7-4829-884b-960cc09f6444
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Sample Queries for Client Status in Configuration Manager

The following sample queries demonstrate how to join common client status views to other views.

## Joining Client Status and Collection Views

This query lists each client computer in the site, the last time it requested policy, and the collections to which the computer belongs. The query uses the **v_CH_PolicyRequestHistory** view to read the last policy request time and joins, using the **ResourceID** column to the **v_ClientCollectionMembers** view.

```sql
    SELECT        dbo.CH_PolicyRequestHistory.MachineID AS ResourceID, dbo.CH_PolicyRequestHistory.RequestTime, dbo.v_ClientCollectionMembers.CollectionID
    FROM            dbo.CH_PolicyRequestHistory INNER JOIN
                             dbo.v_ClientCollectionMembers ON dbo.CH_PolicyRequestHistory.MachineID = dbo.v_ClientCollectionMembers.ResourceID
```

## See Also

[Client Status Views in Configuration Manager](client-status-views-configuration-manager.md)