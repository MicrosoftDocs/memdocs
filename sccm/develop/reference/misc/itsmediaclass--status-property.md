---
title: "ITsMediaClass::Status Property"
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
ms.assetid: 8b0c8021-92ca-49fe-b8b4-3f80b1b67c59searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# ITsMediaClass::Status Property
In Configuration Manager, the `Status` property contains the status for asynchronous task sequence media creation.  

## Syntax  

```  
[IDL]  
HRESULT Status([out,retval] VARIANT_BOOL* status);  
```  

#### Parameters  
 `status`  
 Data type: `VARIANT_BOOL`  

 Qualifiers: [out, retval]  

 Pointer to `true` if media creation is complete.  

## Return Values  
 An `HRESULT` code. Possible values include, but are not limited to, the following value.  

 S_OK  
 The method succeeded.  

## Remarks  
 The task sequence media creation methods, for example, [ITsMediaClass::CreateBootMedia Method](../../../develop/reference/misc/itsmediaclass--createbootmedia-method.md), use this property to poll for status values. When the value of the property is 0, the media creation method can proceed to use the [ITsMediaClass::ExitCode Property](../../../develop/reference/misc/itsmediaclass--exitcode-property.md) property to get the correct return value.  

## See Also  
 [ITsMediaClass Interface](../../../develop/reference/misc/itsmediaclass-interface.md)   
 [ITsMediaClass::CreateBootMedia Method](../../../develop/reference/misc/itsmediaclass--createbootmedia-method.md)   
 [ITsMediaClass::ExitCode Property](../../../develop/reference/misc/itsmediaclass--exitcode-property.md)
