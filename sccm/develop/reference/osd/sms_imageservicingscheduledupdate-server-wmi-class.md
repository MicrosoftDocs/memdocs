---
title: "SMS_ImageServicingScheduledUpdate Class"
titleSuffix: "Configuration Manager"
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
ms.assetid: 125f1a05-3bb4-4743-99c0-5ebca68cf324searchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_ImageServicingScheduledUpdate Server WMI Class
The `SMS_ImageServicingScheduledUpdate` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents all schedules for one software update in offline servicing image.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ImageServicingScheduledUpdate : SMS_BaseClass  
{  
    SInt32 ScheduleID;  
    SInt32 UpdateID;  
};  
```  

## Methods  
 The `SMS_ImageServicingScheduledUpdate` class does not define any methods.  

## Properties  
 `ScheduleID`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 ID for software update installation schedule.  

 `UpdateID`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 ID for software update in offline servicing image.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
