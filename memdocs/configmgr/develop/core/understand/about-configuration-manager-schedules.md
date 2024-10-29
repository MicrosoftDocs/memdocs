---
title: Configuration Manager Schedules
description: The SMS_ScheduleToken WMI class is an abstract parent class for the SMS_ST_ schedule token classes that handle the scheduling of events with differing frequencies.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: conceptual
ms.assetid: 030ee838-5a53-45d0-8fd0-d797743d7630
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# About Configuration Manager Schedules
In Configuration Manager, scheduling information is configured by using schedule tokens. The `SMS_ScheduleToken` Windows Management Instrumentation (WMI) class is an abstract parent class for the SMS_ST_ schedule token classes that handle the scheduling of events with differing frequencies such as daily, weekly, and monthly.  

 The `SMS_ScheduleMethods` WMI class, and the corresponding `ReadFromString` and `WriteToString` methods are used to decode and encode schedule tokens into and from an interval string. The interval strings can be used to set schedule properties when defining or modifying objects.  

## Schedule Token Classes Used To Create Different Types of Schedules  
 The following table describes the embedded classes that you can use to provide scheduling information to Configuration Manager components.  

 [SMS_ST_NonRecurring Server WMI Class](../../../develop/reference/core/servers/configure/sms_st_nonrecurring-server-wmi-class.md)  
 The `SMS_ST_NonRecurring` WMI class is used for nonrecurring event scheduling by designating a date and time.  

 [SMS_ST_RecurInterval Server WMI Class](../../../develop/reference/core/servers/configure/sms_st_recurinterval-server-wmi-class.md)  
 The `SMS_ST_RecurInterval` WMI class enables the scheduling of events that occur at regular intervals, such as every 10 days, rather than on designated dates and times.  

 [SMS_ST_RecurMonthlyByDate Server WMI Class](../../../develop/reference/core/servers/configure/sms_st_recurmonthlybydate-server-wmi-class.md)  
 The `SMS_ST_RecurMonthlyByDate` WMI class enables the scheduling of events that occur on designated days at designated monthly intervals, such as every third month on the 15th day of the month.  

 [SMS_ST_RecurMonthlyByWeekday Server WMI Class](../../../develop/reference/core/servers/configure/sms_st_recurmonthlybyweekday-server-wmi-class.md)  
 The `SMS_ST_RecurMonthlyByWeekday` WMI class enables the scheduling of events that occur for a specific day of the week, on a given week of the month, at a given monthly interval. For example, the second Saturday of every month.  

 [SMS_ST_RecurWeekly Server WMI Class](../../../develop/reference/core/servers/configure/sms_st_recurweekly-server-wmi-class.md)  
 The `SMS_ST_RecurWeekly` WMI class enables the scheduling of events that occur at weekly intervals, regardless of the week's sequence in any month, such as every third week on Wednesday.  

## Class and Methods Used to Read or Write Schedule Tokens  
 The following `SMS_ScheduleMethods` WMI class, and the corresponding `ReadFromString` and `WriteToString` methods are used to decode and encode schedule tokens into and from an interval string.  

 [SMS_ScheduleMethods Server WMI Class](../../../develop/reference/core/servers/configure/sms_schedulemethods-server-wmi-class.md)  
 The `SMS_ScheduleMethods` WMI class contains methods for decoding and encoding schedule tokens into and from an interval string.  

 These methods are not used to convert the schedule tokens to or from the friendly scheduling strings found in the Configuration Manager console, such as Occurs every 1 day(s) effective 9:27AM Tuesday. Instead, the methods are used to convert the schedule tokens to or from SMS interval strings (SMS interval strings are not of the same format as the WMI interval strings). SMS interval strings are an internal representation of the schedule token.  

 [ReadFromString Method in Class SMS_ScheduleMethods](../../../develop/reference/core/servers/configure/readfromstring-method-in-class-sms_schedulemethods.md)  
 The `ReadFromString` WMI class method decodes interval strings and places the results into `SMS_ScheduleToken` objects.  

 [WriteToString Method in Class SMS_ScheduleMethods](../../../develop/reference/core/servers/configure/writetostring-method-in-class-sms_schedulemethods.md)  
 The `WriteToString` WMI class method encodes `SMS_ScheduleToken` data into an SMS interval string.  

## See also

- [How to Create a Schedule Token](../../../develop/core/understand/how-to-create-a-schedule-token.md)
- [SMS_ST_NonRecurring Server WMI Class](../../../develop/reference/core/servers/configure/sms_st_nonrecurring-server-wmi-class.md)
- [SMS_ST_RecurInterval Server WMI Class](../../../develop/reference/core/servers/configure/sms_st_recurinterval-server-wmi-class.md)
- [SMS_ST_RecurMonthlyByDate Server WMI Class](../../../develop/reference/core/servers/configure/sms_st_recurmonthlybydate-server-wmi-class.md)
- [SMS_ST_RecurMonthlyByWeekday Server WMI Class](../../../develop/reference/core/servers/configure/sms_st_recurmonthlybyweekday-server-wmi-class.md)
- [SMS_ST_RecurWeekly Server WMI Class](../../../develop/reference/core/servers/configure/sms_st_recurweekly-server-wmi-class.md)
- [SMS_ScheduleMethods Server WMI Class](../../../develop/reference/core/servers/configure/sms_schedulemethods-server-wmi-class.md)
- [ReadFromString Method in Class SMS_ScheduleMethods](../../../develop/reference/core/servers/configure/readfromstring-method-in-class-sms_schedulemethods.md)
- [WriteToString Method in Class SMS_ScheduleMethods](../../../develop/reference/core/servers/configure/writetostring-method-in-class-sms_schedulemethods.md)
- [Microsoft.ConfigurationManagement.Messaging.Framework.Scheduler namespace](/previous-versions/system-center/developer/mt746124\(v=cmsdk.12\))
