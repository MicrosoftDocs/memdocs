---
title: "UpdateVisibilityInEPDashBoard in Class SMS_Collection"
ms.custom: ""
ms.date: "2016-09-20"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "System Center Configuration Manager (current branch)"
ms.assetid: 1adf0ff2-437e-486d-b548-3470b5246641
caps.latest.revision: 4
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# UpdateVisibilityInEPDashBoard in Class SMS_Collection
The `UpdateVisibilityInEPDashBoard` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that shows this collection in the Endpoint Protection dashboard.  
  
 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  
  
## Syntax  
  
```  
uint32 UpdateVisibilityInEPDashBoard   
{  
    [IN]    Boolean Visible  
};  
```  
  
## Parameters  
 `Visible`  
 Data type: `Boolean`  
  
 Qualifiers: [id("0"), in]  
  
 `true` if this collection should show in the Endpoint Protection dashboard.  
  
## Remarks  
  
## Requirements  
  
## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server runtime requirements.md).  
  
## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server development requirements.md).