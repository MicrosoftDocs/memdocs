---
title: InsertMultipleResourceIds Method
titleSuffix: Configuration Manager
description: WMI class method, in Configuration Manager, inserts multiple resource IDs.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: b0f727a9-9325-47f3-91e6-2b589033b37d
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# InsertMultipleResourceIds Method in Class SMS_MDMDeviceEnrollmentManagers
The `InsertMultipleResourceIds` Windows Management Instrumentation (WMI) class method, in Configuration Manager, inserts multiple resource IDs.  

## Syntax  

```  
 sint32 InsertMultipleResourceIds(  
     UInt32 ResourceIds  
);  

```  

#### Parameters  
 `ResourceIds`  
 Data type: `UInt32`  Array  

 Qualifiers: [in]  

 Resource IDs.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_MDMDeviceEnrollmentManagers Server WMI Class](../../../develop/reference/mdm/sms_mdmdeviceenrollmentmanagers-server-wmi-class.md)   
