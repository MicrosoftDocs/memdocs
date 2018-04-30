---
title: "GetSummary Method in Class SMS_AIMLSParser"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 0c53d501-e55a-4224-bb40-154a16ff3855
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# GetSummary Method in Class SMS_AIMLSParser
The `GetSummary` Windows Management Instrumentation (WMI) class method, in System Center Configuration Manager, retrieves the counts of imported Microsoft License count and non-Microsoft license count.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 GetSummary(      
     UInt32 MVLSCount;   
     UInt32 NonMSLicenseCount;   
);  
```  

#### Parameters  
 `MVLSCount`  
 Data type: `UInt32`  

 Qualifiers: [out]  

 Returns the Microsoft License count.  

 `NonMSLicenseCount`  
 Data type: `UInt32`  

 Qualifiers: [out]  

 Returns the non-Microsoft License count.  

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
