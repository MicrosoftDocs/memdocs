---
title: "ITsMediaClass::ConnectionOptions Property"
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
ms.assetid: e0f33384-2a25-46a2-8df6-09ec1d495534searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# ITsMediaClass::ConnectionOptions Property
In Configuration Manager, the `ConnectionOptions` property contains a comma-delimited list of name=value pairs to use when establishing the Windows Management Instrumentation (WMI) connection to the SMS Provider.  

## Syntax  

```  
[IDL]  
HRESULT ConnectionOptions([in] BSTR Options);  

HRESULT ConnectionOptions([out,retval] BSTR* Options);  
```  

#### Parameters  
 `Options`  
 Data type: `BSTR`  

 Qualifiers: [in; out, retval]  

 On input, the options to set. On output, this parameter points to the retrieved options. For possible values, see the Remarks section later in this topic.  

## Return Values  
 An `HRESULT` code. Possible values include, but are not limited to, the following value.  

 `S_OK`  
 The method succeeded.  

## Remarks  
 Possible values for this property are:  

-   `Username`  

-   `Domain`  

-   `Password`  

-   `Local`  

-   `Authority`  

 For more information about these options, see the MSDN documentation for the method `IWbemLocator::ConnectServer`.  

## See Also  
 [ITsMediaClass Interface](../../../develop/reference/misc/itsmediaclass-interface.md)
