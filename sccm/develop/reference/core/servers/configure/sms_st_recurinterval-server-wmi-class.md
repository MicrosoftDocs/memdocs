---
title: "SMS_ST_RecurInterval Class"
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
ms.assetid: 1d3d70ee-36b2-41a7-b0a6-2a55f63aed0bsearchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_ST_RecurInterval Server WMI Class
The `SMS_ST_RecurInterval` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in System Center Configuration Manager, that represents a schedule token for events that occur at regular intervals, for example, every 10 days.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ST_RecurInterval : SMS_ScheduleToken  
{  
      UInt32 DayDuration;  
      UInt32 DaySpan;  
      UInt32 HourDuration;  
      UInt32 HourSpan;  
      Boolean IsGMT;  
      UInt32 MinuteDuration;  
      UInt32 MinuteSpan;  
      DateTime StartTime;  
};  
```  

## Methods  
 The `SMS_ST_RecurInterval` class does not define any methods.  

## Properties  
 `DayDuration`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_ScheduleToken Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_scheduletoken-server-wmi-class.md).  

 `DaySpan`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [Range("0-31")]  

 Number of days spanning schedule intervals. Allowable values are in the range 0-31. The default value is 0.  

 `HourDuration`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [Range("0-23")]  

 See [SMS_ScheduleToken Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_scheduletoken-server-wmi-class.md).  

 `HourSpan`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [Range("0-23")]  

 Number of hours spanning schedule intervals. Allowable values are in the range 0-23. The default value is 0.  

 `IsGMT`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_ScheduleToken Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_scheduletoken-server-wmi-class.md).  

 `MinuteDuration`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [Range("0-59")]  

 See [SMS_ScheduleToken Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_scheduletoken-server-wmi-class.md).  

 `MinuteSpan`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [Range("0-59")]  

 Number of minutes spanning schedule intervals. Allowable values are in the range 0-59. The default value is 0.  

 `StartTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_ScheduleToken Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_scheduletoken-server-wmi-class.md).  

## Remarks  
 Class qualifiers for this class include:  

-   Embedded  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Scheduling Server WMI Classes](../../../../../develop/reference/core/servers/configure/scheduling-server-wmi-classes.md)   
 [SMS_ScheduleToken Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_scheduletoken-server-wmi-class.md)
