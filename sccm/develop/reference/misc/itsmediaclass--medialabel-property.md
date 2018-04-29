---
title: "ITsMediaClass::MediaLabel Property"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 25d82de0-4a57-44bc-95f1-999dbaf5d60e
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# ITsMediaClass::MediaLabel Property
In Configuration Manager, the `MediaLabel` property contains a label to identify the task sequence media.  

## Syntax  

```  
[IDL]  
HRESULT MediaLabel([in] BSTR Label);  

HRESULT MediaLabel([out,retval] BSTR* Label);  
```  

#### Parameters  
 `Label`  
 Data type: `BSTR`  

 Qualifiers: [in; out, retval]  

 On input, the media label to set. On output, this parameter points to the retrieved media label.  

## Return Values  
 An `HRESULT` code. Possible values include, but are not limited to, the following value.  

 S_OK  
 The method succeeded.  

## Remarks  
 Windows Explorer uses this label to identify the media when the media is launched.  

## See Also  
 [ITsMediaClass Interface](../../../develop/reference/misc/itsmediaclass-interface.md)
