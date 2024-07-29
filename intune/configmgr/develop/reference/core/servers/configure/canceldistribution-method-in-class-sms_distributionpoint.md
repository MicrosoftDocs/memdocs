---
title: CancelDistribution Method
titleSuffix: Configuration Manager
description: A Windows Management Instrumentation class method that cancels a package distribution.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: bfc44693-3266-461f-988a-886333ac9aaf
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# CancelDistribution Method in Class SMS_DistributionPoint
The `CancelDistribution` Windows Management Instrumentation (WMI) class method, in Configuration Manager, cancels a package distribution. If there's a distribution in-progress for the specified package to the specified distribution point, then calling this method cancels the ongoing distribution and the status of the package distribution will be set to fail for this distribution point.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 CancelDistribution(  
     string PackageId,  
     string NALPath  
);  
```  

#### Parameters  
 `PackageId`  
 Data type: `String`  

 Qualifiers: `[in]`  

 ID for an existing package.  

 `NALPath`  
 Data type: `String`  

 Qualifiers: `[in]`  

 Network abstraction layer (NAL) path to the distribution point server.  

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
