---
title: "Schema SQL Views"
titleSuffix: "Configuration Manager"
ms.custom: ""
ms.date: "03/08/2018"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: 0da896ff-441e-4ee3-af8b-ff79ccca73bc
searchScope:
 - ConfigMgr SDK
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# Configuration Manager Schema SQL Views
In Configuration Manager, a number of schema information views are created to get information about the names of all the available views and the schema for the inventory and discovery classes. These are particularly useful for determining the names for custom inventory resource type (architecture) tables. The following table shows a list of these schema information views.  

|View|Description|  Sample Query |
|----------|-----------------|----------------- |
|v_SchemaViews|Lists all the views in the view schema family.|  `Select ViewName, Type from v_SchemaViews order by ViewName`|
|v_ResourceMap|Lists the resource type views.|  `select * from v_ResourceMap`|
|v_ResourceAttributeMap|Lists attributes for each resource type.| `select * from v_ResourceAttributeMap`  |
|v_GroupMap|Lists inventory groups for each inventory architecture.| `select * from v_GroupMap` |
|v_GroupAttributeMap|Lists attributes for each inventory group.| `select * from v_GroupAttributeMap` |
|v_ReportViewSchema|Parallel to the `SMS_ReportViewSchema` class, this view lists all the classes and properties.| `select * from v_ReportViewSchema` |

 For more information about how the SQL views map to their WMI class equivalents, see [Configuration Manager Schema View Mapping](../../../develop/core/understand/configuration-manager-schema-view-mapping.md)  

## See Also  
 [About Configuration Manager Schema](../../../develop/core/understand/about-configuration-manager-schema.md)   
 [Configuration Manager Schema Overview](../../../develop/core/understand/configuration-manager-schema-overview.md)   
 [Configuration Manager Schema View Mapping](../../../develop/core/understand/configuration-manager-schema-view-mapping.md)   
 [Configuration Manager SQL View Security](../../../develop/core/understand/sql-view-security.md)
