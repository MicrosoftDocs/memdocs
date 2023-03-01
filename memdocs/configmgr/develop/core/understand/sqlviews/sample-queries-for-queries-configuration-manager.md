---
title: Sample queries for the query view
titleSuffix: Configuration Manager
description: Sample queries that show how the query view can be joined to a security view.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual


ms.assetid: f03a4839-c731-44c3-99e7-fffc4885cae9
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
---

# Sample queries for the query view in Configuration Manager

The following sample query demonstrates how the query view can be joined to a security view. In most cases, the **v_Query** view won't be used in reports.

## Joining query and security views

The following query lists the query ID, query name, user name, and instance permissions for the user on the query object. The **v_Query** view is joined to the **v_UserInstancePermNames** security view by using the **QueryID** from **v_Query** and **InstanceKey** from **v_UserInstancePermNames**. Because there might be other secured objects with the same value as the **InstanceKey** (for example, MCM00001 could be a custom query or a package), the query also filters specifically for query objects by using the WHERE clause and an **ObjectKey** value of 7.

```sql
    SELECT Q.QueryID, Q.Name AS QueryName, UIP.UserName, UIP.PermissionName 
    FROM v_Query Q INNER JOIN v_UserInstancePermNames UIP 
    ON Q.QueryID = UIP.InstanceKey 
    WHERE UIP.ObjectKey = 7 
    ORDER BY Q.Name, UIP.UserName 
```

## See also

[Query views in Configuration Manager](query-views-configuration-manager.md)
