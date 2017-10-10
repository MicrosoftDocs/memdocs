---
title: "SmsGrantAdminRight"
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
ms.assetid: 734723a6-e7c8-43a6-8dbe-a8c11922bf80searchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SmsGrantAdminRight
In System Center Configuration Manager, the `SmsGrantAdminRight` function grants administrator credentials to the specified account.  

## Syntax  

```  
int _stdcall SmsGrantDomainAdminRight(  
      wchar_t* pLocalServer,   
      wchar_t* pAccountDomain,  
      wchar_t* pAccountName,   
      wchar_t* pLocalDomain  
);  
```  

#### Parameters  
 `pLocalServer`  
 Pointer to Unicode null-terminated string of the local system name with backslashes: \\\MYSYSTEM  

 `pAccountDomain`  
 Pointer to the originating domain for the user account.  

 `pAccountName`  
 Pointer to the name of the user account.  

 `pLocalDomain`  
 Pointer to the local domain name.  

## Return Values  

|Name|Value|  
|----------|-----------|  
|LSAAPI_SUCCESS|0|  
|LSAAPI_ERROR|1|  
|LSAAPI_ACCOUNT_NOT_FOUND|2|  
|LSAAPI_ACCESS_DENIED|5|  

## Remarks  
 For accounts with trusted domains, the `pLocalDomain` and `pLocalServer` parameters should reference the domain and server in question. The trusted domain name, if present, must be removed from the account name. That is, do not submit an account string of type domain\user.  

## Requirements  
 **Windows NT/2000**: Requires Windows NT 4.0 or later.  

 **Version**: Requires SMS 2.0 or later.  

 **Library**: Lsaapi.lib.  

 **Header**: Lsaapi.h.  

## See Also  
 [Configuration Manager Deprecated Functions](../../../develop/reference/misc/deprecated-functions.md)
