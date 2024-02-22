---
title: Sample queries for security
titleSuffix: Configuration Manager
description: Sample queries that show how to join security views to other views.
ms.date: 04/30/2019
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: conceptual


ms.assetid: dc2b403f-b824-47ed-a68f-f9473573e199
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
---

# Sample queries for security in Configuration Manager

The following sample queries demonstrate how to join security views to other views.

## Joining security views

The following query lists the user name, object name, and class permission name that the user has on the secured object. The **v_SecuredObject** view is joined to the **v_UserClassPermNames** view by using the **ObjectKey** column.

```sql
    SELECT UCP.UserName, SO.ObjectName, UCP.PermissionName 
    FROM v_SecuredObject SO INNER JOIN v_UserClassPermNames UCP 
    ON SO.ObjectKey = UCP.ObjectKey 
    ORDER BY UCP.UserName, SO.ObjectName, UCP.PermissionName 
```

## Joining security and collection views

The following query lists all collections, by collection ID and collection name, the user name, and the instance permissions for that collection. The **v_Collection** collection view is joined to the **v_UserInstancePermNames** security view by using the **CollectionID** column and the **InstanceKey** column, respectively.

```sql
    SELECT COL.CollectionID, COL.Name AS CollectionName, UIP.UserName, 
    UIP.PermissionName 
    FROM v_Collection COL INNER JOIN v_UserInstancePermNames UIP 
    ON COL.CollectionID = UIP.InstanceKey 
    ORDER BY COL.CollectionID 
```

The output from the preceding query will list all instance permissions for individual collections. If a user has class permissions for the collections object (which includes all instances), another query will need to be run to get all of the permissions for users on the collections object. (An object key of 1 refers to the collection object.)

The following query can be run from the **v_UserClassPermNames** view to list all user class permissions for the collections object.

```sql
    SELECT UserName, PermissionName 
    FROM v_UserClassPermNames 
    WHERE ObjectKey = 1 
```

When using the two preceding queries together, a list of user permissions for all collection classes and instances can be obtained.

## See also

[Security views in Configuration Manager](security-views-configuration-manager.md)
