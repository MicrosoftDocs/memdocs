---
title: "ITsMediaClass::DistributionPoints Property"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 49fd39de-09bb-480c-ac7a-87fc8638220a
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# ITsMediaClass::DistributionPoints Property
In Configuration Manager, the `DistributionPoints` property contains a comma-delimited list of distribution points, most preferable first.  

## Syntax  

```  
[IDL]  
HRESULT DistributionPoints([in] BSTR DistributionPoints);  

HRESULT DistributionPoints([out,retval] BSTR* DistributionPoints);  
```  

#### Parameters  
 `DistributionPoints`  
 Data type: `BSTR`  

 Qualifiers: [in; out, retval]  

 On input, the distribution points to set. On output, this parameter points to the retrieved distribution points.  

## Return Values  
 An `HRESULT` code. Possible values include, but are not limited to, the following value.  

 S_OK  
 The method succeeded.  

## Remarks  
 Media creation will look for package content from each of these distribution points, in order.  

## See Also  
 [ITsMediaClass Interface](../../../develop/reference/misc/itsmediaclass-interface.md)
