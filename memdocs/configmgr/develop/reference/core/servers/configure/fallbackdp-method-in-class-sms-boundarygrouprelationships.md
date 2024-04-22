---
description: Learn how to set the fallback time, in minutes, for a distribution point (DP) in Configuration Manager.
title: FallbackDP Method
titleSuffix: Configuration Manager
ms.date: 03/13/2017
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 8debe455-119d-4ef0-a786-f4e76bd61273
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# FallbackDP Method in Class SMS_BoundaryGroupRelationships
 The `FallbackDP` Windows Management Instrumentation (WMI) class method, in Configuration Manager, sets the fallback time, in minutes, for a distribution point (DP). The default value is 120.

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 FallbackDP();  
```  

### Parameters  
 None.

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_BoundaryGroupRelationships Server WMI Class](../../../../../develop/reference/core/servers/configure/sms-boundarygrouprelationships-server-wmi-class.md)
