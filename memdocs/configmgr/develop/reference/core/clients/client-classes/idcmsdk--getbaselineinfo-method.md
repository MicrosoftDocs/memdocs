---
description: "Learn how to retrieve the baseline info for the specified configuration item using IDCMSDK::GetBaselineInfo method."
title: "IDCMSDK::GetBaselineInfo"
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: cfb7ce37-44b3-4cd1-b0f7-16b7c2823c09
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# IDCMSDK::GetBaselineInfo Method
The `IDCMSDK::GetBaselineInfo` method, in Configuration Manager, retrieves information for the specified configuration item baseline.  

## Syntax  

```  
[IDL]  
HRESULT GetBaselineInfo(  
     LPCWSTR  pszId,  
     LPCWSTR  pszVersion,  
     DWORD  dwFlags,  
     ICIInfo**  ppCIInfo  
);  
```  

#### Parameters  
 `pszId`  
 Data type: `LPCWSTR`  

 Qualifiers: [in]  

 Pointer to a null-terminated string specifying the baseline configuration item ID. An example ID is "ScopeId_6CD81FFE-63C4-4AF6-B50A-0847707628A0/Baseline_780a1633-ba4d-4172-b2b1-583cc733ef56".  

 `pszVersion`  
 Data type: `LPCWSTR`  

 Qualifiers: [in, unique]  

 Pointer to a null-terminated string specifying the baseline configuration item version. If this parameter is set to NULL, the method retrieves the latest version of the configuration item that exists in the store. Examples of version strings are "1.00" and "27.00".  

 `dwFlags`  
 Data type: `DWORD`  

 Qualifiers: [in]  

 Flags identifying the configuration item. Possible values are:  

| Value | dwFlags type and descriptions |
| ----- | ----------------------------- |
|0|ciinfoAll. Retrieve all properties. Requires administrator privileges.|  
|1|ciinfoPublic. Retrieve only public properties. The detailed compliance report is not a public property.|  

 `ppCIInfo`  
 Data type: `ICIInfo`  

 Qualifiers: [out]  

 Pointer to a pointer to an [ICIINFO Interface](../../../../../develop/reference/core/clients/client-classes/iciinfo-interface.md) object that represents configuration item information.  

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
 [ICIINFO Interface](../../../../../develop/reference/core/clients/client-classes/iciinfo-interface.md)
