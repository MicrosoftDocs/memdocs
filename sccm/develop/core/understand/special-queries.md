---
title: "Special Queries"
titleSuffix: "Configuration Manager"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: d9378514-6125-4bbe-b0bf-7e84e688203esearchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# Configuration Manager Special Queries
Extended WMI Query Language (WQL) supports queries that are specific to System Center Configuration Manager needs. The following table describes the additional queries that are supported.  

 Array property  
 Particular values in an array property.  

 Base class  
 Property values that exist in a base class.  

 Prototype  
 A class definition rather than class data.  

 Collection-limiting  
 Data that is specific to a particular collection.  

## Array Property Queries  
 Due to the nature of array properties, including them in an extended WQL query can be somewhat complex. For example, consider the `SMS_R_System` class that includes the `IPAddresses` property. The `IPAddresses` property is an array that contains one or more individual addresses. To query for computers with IP addresses, you can specify one of the following two queries.  

 SELECT * FROM SMS_R_System WHERE IPAddresses = "2.2.2.2"  

 SELECT * FROM SMS_R_System WHERE IPAddresses IN ("1.1.1.1", "2.2.2.2")  

## Base Class Queries  
 Extended WQL queries on a base class return instances from all the subclasses. For abstract base class queries, the instances that are returned are always instances of the derived classes. For example, the following query returns instances from classes such as `SMS_SCI_Component` and `SMS_SCI_Address`, which inherit properties from `SMS_SiteControlItem`.  

 `SELECT * FROM SMS_SiteControlItem WHERE Sitecode="ABC"`  

## Prototype Queries  
 Extended WQL allows you to request that the result set contains a definition of the class to be returned rather than the actual instances of the class. There are two possible results from this type of query. For most cases, a prototype query returns a class object that contains the definition. If the query is a JOIN operation with multiple classes in the SELECT statement, the prototype query returns an instance of the __Generic class.  

 Although prototype queries are most useful in processing the results of JOIN operations, they are supported for all queries. To request a class definition as the result set, set the `lFlags` parameter in `IWbemServices::ExecQuery` or `IWbemServices::ExecQueryAsync` to WBEM_FLAG_PROTOTYPE.  

## Collection-limiting Queries  
 A System Center Configuration Manager collection is a grouping of resources such as computers and users. Extended WQL supports queries against particular collections. There are two approaches that you can use to limit a query to a particular collection:  

 Set the LimitToCollectionIDs context value to the required CollectionID value. This context value is made available through the IWbemContext pointer in the `IWbemServices::ExecQuery` method to the name of the collection.  

 Specify an inner JOIN operation by using the `SMS_CollectionMember`-derived classes in the query that is passed to ExecQuery.  

 The second approach is slower, but it is the only possible approach if you use an application that uses the WMI ODBC Adapter.  

## See Also  
 [Configuration Manager Association Classes](../../../develop/core/understand/association-classes.md)   
 [Configuration Manager Bit Field Properties](../../../develop/core/understand/configuration-manager-bit-field-properties.md)   
 [Configuration Manager Date and Time Formats](../../../develop/core/understand/date-and-time-formats.md)   
 [Configuration Manager Embedded Objects](../../../develop/core/understand/embedded-objects.md)   
 [Configuration Manager Extended WMI Query Language](../../../develop/core/understand/extended-wmi-query-language.md)   
 [How to Use Configuration Manager Objects With Managed Code](../../../develop/core/understand/how-to-use-configuration-manager-objects-with-managed-code.md)   
 [Configuration Manager Lazy Properties](../../../develop/core/understand/configuration-manager-lazy-properties.md)   
 [Configuration Manager Objects](../../../develop/core/understand/configuration-manager-objects-overview.md)   
 [Configuration Manager Errors](../../../develop/core/understand/configuration-manager-errors.md)   
 [Configuration Manager Object Security](../../../develop/core/understand/configuration-manager-object-security.md)
