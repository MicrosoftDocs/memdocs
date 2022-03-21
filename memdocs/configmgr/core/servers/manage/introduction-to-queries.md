---
title: Introduction to queries
titleSuffix: Configuration Manager
description: Create and run queries to locate objects in a Configuration Manager hierarchy that match your query criteria.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---
# Introduction to queries in Configuration Manager

*Applies to: Configuration Manager (current branch)*

You can create and run queries to locate objects in a Configuration Manager hierarchy that match your query criteria. These objects include items like specific types of computers or user groups. Queries can return most types of Configuration Manager objects, which include sites, collections, applications, and inventory data.  

## Query creation overview

 When you create a query, you must specify a minimum of two parameters: where you want to search and what you want to search for. For example, to find the amount of hard drive space that's available on all computers in a Configuration Manager site, you can create a query to search the **Logical Disk** attribute class and the **Free Space (MB)** attribute for available hard drive space.  

 After you create an initial query, you can specify additional query criteria. For example, you can specify that the query results include only computers that are assigned to a specified site. You can also change how results are displayed so you can view the results in an order that's meaningful to you. For example, you can specify that the results are sorted by the amount of free hard drive space, in either ascending or descending order.  

 When you create a query, it's stored by Configuration Manager and displayed in the **Queries** node in the **Monitoring** workspace. From this location, you can create new queries and run, update, and manage existing queries.  

 You can also import a query into a query rule in a Configuration Manager collection. For more information, see [How to create collections](../../../core/clients/manage/collections/create-collections.md).  

## Next steps

 [How to create queries](../../../core/servers/manage/create-queries.md)
