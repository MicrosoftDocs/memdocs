---
title: Sample queries for Wake on LAN
titleSuffix: Configuration Manager
description: Sample queries that show how to join Wake On LAN views to application management, discovery, and compliance settings views.
ms.date: 04/30/2019
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: conceptual


ms.assetid: 8a1dcdff-9578-447c-b3cf-3c72166bf7cc
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
---

# Sample queries for Wake On LAN in Configuration Manager

The following sample queries demonstrate how to join Wake On LAN views to application management, discovery, and compliance settings views. The Wake On LAN views are most often joined to other views by using the **ObjectID** and **ResourceID** columns, and to other Wake On LAN views by using the **ObjectType** column.

## Joining Wake On LAN, application management, and compliance settings views

The following query retrieves the Configuration Manager object type, the deployment ID or advertisement ID, and the name for all objects that have Wake On LAN enabled. The results are sorted by object type and then by object name. The query joins the **v_WOLGetSupportedObjects** and **v_WOLEnabledObjects** Wake On LAN views by using the ObjectType column; joins the **v_WOLEnabledObjects** view with the **v_Advertisement** software distribution view by performing a LEFT OUTER JOIN on the **ObjectType** and **AdvertisementID** columns, respectively; and joins the **v_WOLEnabledObjects** view with the **v_CIAssignment** desired configuration management view by performing a LEFT OUTER JOIN on the **ObjectType** and **Assignment_UniqueID** columns, respectively. Using the LEFT OUTER JOIN retrieves all records from the **v_WOLEnabledObjects** view and only the associated records from the **v_Advertisement** and **v_CIAssignment** views.

```sql
    SELECT v_WOLGetSupportedObjects.Name AS [Object Type], 
    v_CIAssignment.AssignmentID AS DeploymentID, v_Advertisement.AdvertisementID 
    ��v_WOLEnabledObjects.ObjectName AS Name 
    FROM v_WOLGetSupportedObjects INNER JOIN v_WOLEnabledObjects ON 
    ��v_WOLGetSupportedObjects.ObjectType = v_WOLEnabledObjects.ObjectType 
    ��LEFT OUTER JOIN v_Advertisement ON 
    ��v_WOLEnabledObjects.ObjectID = v_Advertisement.AdvertisementID 
    ��LEFT OUTER JOIN v_CIAssignment ON 
    ��v_WOLEnabledObjects.ObjectID = v_CIAssignment.Assignment_UniqueID 
    ORDER BY [Object Type], Name 
```

## Joining Wake On LAN and discovery views

The following query retrieves client computers, by NetBIOS name, that have been targeted for an advertisement or deployment with Wake On LAN enabled, as well as the name of the advertisement or deployment, the type of object, and the advertisement ID or deployment ID. The results are sorted by NetBIOS name, object type, and then object ID. The query joins the **v_WOLTargetedClients** Wake On LAN view with the **v_R_System** discovery view by using the **ResourceID** column, joins the **v_WOLEnabledObjects** and **v_WOLTargetedClients** Wake On LAN views by using the **ObjectID** column, joins the **v_WOLGetSupportedObjects** and **v_WOLEnabledObjects** Wake On LAN views by using the **ObjectType** column.

```sql
    SELECT v_R_System.Netbios_Name0 AS Computer, v_WOLEnabledObjects.ObjectName, 
    ��v_WOLGetSupportedObjects.Name AS ObjectType, v_WOLEnabledObjects.ObjectID 
    FROM v_WOLTargetedClients INNER JOIN v_R_System ON 
    ��v_WOLTargetedClients.ResourceID = v_R_System.ResourceID INNER JOIN v_WOLEnabledObjects ON 
    ��v_WOLTargetedClients.ObjectID = v_WOLEnabledObjects.ObjectID INNER JOIN v_WOLGetSupportedObjects ON 
    ��v_WOLEnabledObjects.ObjectType = v_WOLGetSupportedObjects.ObjectType 
    ORDER BY Computer, v_WOLGetSupportedObjects.ObjectType, v_WOLEnabledObjects.ObjectID 
```

## See also

[Wake On LAN views in Configuration Manager](wake-lan-views-configuration-manager.md)
