---
title: "Lazy Properties"
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
ms.assetid: bc8b9495-845f-4fae-b4bc-ac94e6f091e4searchScope: - ConfigMgr SDK
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# Configuration Manager Lazy Properties
Some System Center Configuration Manager object properties are relatively inefficient to retrieve. If these properties were retrieved for many instances in a class (as might be done in a query), the response would be considerably delayed. Such properties are considered lazy properties and are not usually retrieved during query operations. However, if these properties are retrieved during a query, they have `null` or zero values, which might not be the actual value of the property for every instance. Therefore, if you want to get the correct value for lazy properties, you must get each instance individually.  

## See Also  
 [How to Read Lazy Properties Using Managed Code](../../../develop/core/understand/how-to-read-lazy-properties-by-using-managed-code.md)   
 [How to Read Lazy Properties Using WMI](../../../develop/core/understand/how-to-read-lazy-properties-by-using-wmi.md)
