---
title: "SmsLsaAccount"
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
ms.assetid: 29ee2324-72c8-48a1-bf37-15c4e03d742esearchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SmsLsaAccount
In System Center Configuration Manager, the `SmsLsaAccount` function determines whether a particular account has administrator credentials, as required by Configuration Manager services. The function also checks the password.  

## Syntax  

```  
int _stdcall SmsLsaAccount(  
      wchar_t* pLocalServer,   
      wchar_t* pAccountDomain,   
      wchar_t* pAccountName,  
      wchar_t* pLocalDomain,  
      int* piFlags  
);   
```  

#### Parameters  
 `pLocalServer`  
 Pointer to Unicode null-terminated string of the local system name with backslashes: \\\MYSYSTEM.  

 `pAccountDomain`  
 Pointer to domain name containing the account being tested.  

 `pAccountName`  
 Pointer to the name of the account being tested.  

 `pLocalDomain`  
 Pointer to the local domain.  

 `piFlags`  
 If the account is found, pointer to combinations of LSAAPI_ADMIN(0x10000) and LSAAPI_SERVICELOGON (0x20000).  

## Return Values  

|Name|Value|  
|----------|-----------|  
|LSAAPI_SUCCESS|0|  
|LSAAPI_ERROR|1|  
|LSAAPI_ACCOUNT_NOT_FOUND|2|  
|LSAAPI_ACCESS_DENIED|5|  

## Remarks  
 For accounts with trusted domains, the `pAccountDomain` and `pLocalServer` parameters should reference the domain and server in question. The trusted domain name, if present, must be removed from the account name. That is, do not submit an account string of type domain\user.  

## Requirements  
 **Windows NT/2000**: Requires Windows NT 4.0 or later.  

 **Version**: Requires SMS 2.0 or later.  

 **Library**: Lsaapi.lib.  

 **Header**: Lsaapi.h.  

## See Also  
 [Configuration Manager Deprecated Functions](../../../develop/reference/misc/deprecated-functions.md)
