---
title: "GetStatus Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 4c0d8a9a-e9a7-4be9-9691-a86cfb9233e0
author: aczechowski
ms.author: aaroncz
manager: dougeby


---
# GetStatus Method in Class SMS_AIMLSParser
The `GetStatus` Windows Management Instrumentation (WMI) class method, in Configuration Manager, which is used to monitor the status of a previous call to the `Import` method.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 GetStatus(      
     SInt32 Status   
);  
```  

#### Parameters  
 `Status`  
 Data type: `SInt32`  

 Qualifiers: [out]  

 When 0, indicates a successful call to `Import`.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_AIMLSParser Server WMI Class](../../../../../develop/reference/core/clients/asset-intelligence/sms_aimlsparser-server-wmi-class.md)
