---
title: Sample queries for content management
titleSuffix: Configuration Manager
description: Sample queries that show how to join the most common content management views to other views.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual


ms.assetid: 07c979e1-6e57-464a-9c87-6cfe8036a39b
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
---

# Sample queries for content management in Configuration Manager

The following sample queries demonstrate how to join the most common content management views to other views.

## Joining software distribution and package status views

The following query lists all packages by package ID and package name, the current status of each package, the Network Abstraction Layer (NAL) path for the distribution point, and the last time the package was refreshed on the distribution point. The **v_Package** view is joined to the **v_PackageStatusDetailSumm** status view and **v_DistributionPoint** software distribution view by using the **PackageID** columns.

```sql
    SELECT PCK.PackageID, PCK.Name as PackageName, PSD.Targeted, 
    PSD.Installed, PSD.Retrying, PSD.Failed, DP.ServerNALPath, 
    DP.LastRefreshTime 
    FROM v_Package PCK INNER JOIN v_PackageStatusDetailSumm PSD 
    ON PCK.PackageID = PSD.PackageID INNER JOIN v_DistributionPoint DP 
    ON PCK.PackageID = DP.PackageID 
    ORDER BY PCK.PackageID 
```

## See also

[Content management views in Configuration Manager](content-management-views-configuration-manager.md)
