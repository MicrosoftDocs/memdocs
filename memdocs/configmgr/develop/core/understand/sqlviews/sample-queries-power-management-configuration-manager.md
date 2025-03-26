---
title: Sample queries for power management
titleSuffix: Configuration Manager
description: Sample queries that show how to join power management views to other views.
ms.date: 04/30/2019
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: how-to


ms.assetid: 4a68faf9-29c7-458b-b3ef-fb99aad5ee7d
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
---

# Sample queries for power management in Configuration Manager

The following sample queries demonstrate how to join power management views to other views.

## Joining power management views to discovery views

The following query lists all computers, by Netbios name, that are excluded from power management because the user chose to exclude them.

The query returns the Netbios name and the domain of the computer and also the client opt-out setting where this value is 1 (indicating that the computer has been excluded from power management).

```sql
    SELECT        v_R_System.Name0, v_R_System.Resource_Domain_OR_Workgr0, 
                             v_GS_POWER_MANAGEMENT_CLIENTOPTOUT_SETTINGS.IsClientOptOut0
    FROM            v_R_System INNER JOIN
                             v_GS_POWER_MANAGEMENT_CLIENTOPTOUT_SETTINGS ON 
                             v_R_System.ResourceID = v_GS_POWER_MANAGEMENT_CLIENTOPTOUT_SETTINGS.ResourceID
    WHERE        (v_GS_POWER_MANAGEMENT_CLIENTOPTOUT_SETTINGS.IsClientOptOut0 = 1)
```

## See also

[Power management views in Configuration Manager](power-management-views-configuration-manager.md)
