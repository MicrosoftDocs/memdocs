---
title: "SMS_CH_CheckSummary Class"
titleSuffix: "Configuration Manager"
description: "A provider server class that represents the client check summary."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 21544fbd-26da-4357-a714-69437ca3a7d0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_CH_CheckSummary Server WMI Class
The `SMS_CH_CheckSummary` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the client check summary.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_CH_CheckSummary : SMS_BaseClass  
{  
    String CollectionID;  
    UInt32 CountCurrent;  
    UInt32 CountRemaining;  
    String HealthCheckGUID;  
};  
```  

## Methods  
 The `SMS_CH_CheckSummary` class does not define any methods.  

## Properties  
 `CollectionID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Unique auto-generated ID containing eight characters identifying the collection.  

 `CountCurrent`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Count of the current clients.  

 `CountRemaining`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Count of the remaining clients.  

 `HealthCheckGUID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Health check GUID.   

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
