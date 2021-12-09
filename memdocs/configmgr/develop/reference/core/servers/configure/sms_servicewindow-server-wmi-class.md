---
title: "SMS_ServiceWindow Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: a45f7f94-d2c4-4185-9035-ef07b90c7846
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_ServiceWindow Server WMI Class
The `SMS_ServiceWindow` Windows Management Instrumentation (WMI) class, in Configuration Manager, is an SMS Provider server class that represents a window of time, called a maintenance window, in which a program is allowed to execute on a group of computers.  

## Syntax  

```  
Class SMS_ServiceWindow  
{  
      String Description  
      UInt32 Duration  
      Boolean IsEnabled  
      Boolean IsGMT  
      String Name  
      UInt32 RecurrenceType  
      String ServiceWindowID  
      String ServiceWindowSchedules  
      UInt32 ServiceWindowType  
      DateTime StartTime  
}  
```  

## Methods  
 The `SMS_ServiceWindow` class does not define any methods.  

## Properties  
 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The maintenance window description. The default value is "".  

 `Duration`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The duration, in minutes, of the maintenance window. The default value is 5.  

 `IsEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if the maintenance window is enabled. The default value is `false`.  

 `IsGMT`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if the start time is in Universal Coordinated Time (UTC). The default value is `false`.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The maintenance window name. The default value is "".  

 `RecurrenceType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, enumeration]  

 The schedule recurrence. Possible values are listed below. The default value is NONE (1).  

|Value|Recurrence type|  
|-|-|  
|1|NONE|  
|2|DAILY|  
|3|WEEKLY|  
|4|MONTHLYBYWEEKDAY|  
|5|MONTHLYBYDATE|  

 `ServiceWindowID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 A unique ID for the maintenance window. The default value is "".  

 `ServiceWindowSchedules`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The maintenance window schedules in schedule token format. Some valid recurring maintenance window schedules are:  

 0034394008100008 -- every 1 day(s), 1:00:00 AM  

 00343940081A2000 -- every 1 week(s), 1:00:00 AM  

 0034394008284400 -- every 1 month(s), 1:00:00 AM  

 The default value is "".  

> [!NOTE]
>  Creating a schedule token is described in How to Create a Schedule Token.  

 `ServiceWindowType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The maintenance window type. Possible values are listed below. The default value is GENERAL (1).  

|Value|Maintenance window type|  
|-|-|  
|1|GENERAL. General maintenance window.|  
|4|UPDATES. Software Updates maintenance window.|  
|5|OSD. Operating system deployment task sequence maintenance window.|  

 `StartTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 The date and time indicating the start time for the maintenance window.  

## Remarks  
 Class qualifiers for this class include:  

- Embedded  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

  The maintenance window represented by this class has start and end times that can span days. The time span allows you to select certain hours of the week during which the client can execute the targeted programs and software updates. You can define maintenance windows for all Data Center computers by modifying the `Service Window` property of the Data Center collection.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [About maintenance windows](../../../../core/servers/configure/about-maintenance-windows.md)
