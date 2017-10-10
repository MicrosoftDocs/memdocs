---
title: "SMS_ImageUpdateHistory Class"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: ee4170d1-a439-4032-a134-a7c3b34cd9d9searchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_ImageUpdateHistory Server WMI Class
The `SMS_ImageUpdateHistory` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents software update installation history of offline servicing image.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ImageUpdateHistory : SMS_BaseClass  
{  
    SInt32 FailedUpdateID;  
    String ImagePackageID;  
    DateTime RunDateTime;  
    SInt32 ScheduleID;  
    SInt32 Status;  
};  
```  

## Methods  
 The `SMS_ImageUpdateHistory` class does not define any methods.  

## Properties  
 `FailedUpdateID`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 ID for software update that failed to install.  

 `ImagePackageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 ID for offline servicing image.  

 `RunDateTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Last run time for software update.  

 `ScheduleID`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 ID for software update installation schedule.  

 `Status`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Software update installation status.  

|||  
|-|-|  
|2|Success|  
|3|Failed|  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
