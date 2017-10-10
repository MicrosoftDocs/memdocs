---
title: "ITsMediaClass::ExitCode Property"
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
ms.assetid: 337178ac-9170-48ac-a249-7a674be459a2searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# ITsMediaClass::ExitCode Property
In Configuration Manager, the `ExitCode` property contains the exit code for asynchronous task sequence media creation.  

## Syntax  

```  
[IDL]  
HRESULT ExitCode([out,retval] long* Result);  
```  

#### Parameters  
 `Result`  
 Data type: `long`  

 Qualifiers: [out, retval]  

 Pointer to the exit code.  

## Return Values  
 An `HRESULT` code. Possible values include, but are not limited to, the following value.  

 S_OK  
 The method succeeded.  

## Remarks  
 The task sequence media creation methods, for example, [ITsMediaClass::CreateBootMedia Method](../../../develop/reference/misc/itsmediaclass--createbootmedia-method.md), use this property to get the correct return value when the [ITsMediaClass::Status Property](../../../develop/reference/misc/itsmediaclass--status-property.md) property is set to 0.  

## See Also  
 [ITsMediaClass Interface](../../../develop/reference/misc/itsmediaclass-interface.md)   
 [ITsMediaClass::CreateBootMedia Method](../../../develop/reference/misc/itsmediaclass--createbootmedia-method.md)   
 [ITsMediaClass::Status Property](../../../develop/reference/misc/itsmediaclass--status-property.md)
