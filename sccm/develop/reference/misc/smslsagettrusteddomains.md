---
title: "SmsLsaGetTrustedDomains"
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
ms.assetid: f84d52db-7fb3-4e71-892e-f16f6fc2228bsearchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SmsLsaGetTrustedDomains
In System Center Configuration Manager, the `SmsLsaGetTrustedDomains` function gets a list of trusted domain names.  

## Syntax  

```  
int _stdcall SmsLsaGetTrustedDomains(  
      wchar_t* pSystemName,   
      int* pNumDomains,  
      SmsLsaDomainName** pArray  
);  
```  

#### Parameters  
 `pSystemName`  
 Pointer to a Unicode null-terminated string containing the system name: \\\MYSYSTEM  

 `pNumDomains`  
 If this function succeeds, pointer to the number of elements in `pArray`.  

 `pArray`  
 Pointer to a block of memory containing an array of `SmsLsaDomainName` structures.  

## Return Values  
 LSAAPI_SUCCESS or one of the LSAAPI_ERROR codes. A nonzero value is always an error.  

|Name|Value|  
|----------|-----------|  
|LSAAPI_SUCCESS|0|  
|LSAAPI_ERROR|1|  
|LSAAPI_ACCOUNT_NOT_FOUND|2|  
|LSAAPI_ACCOUNT_NOT_ADMIN|3|  
|LSAAPI_ACCOUNT_NOT_SERVICE|4|  
|LSAAPI_ACCESS_DENIED|5|  
|LSAAPI_ACCOUNT_NOT_DOMAINADMIN|6|  

## Remarks  
 This function assigns a global memory pointer to an array of `SmsLsaDomainName` structures. The caller should call `free()` on the pointer when the memory is no longer needed. Do not use the C++ delete operator. The function might return success and a zero count of trusted domains.  

 The `SmsLsaDomainName` structure is defined as follows.  

```  
#define LSAAPI_DOMAINNAME 32  

typedef struct  
{  
    wchar_t Name[LSAAPI_DOMAINNAME];  
}   SmsLsaDomainName;  
```  

## Requirements  
 **Windows NT/2000**: Requires Windows NT 4.0 or later.  

 **Version**: Requires SMS 2.0 or later.  

 **Library**: Lsaapi.lib.  

 **Header**: Lsaapi.h.  

## See Also  
 [Configuration Manager Deprecated Functions](../../../develop/reference/misc/deprecated-functions.md)
