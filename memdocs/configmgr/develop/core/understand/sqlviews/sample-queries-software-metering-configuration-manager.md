---
title: Sample queries for software metering
titleSuffix: Configuration Manager
description: Sample queries that show how to join the most common software metering views to other views.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual


ms.assetid: 2cf7208f-7684-40a0-9402-656a7abcd583
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
---

# Sample queries for software metering in Configuration Manager

The following sample queries demonstrate how to join the most common software metering views to other views.

## Joining software metering, software inventory, and discovery views

The following query lists all resources that have run metered files, including the resource name, file ID, file name, file version, and start time. The **v_MeterData** software metering view is joined to the **v_ProductFileInfo** software inventory view by using the **FileID** column and to the **v_R_System** discovery view by using the **ResourceID** column.

```sql
    SELECT SYS.Netbios_Name0, PFI.FileID, PFI.FileName, 
    PFI.FileVersion, MD.StartTime 
    FROM v_MeterData MD INNER JOIN v_ProductFileInfo PFI 
    ON MD.FileID = PFI.FileID INNER JOIN v_R_System SYS 
    ON MD.ResourceID = SYS.ResourceID 
    ORDER BY SYS.Netbios_Name0, PFI.FileName 
```

## Joining software metering, status, and software inventory views

The following query lists all users who have run metered files. The query returns the user domain, user name, file name, file version, usage count, total time of usage, and the last time the file was used. The **v_MeteredUser** software metering view is joined to the **v_MonthlyUsageSummary** status view by using the **MeteredUserID** column. The **v_MonthlyUsageSummary** status view is joined to the **v_GS_SoftwareFile** software inventory view by using the **FileID** column.

```sql
    SELECT MU.Domain, MU.UserName, SF.FileName, SF.FileVersion, 
    MUS.UsageCount, MUS.UsageTime, MUS.LastUsage 
    FROM v_MeteredUser MU INNER JOIN v_MonthlyUsageSummary MUS 
    ON MU.MeteredUserID = MUS.MeteredUserID INNER JOIN 
    v_GS_SoftwareFile SF ON MUS.FileID = SF.FileID 
    ORDER BY MU.Domain, MU.UserName, SF.FileName 
```

## See also

[Software metering views in Configuration Manager](software-metering-views-configuration-manager.md)
