---
title: Sample queries for hardware inventory
titleSuffix: Configuration Manager
description: Sample queries that show how to join hardware inventory views to other views that contain system data.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
---

# Sample queries for hardware inventory in Configuration Manager

The following sample queries demonstrate how to join Configuration Manager hardware inventory views to other views that contain system data. Hardware inventory views use the **ResourceID** column when joining to other views.

## List all client OS versions

The following query lists all inventoried Configuration Manager client computers and the operating system and service pack that are running on the client computer. The **v_GS_OPERATING_SYSTEM** hardware inventory view and **v_R_System** discovery view are joined by using the **ResourceID** column, and the results are sorted by the computer name.

```sql
SELECT SYS.Name0,
         OS.Caption0,
         OS.CSDVersion0,
         OS.ResourceID
FROM v_GS_OPERATING_SYSTEM OS
INNER JOIN v_R_System SYS
    ON OS.ResourceID = SYS.ResourceID
```

## List clients with hardware inventory scans more than two days old

The following query lists all active Configuration Manager clients that have not been scanned for hardware inventory in more than two days. The **v_GS_WORKSTATIONSTATUS** hardware inventory view and **v_RA_System_SMSInstalledSites** discovery view are joined to the **v_R_System** discovery view by using the **ResourceID** column.

```sql
    SELECT SYS.Netbios_Name0 as 'Computer Name', 
    SIS.SMS_Installed_Sites0 as 'SMS Site', WS.LastHWScan, 
    DATEDIFF(day,WS.LastHWScan,GETDATE()) as 'Days Since HWScan' 
    FROM v_GS_WORKSTATION_STATUS WS INNER JOIN v_R_System SYS 
    ON WS.ResourceID = SYS.ResourceID INNER JOIN v_RA_System_SMSInstalledSites SIS 
    ON WS.ResourceID = SIS.ResourceID 
    WHERE SYS.Client_Type0 = 1 AND SYS.Active0 = 1 AND 
    WS.LastHWScan < DATEADD([day],-2,GETDATE()) 
```

## See also

[Hardware inventory views in Configuration Manager](hardware-inventory-views-configuration-manager.md)
