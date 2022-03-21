---
title: "SMS_ST_RecurMonthlyByWeekday Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: efed0902-d5cc-40e1-82aa-d6ff893ee44e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_ST_RecurMonthlyByWeekday Server WMI Class
The `SMS_ST_RecurMonthlyByWeekday` WMI class is an SMS Provider server class, in Configuration Manager, that represents a schedule token for events that occur for a specific day of the week, on a given week of the month, at a given monthly interval, for example, the second Saturday of every month.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ST_RecurMonthlyByWeekday : SMS_ScheduleToken  
{  
      UInt32 Day;  
      UInt32 DayDuration;  
      UInt32 ForNumberOfMonths;  
      UInt32 HourDuration;  
      Boolean IsGMT;  
      UInt32 MinuteDuration;  
      DateTime StartTime;  
      UInt32 WeekOrder;  
};  
```  

## Methods  
 The `SMS_ST_RecurMonthlyByWeekday` class does not define any methods.  

## Properties  
 `Day`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Day of the week when the event is scheduled to occur. Possible values are listed below. The default value is 1.  

|Value|Day|  
|-|-|  
|1|SUNDAY|  
|2|MONDAY|  
|3|TUESDAY|  
|4|WEDNESDAY|  
|5|THURSDAY|  
|6|FRIDAY|  
|7|SATURDAY|  

 `DayDuration`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [Range("0-31")]  

 See [SMS_ScheduleToken Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_scheduletoken-server-wmi-class.md).  

 `ForNumberOfMonths`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [Range("1-12")]  

 Number of months for recurrence. Allowable values are in the range 1-12. The default value is 1.  

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

 `StartTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_ScheduleToken Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_scheduletoken-server-wmi-class.md).  

 `WeekOrder`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Week of the month when the event is scheduled to occur. Possible values are listed below. The default value is 0.  

|Value|Week|  
|-|-|  
|0|LAST|  
|1|FIRST|  
|2|SECOND|  
|3|THIRD|  
|4|FOURTH|  

## Remarks  
 Class qualifiers for this class include:  

- Embedded  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_ScheduleToken Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_scheduletoken-server-wmi-class.md)
