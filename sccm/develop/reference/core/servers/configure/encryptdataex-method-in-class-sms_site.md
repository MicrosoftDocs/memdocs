---
title: "EncryptDataEx Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 97b54531-f6ab-4e08-81ce-97e6775f5a22
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# EncryptDataEx Method in Class SMS_Site
The `EncryptDataEx` Windows Management Instrumentation (WMI) class method, in Configuration Manager, encrypts data using the specified site server’s public key and returns the encrypted data.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 EncryptDataEx(  
     String SiteCode,  
     String Data,  
     String EncryptedData  
);  
```  

#### Parameters  
 `SiteCode`  
 Data type: `String`  

 Qualifiers: [in]  

 Site where the data can be encrypted.   

 `Data`  
 Data type: `String`  

 Qualifiers: [in]  

 Data to be encrypted.  

 `EncryptedData`  
 Data type: `String`  

 Qualifiers: [out]  

 Data encrypted for the specific site.  

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
