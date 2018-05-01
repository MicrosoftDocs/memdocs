---
title: "SMS_ImageServicingSchedule Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 9f1bbe06-85f4-4d62-b073-0ca5c9e45c7a
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_ImageServicingSchedule Server WMI Class
The `SMS_ImageServicingSchedule` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents schedule details for offline servicing image.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ImageServicingSchedule : SMS_BaseClass  
{  
    SInt32 Action;  
    Boolean ContinueOnError;  
    String Description;  
    DateTime LastRunDateTime;  
    String Name;  
    String Schedule;  
    SInt32 ScheduleID;  
    SInt32 State;  
    Boolean UpdateDP;  
};  
```  

## Methods  
 The `SMS_ImageServicingSchedule` class does not define any methods.  

## Properties  
 `Action`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Action for software update.  

|||  
|-|-|  
|0|None.|  
|1|Install software update immediately.|  
|2|Cancel software update installation.|  

 `ContinueOnError`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` to continue to apply software updates to the image when an error occurs. The default value is `false`.  

 This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Description for software update installation schedule.  

 `LastRunDateTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Last run time for software update installation.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Name for software update installation schedule.  

 `Schedule`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Schedule for software update installation schedule.  

 `ScheduleID`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 ID for software update installation schedule.  

 `State`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 State for software update installation at this scheduled time.  

|||  
|-|-|  
|0|None|  
|1|Scheduled|  
|2|Running|  
|3|Succeeded|  
|4|Failed|  

 `UpdateDP`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `True` to specify whether to update distribution points with the image after the software updates are successfully applied. The image might not be available until the image distribution is complete.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
