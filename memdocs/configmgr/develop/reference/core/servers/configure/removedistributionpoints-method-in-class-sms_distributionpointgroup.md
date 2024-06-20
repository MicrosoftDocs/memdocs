---
title: RemoveDistributionPoints Method
titleSuffix: Configuration Manager
description: The RemoveDistributionPoints WMI class method removes distribution points from this distribution point group.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 9cfacf13-1d30-4a0c-9453-aaa3e9aa677b
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# RemoveDistributionPoints Method in Class SMS_DistributionPointGroup
The `RemoveDistributionPoints` Windows Management Instrumentation (WMI) class method, in Configuration Manager, removes distribution points from this distribution point group.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 RemoveDistributionPoints(  
     string DPNALPath[],  
     boolean RemoveTargetedPackages  
);  
```  

#### Parameters  
 `DPNALPath`  
 Data type: `String` Array  

 Qualifiers: `[in]`  

 Distribution point NAL path.  

 `RemoveTargetedPackages`  
 Data type: `Boolean`  

 Qualifiers: `[in, optional]`  

 The default value is `false`.

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
