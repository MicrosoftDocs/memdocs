---
description: The SMS_ST_NonRecurring Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a schedule token for non-recurring events.
title: "SMS_ST_NonRecurring Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: c44ae9b7-6518-41e0-8c8f-3b2802eae34d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_ST_NonRecurring Server WMI Class
The `SMS_ST_NonRecurring` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a schedule token for non-recurring events.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ST_NonRecurring : SMS_ScheduleToken  
{  
      UInt32 DayDuration;  
      UInt32 HourDuration;  
      Boolean IsGMT;  
      UInt32 MinuteDuration;  
      DateTime StartTime;  
};  
```  

## Methods  
 The `SMS_ST_NonRecurring` class does not define any methods.  

## Properties  
 `DayDuration`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [Range("0-31")]  

 See [SMS_ScheduleToken Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_scheduletoken-server-wmi-class.md).  

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
