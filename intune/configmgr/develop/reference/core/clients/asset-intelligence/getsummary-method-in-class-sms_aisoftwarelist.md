---
title: GetSummary Method in Class SMS_AISoftwareList
titleSuffix: Configuration Manager
description: A Windows Management Instrumentation class method that returns a summary count of each of the states defined by the SMS_AISoftwareList WMI class records State property.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 6647eed3-567d-47f2-a484-a749b3e37456
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# GetSummary Method in Class SMS_AISoftwareList
The `GetSummary` Windows Management Instrumentation (WMI) class method, in Configuration Manager, returns a summary count of each of the states defined by the `SMS_AISoftwareList` WMI class records `State` property.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 GetSummary(      
     UInt32 Validated,  
     UInt32 UserDefined,  
     UInt32 Pending,  
     UInt32 Updatable,  
     UInt32 Uncategorized  
);  
```  

#### Parameters  
 `Validated`  
 Data type: `UInt32`  

 Qualifiers: [out]  

 Count of software titles with the state `Validated`.  

 `UserDefined`  
 Data type: `UInt32`  

 Qualifiers: [out]  

 Count of software titles with the state `User Defined`.  

 `Pending`  
 Data type: `UInt32`  

 Qualifiers: [out]  

 Count of software titles with the state `Pending`.  

 `Updatable`  
 Data type: `UInt32`  

 Qualifiers: [out]  

 Count of software titles with the state `Updatable`.  

 `Uncategorized`  
 Data type: `UInt32`  

 Qualifiers: [out]  

 Count of software titles with the state `Uncategorized`.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_AISoftwareList Server WMI Class](../../../../../develop/reference/core/clients/asset-intelligence/sms_aisoftwarelist-server-wmi-class.md)
