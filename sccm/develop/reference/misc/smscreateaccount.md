---
title: "SmsCreateAccount"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: cbc5c37b-856b-4ca9-957f-1b126e7295c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SmsCreateAccount
In System Center Configuration Manager, the `SmsCreateAccount` function creates an account in the specified domain and with the specified account name and password.  

## Syntax  

```  
int _stdcall SmsCreateAccount(  
      wchar_t* pLocalServer,  
      wchar_t* pAccountDomain,  
      wchar_t* pAccountName,  
      wchar_t* pPassword,  
      wchar_t* pComment,  
      int iFlags  
);  
```  

#### Parameters  
 `pLocalServer`  
 Pointer to Unicode null-terminated string of the local system name with backslashes: \\\MYSYSTEM  

 `pAccountDomain`  
 Pointer to domain name containing the account being tested.  

 `pAccountName`  
 Pointer to the account name being tested.  

 `pPassword`  
 Pointer to the account password.  

 `pComment`  
 Pointer to an account comment.  

 `iFlags`  
 Flags defining options for account creation. Possible values are:  

|||  
|-|-|  
|0x10000|LSAAPI_ADMIN|  
|0x20000|LSAAPI_SERVICELOGON|  
|0x80000|LSAAPI_FORCE|  

## Return Values  

|Name|Value|  
|----------|-----------|  
|LSAAPI_SUCCESS|0|  
|LSAAPI_ERROR|1|  
|LSAAPI_ACCOUNT_NOT_FOUND|2|  
|LSAAPI_ACCESS_DENIED|5|  

## Remarks  
 The account is initially created with user credentials and no service logon credentials. The caller can pass in LSAAPI_ADMIN (0x10000) or LSAAPI_SERVICELOGON (0x20000) or both to create the account with administrator or service logon credentials or both.  

 For accounts with trusted domains, the `pAccountDomain` and `pLocalServer` parameters should reference the domain and server in question. The trusted domain name, if present, must be removed from the account name. That is, do not submit an account string of type domain\user.  

## Requirements  
 **Windows NT/2000**: Requires Windows NT 4.0 or later.  

 **Version**: Requires SMS 2.0 or later.  

 **Library**: Lsaapi.lib.  

 **Header**: Lsaapi.h.  

## See Also  
 [Configuration Manager Deprecated Functions](../../../develop/reference/misc/deprecated-functions.md)
