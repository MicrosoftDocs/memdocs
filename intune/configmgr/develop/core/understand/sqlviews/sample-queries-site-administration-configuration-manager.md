---
title: Sample queries for site administration
titleSuffix: Configuration Manager
description: Sample queries that show how to join site administration views to other views to retrieve specific data.
ms.date: 04/30/2019
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: how-to


ms.assetid: 965581db-786b-413e-a444-26533a339642
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
---

# Sample queries for site administration in Configuration Manager

The following sample queries demonstrate how the Configuration Manager site administration views can be joined to other views to retrieve specific data.

## Joining site administration views

The following sample query demonstrates how to join a site view to another site view. This query lists the boundaries for each site in the Configuration Manager hierarchy, the type of boundary, the boundary value, whether the connection is fast or slow, and the boundary description. The **v_Site** and **v_BoundaryInfo** site views are joined by using the **SiteCode** column. The query results are sorted by site code, boundary type, and then value. The CASE function is used to take a numeric value for boundary type and connection speed and to provide friendly names based on the value.

```sql
    SELECT v_Site.SiteCode, v_Site.ServerName, 
    ��CASE v_BoundaryInfo.BoundaryType 
    ����WHEN 0 THEN 'IP subnet' 
    ����WHEN 1 THEN 'Active Directory site' 
    ����WHEN 2 THEN 'IPv6 Prefix' 
    ����WHEN 3 THEN 'IP address range' 
    ��END AS [Boundary Type], v_BoundaryInfo.Value, 
    ��CASE v_BoundaryInfo.BoundaryFlags 
    ����WHEN 0 THEN 'Fast' 
    ����WHEN 1 THEN 'Slow' 
    END AS Connection, v_BoundaryInfo.DisplayName AS Description 
    FROM v_BoundaryInfo INNER JOIN v_Site ON v_BoundaryInfo.SiteCode = v_Site.SiteCode 
    ORDER BY v_Site.SiteCode, [Boundary Type], v_BoundaryInfo.Value
```

## See also

[Site administration views in Configuration Manager](site-admin-views-configuration-manager.md)
