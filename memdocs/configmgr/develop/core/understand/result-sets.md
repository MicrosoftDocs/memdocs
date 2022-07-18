---
title: "Configuration Manager Result Sets"
description: "Result sets of a query contain one or more instances that match the specified criteria of the SELECT statement in Configuration Manager. The result instances are either Generic class instances or instances of the class specified in the FROM clause."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: e27f8d92-e7b1-4bde-a75c-8c88f1275829
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# Configuration Manager Result Sets
In Configuration Manager, the result set of a query contains one or more instances that match the specified criteria of the`SELECT` statement. The result instances are either `Generic` class instances or instances of the class that is specified in the FROM clause.  

## __Generic Class Results  
 The results of a `JOIN` operation are returned in either an instance of a class specified in the query or an instance of the __`Generic` class. If a single class is implied by the property list in the SELECT statement, the results are returned as instances of that class. If there are multiple classes, the results are returned as instances of the **\__Generic** class.  

 The __`Generic` class is a generic container for the results of `JOIN` operations and `COUNT` operations. This class has no set definition. Its properties depend on its use at the time. For `JOIN` results, the properties are embedded objects representing the classes specified in the query, as the following example shows.  

 `SELECT * FROM SMS_Package AS Pack`  

 `INNER JOIN SMS_Program AS Prog`  

 `ON Pack.PackageID = Prog.PackageID`  

 The following example shows the __Generic class result of the above query.  

 `Class __Generic`  

 `{`  

 `SMS_Package  Pack;`  

 `SMS_Program  Prog;`  

 `}`  

 For COUNT results, the instance includes a Count property, as the following class shows.  

 `Class __Generic`  

 `{`  

 `uint32  Count;`  

 `}`  

## Actual Class Instance Results  
 The class instances that are returned in a result set contain both system and class properties. However, embedded and lazy properties are not returned.  

 The system properties include those for the specified class and its derived classes. Because not all system properties are relevant to all queries, the value of a particular system property can be `null`.  

 The class properties that are returned depend on whether you specify a property list or the asterisk. If you specify a property list containing one or more class properties, the returned instance contains only the properties in the list. The property list should include the key properties for the class. When you invoke a query that does not specify key properties in the property list, the result set contains incomplete and therefore incorrect values for the system properties, `__Path` and `__Relpath`.  

## See Also  
 [How to Read Lazy Properties Using Managed Code](../../../develop/core/understand/how-to-read-lazy-properties-by-using-managed-code.md)   
 [How to Read Lazy Properties Using WMI](../../../develop/core/understand/how-to-read-lazy-properties-by-using-wmi.md)
