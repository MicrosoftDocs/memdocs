---
title: "GetSummary Method in Class SMS_AIHardwareRequirements"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 609e3a2c-d852-48b1-9a7b-9648e3a04780
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# GetSummary Method in Class SMS_AIHardwareRequirements
The `GetSummary` Windows Management Instrumentation (WMI) class method, in System Center Configuration Manager, provides a summary count of validated and user-defined state items in the `SMS_AIHardwareRequirements` class.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 GetSummary(      
     UInt32 Validated,  
     UInt32 UserDefined  
);  
```  

#### Parameters  
 `Validated`  
 Data type: `UInt32`  

 Qualifiers: [out]  

 Count of Microsoft-defined items.  

 `UserDefined`  
 Data type: `UInt32`  

 Qualifiers: [out]  

 Count of user-defined items.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_AIHardwareRequirements Server WMI Class](../../../../../develop/reference/core/clients/asset-intelligence/sms_aihardwarerequirements-server-wmi-class.md)
