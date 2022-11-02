---
title: ClearLastNBSAdvForMachines Method
titleSuffix: Configuration Manager
description: The ClearLastNBSAdvForMachines Windows Management Instrumentation class method, in Configuration Manager, clears the last Network Boot advertisement for selected client computers.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: f2a51410-3735-49fe-9024-be458ab3578d
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# ClearLastNBSAdvForMachines Method in Class SMS_Collection
The `ClearLastNBSAdvForMachines` Windows Management Instrumentation (WMI) class method, in Configuration Manager, clears the last Network Boot advertisement for selected client computers.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 ClearLastNBSAdvForMachines(  
   UInt32 ResourceIDs[]  
);  
```  

#### Parameters  
 `ResourceIDs`  
 Data type: `UInt32` Array  

 Qualifiers: [in]  

 IDs of member resources for the client computers.  

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Collection Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md)   
 [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md)
