---
title: "GetPendingComponentList Method"
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
ms.assetid: 826de7bf-3990-49a4-924f-8dc6aa08324esearchScope: - ConfigMgr SDK
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# GetPendingComponentList Method in Class CCM_Application
The `GetPendingComponentList` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that gets the pending component list for an application.   

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 GetPendingComponentList   
{  
    [IN]    String AppDeliveryTypeId  
    [IN]    UInt32 Revision  
    [OUT]   String PendingComponentList  
};  
```  

## Parameters  
 `AppDeliveryTypeId`  
 Data type: `String`  

 Qualifiers: [id("0"), in]  

 Application delivery type identifier.    

 `Revision`  
 Data type: `UInt32`  

 Qualifiers: [id("1"), in]  

 Revision.    

 `PendingComponentList`  
 Data type: `String`  

 Qualifiers: [id("2"), out]  

 Pending component list.    

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
