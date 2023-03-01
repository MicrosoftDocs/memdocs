---
title: Configuration Manager lazy properties
titleSuffix: Configuration Manager
description: If lazy properties are retrieved during query operations, they have null or zero values.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: bc8b9495-845f-4fae-b4bc-ac94e6f091e4
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Configuration Manager Lazy Properties
Some Configuration Manager object properties are relatively inefficient to retrieve. If these properties were retrieved for many instances in a class (as might be done in a query), the response would be considerably delayed. Such properties are considered lazy properties and are not usually retrieved during query operations. However, if these properties are retrieved during a query, they have `null` or zero values, which might not be the actual value of the property for every instance. Therefore, if you want to get the correct value for lazy properties, you must get each instance individually.  

## See Also  
 [How to Read Lazy Properties Using Managed Code](../../../develop/core/understand/how-to-read-lazy-properties-by-using-managed-code.md)   
 [How to Read Lazy Properties Using WMI](../../../develop/core/understand/how-to-read-lazy-properties-by-using-wmi.md)
