---
title: "SMS_ST_RecurMonthlyByDate Class"
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
ms.assetid: a0f5758c-0195-4f2d-b734-3586f1b1cb46searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_ST_RecurMonthlyByDate Server WMI Class
The `SMS_ST_RecurMonthlyByDate` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in System Center Configuration Manager, that represents a schedule token for events that occur on designated days at designated monthly intervals, for example, every third month on the 15th day of the month.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ST_RecurMonthlyByDate : SMS_ScheduleToken  
{  
      UInt32 DayDuration;  
      UInt32 ForNumberOfMonths;  
      UInt32 HourDuration;  
      Boolean IsGMT;  
      UInt32 MinuteDuration;  
      UInt32 MonthDay;  
      DateTime StartTime;  
};  
```  

## Methods  
 The `SMS_ST_RecurMonthlyByDate` class does not define any methods.  

## Properties  
 `DayDuration`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_ScheduleToken Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_scheduletoken-server-wmi-class.md).  

 `ForNumberOfMonths`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [Range("1-12")]  

 Number of months for the recurrence. Allowable values are in the range 1-12. The default value is 1.  

 `HourDuration`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [Range("0-23")]  

 See [SMS_ScheduleToken Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_scheduletoken-server-wmi-class.md).  

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

 `MonthDay`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [Range("0-31")]  

 Day of the month on which the action occurs. Allowable values are in the range 0-31. The default value is 0, indicating the last day of the month.  

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
