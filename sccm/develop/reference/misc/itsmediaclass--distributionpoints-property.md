---
title: "ITsMediaClass::DistributionPoints Property"
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
ms.assetid: 49fd39de-09bb-480c-ac7a-87fc8638220asearchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
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
