---
title: Sample queries for application management
titleSuffix: Configuration Manager
description: Sample queries that show how to join the most common application management views to other views.
ms.date: 04/30/2019
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: how-to


ms.assetid: c0d69334-75eb-408c-8828-94898cf134f5
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
---

# Sample queries for application management in Configuration Manager

The following sample queries demonstrate how to join the most common application management views to other views.

## Joining package and program deployment and collection views

The following query lists all package and program deployments by advertisement ID, advertisement name, and the collection that was targeted for the deployment. The **v_Advertisement** view is joined to the **v_Collection** view by using the **AdvertisementID** column.

```sql
    SELECT ADV.AdvertisementID, ADV.AdvertisementName, 
    COL.CollectionID, COL.Name as CollectionName 
    FROM v_Advertisement ADV INNER JOIN v_Collection COL 
    ON ADV.CollectionID = COL.CollectionID 
    ORDER BY ADV.AdvertisementID 
```

## See also

[Application management views in Configuration Manager](application-management-views-configuration-manager.md)
