---
title: "DeleteDiscoveryData Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 33723e8b-cc0c-4b1d-a2f5-a4629b32eab3
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# DeleteDiscoveryData Method in Class SMS_ADForest
The `DeleteDiscoveryData` Windows Management Instrumentation (WMI) class method, in Configuration Manager, removes information gathered by the forest discovery process.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 DeleteDiscoveryData(  
     UInt32 ForceDelete  
);  
```  

#### Parameters  
 `ForceDelete`  
 Data type: `UInt32`  

 Qualifiers: `[in]`  

 Delete discovered data. Possible values are:  

|||  
|-|-|  
|0|Delete all discovered data excluding forest name and forest properties information.|  
|1|Delete all data including forest name and forest properties information.|  

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_ADForest Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_adforest-server-wmi-class.md)   
 [Discovery Server WMI Classes](../../../../../develop/reference/core/servers/configure/discovery-server-wmi-classes.md)
