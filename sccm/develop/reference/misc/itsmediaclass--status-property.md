---
title: "ITsMediaClass::Status Property"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 8b0c8021-92ca-49fe-b8b4-3f80b1b67c59
author: aczechowski
ms.author: aaroncz
manager: dougeby
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
