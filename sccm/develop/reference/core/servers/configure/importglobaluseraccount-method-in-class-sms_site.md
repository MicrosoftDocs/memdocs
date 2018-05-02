---
title: "ImportGlobalUserAccount Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 3300967b-9080-4b60-901f-e52bc2234f8e
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# ImportGlobalUserAccount Method in Class SMS_Site
The `ImportGlobalUserAccount` Windows Management Instrumentation (WMI) class method, in Configuration Manager, encrypts data that is shared in the hierarchy.   

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 ImportGlobalUserAccount(    
     String UserName,    
     UInt8 Password[]    
);  
```  

#### Parameters  
 `UserName`  
 Data type: `String`  

 Qualifiers: [in]  

 Name of the user account to import.  

 `Password`  
 Data type: `Uint8` Array  

 Qualifiers: [in]  

 Password.   

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md)
