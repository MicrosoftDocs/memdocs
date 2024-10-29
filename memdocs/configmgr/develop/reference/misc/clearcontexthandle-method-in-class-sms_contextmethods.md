---
title: ClearContextHandle Method
titleSuffix: Configuration Manager
description: The ClearContextHandle method clears cached context data associated with the specified context handle.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: c17604c0-fa60-4b94-b42a-07dcfe9a70a7
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# ClearContextHandle Method in Class SMS_ContextMethods
The `ClearContextHandle` method, in Configuration Manager, clears cached context data that is associated with the specified context handle.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 ClearContextHandle(  
   String ContextHandle  
);  
```  

## Parameter  
 `ContextHandle`  
 Data type: `String`  

 Qualifiers: [in]  

 Context handle resulting from a call to the [GetContextHandle Method in Class SMS_ContextMethods](../../../develop/reference/misc/getcontexthandle-method-in-class-sms_contextmethods.md).  

## Return Values  
 An `SInt32` data type that indicates 0 for success, or non-zero for failure.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_ContextMethods Class](../../../develop/reference/misc/sms_contextmethods-server-wmi-class.md)   
 [GetContextHandle Method in Class SMS_ContextMethods](../../../develop/reference/misc/getcontexthandle-method-in-class-sms_contextmethods.md)
