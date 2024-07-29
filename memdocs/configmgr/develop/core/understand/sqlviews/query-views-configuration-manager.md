---
title: Query views
titleSuffix: Configuration Manager
description: Information about all the queries in the Configuration Manager hierarchy.
ms.date: 04/30/2019
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: conceptual


ms.assetid: 87b3f582-449b-4659-be0b-265fecdda6dd
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
---

# Query views in Configuration Manager

Configuration Manager has only one query view, **v_Query**. It contains information about all the queries in the Configuration Manager hierarchy. The query ID, query name, comment, target class name, and the collection ID to which the query is limited, if applicable, are all listed.

The **v_Query** view can be joined to the **v_CollectionRuleQuery** collection view by using the **QueryID** column and to collection views by using the **LimitToCollectionID** column, which contains the same information as the **CollectionID** column in other views. It's also possible to join the query view to a security view so that the query name can be displayed when listing the class or instance permissions on the specific query object. An example is available in the section [Sample queries for queries in Configuration Manager](sample-queries-for-queries-configuration-manager.md).

## See also

[SQL Server views in Configuration Manager](sql-server-views-configuration-manager.md)  
