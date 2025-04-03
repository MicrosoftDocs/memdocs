---
description: The WriteToString Windows Management Instrumentation (WMI) class method, in Configuration Manager, writes an interval string from objects.
title: WriteToString Method
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 365617e1-9caf-4e90-99be-f486bcbb23ff
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# WriteToString Method in Class SMS_ScheduleMethods
The `WriteToString` Windows Management Instrumentation (WMI) class method, in Configuration Manager, writes an interval string from [SMS_ScheduleToken Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_scheduletoken-server-wmi-class.md) objects.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 WriteToString(  
   SMS_ScheduleToken TokenData[],  
   String StringData  
);  
```  

#### Parameters  
 `StringData`  
 Data type: `String`  

 Qualifiers: [out]  

 The interval string (details in table below).  

 `TokenData`  
 Data type: `SMS_ScheduleToken` Array  

 Qualifiers: [in]  

 [SMS_ScheduleToken Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_scheduletoken-server-wmi-class.md) objects.  

```  

The ScheduleToken class uses two DWORDs to store the schedule data.   

Values for the first DWORD laid out as follows:   

  3 3 2 2 2 2 2 2 2 2 2 2 1 1 1 1 1 1 1 1 1 1   
  1 0 9 8 7 6 5 4 3 2 1 0 9 8 7 6 5 4 3 2 1 0 9 8 7 6 5 4 3 2 1 0   
 +-----------+---------+---------+-------+-----------+-----------+   
 |  Start    |  Start  |  Start  | Start |   Start   | Duration  |   
 |  Minute   |  Hour   |  Day    | Month |   Year    | Minutes   |   
 +-----------+---------+---------+-------+-----------+-----------+   

Values for the second DWORD laid out as follows:   

 SCHED_TOKEN_RECUR_NONE   

  3 3 2 2 2 2 2 2 2 2 2 2 1 1 1 1 1 1 1 1 1 1   
  1 0 9 8 7 6 5 4 3 2 1 0 9 8 7 6 5 4 3 2 1 0 9 8 7 6 5 4 3 2 1 0   
 +---------+---------+-----+-------------------------------------+   
 | Duration| Duration|Flags|           Unused                  |U|   
 | Hours   | Days    |     |                                   |T|   
 |         |         |     |                                   |C|   
 +---------+---------+-----+-------------------------------------+   

 SCHED_TOKEN_RECUR_INTERVAL   

  3 3 2 2 2 2 2 2 2 2 2 2 1 1 1 1 1 1 1 1 1 1   
  1 0 9 8 7 6 5 4 3 2 1 0 9 8 7 6 5 4 3 2 1 0 9 8 7 6 5 4 3 2 1 0   
 +---------+---------+-----+-----------+---------+---------+-----+   
 | Duration| Duration|Flags|  Num of   |  Num of |  Num of |   |U|   
 | Hours   | Days    |     |  Minutes  |  Hours  |  Days   |   |T|   
 |         |         |     |           |         |         |   |C|   
 +---------+---------+-----+-------------------------------------+   

 SCHED_TOKEN_RECUR_WEEKLY   

  3 3 2 2 2 2 2 2 2 2 2 2 1 1 1 1 1 1 1 1 1 1   
  1 0 9 8 7 6 5 4 3 2 1 0 9 8 7 6 5 4 3 2 1 0 9 8 7 6 5 4 3 2 1 0   
 +---------+---------+-----+-----+-----+-------------------------+   
 | Duration| Duration|Flags| Week|# of |       Unused          |U|   
 | Hours   | Days    |     | Day |Weeks|                       |T|   
 |         |         |     |     |     |                       |C|   
 +---------+---------+-----+-------------------------------------+   

 SCHED_TOKEN_RECUR_MONTHLY_BY_WEEKDAY   

  3 3 2 2 2 2 2 2 2 2 2 2 1 1 1 1 1 1 1 1 1 1   
  1 0 9 8 7 6 5 4 3 2 1 0 9 8 7 6 5 4 3 2 1 0 9 8 7 6 5 4 3 2 1 0   
 +---------+---------+-----+-----+-------+-----+-----------------+   
 | Duration| Duration|Flags| Week|Num of |Week |     Unused    |U|   
 | Hours   | Days    |     | Day |months |Order|               |T|   
 |         |         |     |     |       |     |               |C|   
 +---------+---------+-----+-------------------------------------+   

 SCHED_TOKEN_RECUR_MONTHLY_BY_DATE   

  3 3 2 2 2 2 2 2 2 2 2 2 1 1 1 1 1 1 1 1 1 1   
  1 0 9 8 7 6 5 4 3 2 1 0 9 8 7 6 5 4 3 2 1 0 9 8 7 6 5 4 3 2 1 0   
 +---------+---------+-----+---------+-------+-------------------+   
 | Duration| Duration|Flags|   Date  |Num of |       Unused    |U|   
 | Hours   | Days    |     |         |months |                 |T|   
 |         |         |     |         |       |                 |C|   
 +---------+---------+-----+-------------------------------------+  

```  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_ScheduleMethods Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_schedulemethods-server-wmi-class.md)   
 [ReadFromString Method in Class SMS_ScheduleMethods](../../../../../develop/reference/core/servers/configure/readfromstring-method-in-class-sms_schedulemethods.md)
