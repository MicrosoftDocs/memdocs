---
title: Sample queries for operating system deployment
titleSuffix: Configuration Manager
description: Sample queries that show how to join operating system deployment views to each other and to compliance settings views.
ms.date: 04/30/2019
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: conceptual


ms.assetid: d31a8e79-87a1-4e4d-bcaa-856006b4889a
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
---

# Sample queries for operating system deployment in Configuration Manager

The following sample queries demonstrate how to join operating system deployment views to each other and to compliance settings views. You can join the operating system deployment views to other operating system deployment views and application management views by using the view column that contains the package ID, which might have different column names depending on the view. You can join the operating system deployment views to compliance settings views by using the **CI_ID** column, and they can be joined to discovery views by using the **ResourceID** column.

## Joining operating system deployment and application management views

The following query lists all task sequence packages, by package ID and package name, the associated boot image package, by package ID and package name, and the source path for the boot image package. The query results are sorted by the task sequence package ID. A LEFT OUTER JOIN is used to join the **v_TaskSequencePackage** and **v_BootImagePackage** operating system deployment views by using the **BootImageID** and **PackageID** columns, respectively.

```sql
    SELECT DISTINCT 
    ��v_TaskSequencePackage.PackageID AS [Task Sequence Package ID], 
    ��v_TaskSequencePackage.Name AS [Task Sequence Package Name], 
    ��v_TaskSequencePackage.BootImageID AS [Boot Image Package ID], 
    ��v_BootImagePackage.Name AS [Boot Image Package Name], 
    ��v_BootImagePackage.PkgSourcePath AS [Boot Image Package Source Path] 
    FROM v_TaskSequencePackage LEFT OUTER JOIN v_BootImagePackage ON 
    ��v_TaskSequencePackage.BootImageID = v_BootImagePackage.PackageID 
    ORDER BY [Task Sequence Package ID] 
```

## Joining operating system deployment and compliance settings views

The following query lists all operating system deployment boot image packages, by package ID and package name, the drivers that are contained in the boot image package, and the source path for the driver. The query results are sorted by the boot image package ID and then by the driver name. The **v_BootImagePackage** and **v_BootImagePackage_References** operating system deployment views are joined by using the **PackageID** and **PkgID** columns, respectively; the **v_BootImagePackage_References** view is joined to the **v_ConfigurationItems** compliance settings view by using the **CI_ID** column; and the **v_ConfigurationItems** view is joined to the **v_LocalizedCIProperties** compliance settings view by using the **CI_ID** column.

```sql
    SELECT v_BootImagePackage.PackageID AS [Boot Image Package ID], 
    ��v_BootImagePackage.Name AS [Boot Image Package Name], 
    ��v_LocalizedCIProperties.DisplayName AS [Driver Name], 
    ��v_BootImagePackage_References.SourcePath AS [Driver Source Path] 
    FROM v_BootImagePackage INNER JOIN v_BootImagePackage_References ON 
    ��v_BootImagePackage.PackageID = v_BootImagePackage_References.PkgID 
    ��INNER JOIN v_ConfigurationItems ON 
    ��v_BootImagePackage_References.CI_ID = v_ConfigurationItems.CI_ID 
    ��INNER JOIN v_LocalizedCIProperties ON 
    ��v_ConfigurationItems.CI_ID = v_LocalizedCIProperties.CI_ID 
    ORDER BY [Boot Image Package ID], [Driver Name] 
```

## See also

[Operating system deployment views in Configuration Manager](operating-system-deployment-views-configuration-manager.md)
