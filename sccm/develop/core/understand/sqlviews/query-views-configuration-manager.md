---
title: Query Views
titleSuffix: Configuration Manager
description: Information about all the queries in the Configuration Manager hierarchy.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other #app client compliance hybrid osd protect sum
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 87b3f582-449b-4659-be0b-265fecdda6dd
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Query Views in Configuration Manager

Configuration Manager has only one query view, **v\_Query**. It contains information about all the queries in the Configuration Manager hierarchy. The query ID, query name, comment, target class name, and the collection ID to which the query is limited, if applicable, are all listed.

The **v\_Query** view can be joined to the **v\_CollectionRuleQuery** collection view by using the **QueryID** column and to collection views by using the **LimitToCollectionID** column, which contains the same information as the **CollectionID** column in other views. It is also possible to join the query view to a security view so that the query name can be displayed when listing the class or instance permissions on the specific query object. An example of this is available in the section [Sample Queries for Queries in Configuration Manager](https://docs.microsoft.com/en-us/previous-versions/system-center/system-center-2012-R2/dn581990(v=technet.10)).

## See Also

[SQL Server Views in Configuration Manager](sql-server-views-configuration-manager.md)  