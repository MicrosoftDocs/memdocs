---
title: "SMS_ScheduleToken Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 18ad99a2-dd6e-4c1f-b452-464d0b65c8bd
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_ScheduleToken Server WMI Class
The `SMS_ScheduleToken` abstract Windows Management Instrumentation (WMI) class is an SMS Provider server class, in System Center Configuration Manager, that represents a schedule token that is used for the scheduling of events with different frequencies, for example, hourly and daily.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ScheduleToken  
{  
      UInt32 DayDuration;  
      UInt32 HourDuration;  
      Boolean IsGMT;  
      UInt32 MinuteDuration;  
      DateTime StartTime;  
};  
```  

## Methods  
 The `SMS_ScheduleToken` class does not define any methods.  

## Properties  
 `DayDuration`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [Range("0-31")]  

 Number of days during which the scheduled action occurs. Allowable values are in the range 0-31. The default value is 0, indicating that the scheduled action continues indefinitely.  

 `HourDuration`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [Range("0-23")]  

 Number of hours during which the scheduled action occurs. Allowable values are in the range 0-23. The default value is 0, indicating no duration.  

 `IsGMT`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if the time is in Coordinated Universal Time (UTC). The default value is `false`, for local time.  

 `MinuteDuration`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [Range("0-59")]  

 Number of minutes during which the scheduled action occurs. Allowable values are in the range 0-59. The default value is 0, indicating no duration.  

 `StartTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 Date and time when the scheduled action takes place. The default value is "19700201000000.000000+***".  

## Remarks  
 Class qualifiers for this class include:  

- Abstract  

- Embedded  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

  This class is the abstract base class for a number of derived classes representing schedule tokens used for scheduling events with different frequencies, for example, daily. An example of a derived class is [SMS_ST_RecurWeekly Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_st_recurweekly-server-wmi-class.md).  

  This class defines several properties related to duration. Network Discovery is the only System Center Configuration Manager component that uses the duration properties. The following is an example showing the use of classes derived from `SMS_ScheduleToken` with an interval string decoded to make a connection to the site server.  

```  
sInterval = "791378800008000055147880001B200055177880001E2000"  
…  
instance of SMS_ST_NonRecurring  
{  
 DayDuration = 0;  
 HourDuration = 0;  
 IsGMT = FALSE;  
 MinuteDuration = 0;  
 StartTime = "20040719083000.000000+***";  
};  

instance of SMS_ST_RecurWeekly  
{  
 Day = 3;  
 DayDuration = 0;  
 ForNumberOfWeeks = 1;  
 HourDuration = 0;  
 IsGMT = FALSE;  
 MinuteDuration = 0;  
 StartTime = "20040720082100.000000+***";  
};  

instance of SMS_ST_RecurWeekly  
{  
 Day = 6;  
 DayDuration = 0;  
 ForNumberOfWeeks = 1;  
 HourDuration = 0;  
 IsGMT = FALSE;  
 MinuteDuration = 0;  
 StartTime = "20040723082100.000000+***";  
};  
```  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Scheduling Server WMI Classes](../../../../../develop/reference/core/servers/configure/scheduling-server-wmi-classes.md)   
 [SMS_ST_NonRecurring Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_st_nonrecurring-server-wmi-class.md)   
 [SMS_ST_RecurWeekly Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_st_recurweekly-server-wmi-class.md)
