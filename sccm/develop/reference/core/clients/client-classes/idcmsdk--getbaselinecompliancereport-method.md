---
title: "IDCMSDK::GetBaselineComplianceReport"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 1f865cb8-b8eb-414d-891a-4028bd0df477
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# IDCMSDK::GetBaselineComplianceReport Method
The `IDCMSDK::GetBaselineComplianceReport` method, in Configuration Manager, retrieves the cached discovery report for the specified configuration item baseline.  

## Syntax  

```  
[IDL]  
HRESULT GetBaselineComplianceReport(  
     LPCWSTR  pszId,  
     LPCWSTR  pszVersion,  
     LPWSTR*  ppszComplianceInfo  
);  
```  

#### Parameters  
 `pszId`  
 Data type: `LPCWSTR`  

 Qualifiers: [in]  

 Pointer to a null-terminated string specifying the ID of the baseline configuration item. An example ID is "ScopeId_6CD81FFE-63C4-4AF6-B50A-0847707628A0/Baseline_780a1633-ba4d-4172-b2b1-583cc733ef56".  

 `pszVersion`  
 Data type: `LPCWSTR`  

 Qualifiers: [in, unique]  

 Pointer to a null-terminated string specifying the baseline configuration item version. If this parameter is set to `null`, the method retrieves the latest version of the baseline configuration item that exists in the client data store.  

 `ppszComplianceInfo`  
 Data type: `LPWSTR`  

 Qualifiers: [out]  

 Pointer to a null-terminated string specifying a report of compliance information for the baseline configuration item.  

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
 [IDCMSDK Interface](../../../../../develop/reference/core/clients/client-classes/idcmsdk-interface.md)
