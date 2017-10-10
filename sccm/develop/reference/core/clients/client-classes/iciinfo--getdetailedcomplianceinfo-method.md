---
title: "ICIINFO::GetDetailedComplianceInfo"
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
ms.assetid: cdc74613-5c3d-4eb0-a6fd-d4e4c0ee05f6searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# ICIINFO::GetDetailedComplianceInfo Method
The `ICIINFO::GetDetailedComplianceInfo` method, in Configuration Manager, gets detailed compliance information from the last compliance evaluation run for the configuration item. The string returned by the method contains an XML report from the last evaluation of the configuration item.  

## Syntax  

```  
[IDL]  
HRESULT GetDetailedComplianceInfo(  
     LPWSTR* ppszComplianceInfo  
);  
```  

#### Parameters  
 `ppszComplianceInfo`  
 Data type: `LPWSTR`  

 Qualifiers: [out]  

 Pointer to the detailed compliance information.  

## Return Values  
 An `HRESULT` code. Possible values include, but are not limited to, the following:  

 S_OK  
 The method succeeded. All other return values indicate failure.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [ICIINFO Interface](../../../../../develop/reference/core/clients/client-classes/iciinfo-interface.md)
