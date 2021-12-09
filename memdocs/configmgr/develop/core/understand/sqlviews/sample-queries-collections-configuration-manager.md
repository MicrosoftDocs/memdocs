---
title: Sample queries for collections
titleSuffix: Configuration Manager
description: Sample queries that show how to join some of the most commonly used collection views to other views.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual


ms.assetid: 9b2fec1a-41d1-4c62-8a3b-154e63a67ddf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
---

# Sample queries for collections in Configuration Manager

The following sample queries demonstrate how to join some of the most commonly used collection views to other views.

## Joining collection views

The following query lists the resources in the Configuration Manager hierarchy that are in a collection, the assigned site for client computers, the collection ID, collection name, and the last time the collection was refreshed. The **v_FullCollectionMembership** view is joined to the **v_Collection** view by using the **CollectionID** column. The query results are sorted by resource name and then by collection ID.

```sql
    SELECT FCM.Name, FCM.SiteCode, FCM.CollectionID, 
    ��COL.Name, COL.LastRefreshTime 
    FROM v_FullCollectionMembership FCM INNER JOIN v_Collection COL 
    ��ON FCM.CollectionID = COL.CollectionID 
    ORDER BY FCM.Name, FCM.CollectionID 
```

## Joining collection and resource views

The following query lists all of the discovered resources that do not have a Configuration Manager client installed. The query lists the domain, computer name, and all discovered IP addresses using data by joining three views. The **v_CM_RES_COLL_SMS00001** collection view is joined to the **v_R_System** and **v_RA_IPAddresses** discovery views by using the **ResourceID** column.

```sql
    SELECT SYS.Resource_Domain_OR_Workgr0, COLL1.Name, 
    ��SYSIP.IP_Addresses0 
    FROM v_CM_RES_COLL_SMS00001 COLL1 
    ��INNER JOIN v_R_System SYS 
    ��ON COLL1.ResourceID = SYS.ResourceID 
    ��INNER JOIN v_RA_System_IPAddresses SYSIP 
    ��ON COLL1.ResourceID = SYSIP.ResourceID 
    WHERE COLL1.IsClient = 0 
    ORDER BY SYS.Resource_Domain_OR_Workgr0, COLL1.Name 
```

## Joining collection and deployment views

The following query lists all of the resources in the Configuration Manager hierarchy that have been targeted for an advertisement, as well as the source site code, advertisement ID and advertisement name, program name, and target collection name, and then it sorts the data by the name of the resource. The **v_FullCollectionMembership** collection view is joined to the **v_Advertisement** software distribution view and **v_Collection** collection view by using the **CollectionID** column.

```sql
    SELECT FCM.Name AS ResourceName, FCM.ResourceID, 
    ��ADV.SourceSite, ADV.AdvertisementID, ADV.AdvertisementName, 
    ��ADV.ProgramName, COL.Name AS CollectionName 
    FROM v_FullCollectionMembership FCM INNER JOIN v_Advertisement ADV 
    ��ON FCM.CollectionID = ADV.CollectionID INNER JOIN 
    ��v_Collection COL ON FCM.CollectionID = COL.CollectionID 
    ORDER BY FCM.Name 
```

## See also

[Collection views in Configuration Manager](collection-views-configuration-manager.md)
