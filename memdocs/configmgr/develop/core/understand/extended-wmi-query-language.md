---
title: Extended WMI Query Language
titleSuffix: Configuration Manager
description: A superset of the Windows Management Instrumentation (WMI) Query Language (WQL) known as Extended WQL. Configuration Manager supports both WQL and Extended WQL.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: article
ms.assetid: ea9ebb36-8bd7-49ed-a0d5-8dc6dba104d0
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Configuration Manager Extended WMI Query Language
Configuration Manager supports a superset of the Windows Management Instrumentation (WMI) Query Language (WQL) known as Extended WQL. Both WQL and Extended WQL are retrieval-only languages that are used to create queries. Neither language can be used to create, modify, or delete classes or instances.  

 WQL and Extended WQL are based on the American National Standards Institute (ANSI) Structured Query Language (SQL) standard. However, they differ from standard SQL in that they retrieve from classes rather than tables and return instances rather than rows.  

 Extended WQL supports elements from two versions of ANSI SQL:  

 ANSI-92, which is the recommended version for most operations.  

 ANSI-89, which is primarily used only for `JOIN` operations by Open Database Connectivity (ODBC) applications requiring the services of the WMI ODBC Adapter.  

 Extended WQL includes a much broader range of operations than WQL. The following list shows the `SELECT` clauses that Extended WQL supports:  

 `DISTINCT`  

 `COUNT`  

 `JOIN`  

 `WHERE`  

 `SUBSTRING`  

 `ORDER BY`  

 `UPPER, LOWER`, and `DATEPART` functions  

 Because Extended WQL is fully case-insensitive, the UPPER and LOWER functions are not useful. Extended WQL supports the standard comparison operators (including LIKE and IN) and sub queries.  

 The SMS Provider does not support querying on system properties. System properties are those preceded by a double underscore prefix, for example `__path`.  

 Association queries are limited to the WQL syntax.  

 The use of `COUNT` and `DISTINCT` keywords together in a statement is not supported.  

 in Configuration Manager the `WHERE` clause supports `GetDate()`, `DateDiff()`, `and DateAdd()`.  

 The `ORDER BY` clause does not work with the collection-limiting context qualifier.  

## See Also  
 [Configuration Manager Association Classes](../../../develop/core/understand/association-classes.md)   
 [Configuration Manager Bit Field Properties](../../../develop/core/understand/configuration-manager-bit-field-properties.md)   
 [Configuration Manager Date and Time Formats](../../../develop/core/understand/date-and-time-formats.md)   
 [Configuration Manager Embedded Objects](../../../develop/core/understand/embedded-objects.md)   
 [Objects overview](configuration-manager-objects-overview.md)
 [Configuration Manager Lazy Properties](../../../develop/core/understand/configuration-manager-lazy-properties.md)   
 [About errors](about-configuration-manager-errors.md)
 [Configuration Manager Object Security](../../../develop/core/understand/configuration-manager-object-security.md)   
 [Configuration Manager Special Queries](../../../develop/core/understand/special-queries.md)
