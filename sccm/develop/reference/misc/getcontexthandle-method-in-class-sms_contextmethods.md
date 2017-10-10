---
title: "GetContextHandle Method"
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
ms.assetid: 0e9491a9-32cb-4466-8da3-e5b2babc3c3dsearchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# GetContextHandle Method in Class SMS_ContextMethods
The `GetContextHandle` method, in Configuration Manager, stores context objects on the server.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 GetContextHandle(  
      String ContextHandle  
);  
```  

#### Parameters  
 `ContextHandle`  
 Data type: `String`  

 Qualifiers: [out]  

 Context handle that identifies the cached context object on the server.  

## Return Values  
 An `SInt32` data type that indicates 0 for success or non-zero for failure.  

## Remarks  
 Use this method to replace the contents of your context object with the object indicated by the retrieved context handle. Storing context object data on the server saves network bandwidth for client applications that repeatedly call the SMS Provider using a large number of context qualifiers or a large amount of qualifier data.  

 For a complete description of the steps required to use this optimization technique, see the ContextHandle qualifier in [Configuration Manager Context Qualifiers](../../../develop/core/understand/context-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_ContextMethods Class](../../../develop/reference/misc/sms_contextmethods-server-wmi-class.md)   
 [ClearContextHandle](../../../develop/reference/misc/clearcontexthandle-method-in-class-sms_contextmethods.md)
