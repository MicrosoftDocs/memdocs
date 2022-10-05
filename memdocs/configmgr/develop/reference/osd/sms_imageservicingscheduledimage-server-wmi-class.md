---
title: SMS_ImageServicingScheduledImage Class
titleSuffix: Configuration Manager
description: The SMS_ImageServicingScheduledImage WMI class represents all schedules for offline servicing image.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 280d959d-ac8b-4ec6-912d-0af7caa6e840
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_ImageServicingScheduledImage Server WMI Class
The `SMS_ImageServicingScheduledImage` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents all schedules for offline servicing image.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ImageServicingScheduledImage : SMS_BaseClass  
{  
    String ImagePackageID;  
    SInt32 ScheduleID;  
};  
```  

## Methods  
 The `SMS_ImageServicingScheduledImage` class does not define any methods.  

## Properties  
 `ImagePackageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 ID for offline servicing image that is installed on client computer.  

 `ScheduleID`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 ID for offline servicing image installation schedule.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
