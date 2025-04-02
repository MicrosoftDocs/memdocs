---
description: Learn how to add the SoftwarePropertiesHash from SoftwareCode and Title in Configuration Manager using the AddSoftwareHashData class method.
title: AddSoftwareHashData Method
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 3a07f56d-e00f-4d46-9f4b-36b99e3a243b
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# AddSoftwareHashData Method in Class SMS_AISoftwareList
The `AddSoftwareHashData` Windows Management Instrumentation (WMI) class method, in Configuration Manager, adds the `SoftwarePropertiesHash` from `SoftwareCode` and `Title`.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 AddSoftwareHashData(   
     UInt32 SoftwareTitles,  
     UInt32 SoftwareHashs   
);  
```  

#### Parameters  
 `SoftwareTitles`  
 Data type: `UInt32`  

 Qualifiers: [out]  

 Count of software titles inserted during this method call.  

 `SoftwareHashs`  
 Data type: `UIn32`  

 Qualifiers: [out]  

 Count of software hashes inserted during this method call.  

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
