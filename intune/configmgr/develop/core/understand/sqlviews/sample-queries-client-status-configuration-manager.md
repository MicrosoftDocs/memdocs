---
title: Sample queries for client status
description: Sample queries that show how to join common client status views to other views.
ms.date: 04/30/2019
ms.subservice: sdk
ms.topic: how-to


ms.collection: tier3
---

# Sample queries for client status in Configuration Manager

The following sample queries demonstrate how to join common client status views to other views.

## Joining client status and collection views

This query lists each client computer in the site, the last time it requested policy, and the collections to which the computer belongs. The query uses the **v_CH_PolicyRequestHistory** view to read the last policy request time and joins, using the **ResourceID** column to the **v_ClientCollectionMembers** view.

```sql
    SELECT        dbo.CH_PolicyRequestHistory.MachineID AS ResourceID, dbo.CH_PolicyRequestHistory.RequestTime, dbo.v_ClientCollectionMembers.CollectionID
    FROM            dbo.CH_PolicyRequestHistory INNER JOIN
                             dbo.v_ClientCollectionMembers ON dbo.CH_PolicyRequestHistory.MachineID = dbo.v_ClientCollectionMembers.ResourceID
```

## See also

[Client status views in Configuration Manager](client-status-views-configuration-manager.md)
