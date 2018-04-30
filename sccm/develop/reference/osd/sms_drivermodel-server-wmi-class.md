---
title: "SMS_DriverModel Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 8cba1658-0445-4e9e-a51b-b1c8eba30801
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_DriverModel Server WMI Class
The `SMS_DriverModel` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents driver model information for the specified driver.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DriverModel : SMS_BaseClass  
{  
    UInt32 CI_ID;  
    String CI_UniqueID;  
    String ModelManufacture;  
    String ModelName;  
};  
```  

## Methods  
 The `SMS_DriverModel` class does not define any methods.  

## Properties  
 `CI_ID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Driver configuration item local unique ID.  

 `CI_UniqueID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Driver configuration item global unique ID.  

 `ModelManufacture`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Driver configuration item Model manufacturer.  

 `ModelName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Driver configuration item Model name.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
