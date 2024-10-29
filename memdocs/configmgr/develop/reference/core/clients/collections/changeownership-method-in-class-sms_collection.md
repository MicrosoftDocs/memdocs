---
title: ChangeOwnership Method
description: Learn how the ChangeOwnership Windows Management Instrumentation (WMI) class method, in Configuration Manager, changes ownership of the devices.
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 41613023-d4e2-4933-a05a-ba84743c3b2b
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# ChangeOwnership Method in Class SMS_Collection
The `ChangeOwnership` Windows Management Instrumentation (WMI) class method, in Configuration Manager, changes ownership of the devices.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 ChangeOwnership(  
     UInt32 ResourceIDs[],  
     UInt32 DeviceOwner  
     SInt32 ReturnValue  
);  
```  

#### Parameters  
 `ResourceIDs`  
 Data type: `UInt32` Array  

 Qualifiers: [in]  

 IDs of member resources.  

 `DeviceOwner`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 The new owner of the machines.  

| Value | Device owner |
| ----- | ------------ |
|1|Company|  
|2|Personal|  

 `ReturnValue`  
 Data type: `SInt32`  

 Qualifiers: [out]  

 The number of devices that were successfully reassigned ownership.  

> [!IMPORTANT]
>  Even if there is an error, some devices may still get reassigned ownership.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Collection Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md)   
 [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md)
