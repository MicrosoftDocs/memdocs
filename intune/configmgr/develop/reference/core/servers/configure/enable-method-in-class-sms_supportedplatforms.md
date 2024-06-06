---
description: The Enable Windows Management Instrumentation (WMI) class method, in Configuration Manager, enables or disables the platforms.
title: Enable Method
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 11e5ed2e-12eb-415d-b98a-a9c1a1306e3f
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Enable Method in Class SMS_SupportedPlatforms
The `Enable` Windows Management Instrumentation (WMI) class method, in Configuration Manager, enables or disables the platforms.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 Enable(  
     boolean IsSupported  
);  
```  

#### Parameters  
 `IsSupported`  
 Data type: `Boolean`  

 Qualifiers: `[in]`  

 `true` if the platforms are enabled. The default value is `true`.  

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Application Server WMI Class](../../../../../develop/reference/apps/sms_application-server-wmi-class.md)   
