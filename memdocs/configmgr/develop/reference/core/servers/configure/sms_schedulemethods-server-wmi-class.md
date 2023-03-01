---
description: Learn how the SMS_ScheduleMethods abstract Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, represents methods for decoding and encoding schedule tokens into and from a Configuration Manager interval string.
title: SMS_ScheduleMethods Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: e7ccc430-34b6-4c65-8933-d13bf8e8202f
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_ScheduleMethods Server WMI Class
The `SMS_ScheduleMethods` abstract Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents methods for decoding and encoding schedule tokens into and from a Configuration Manager interval string.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ScheduleMethods : SMS_BaseClass  
{  
};  
```  

## Methods  
 The following table shows the methods in `SMS_ScheduleMethods`.  

|Method|Description|  
|------------|-----------------|  
|[ReadFromString Method in Class SMS_ScheduleMethods](../../../../../develop/reference/core/servers/configure/readfromstring-method-in-class-sms_schedulemethods.md)|Reads `SMS_ScheduleToken` objects from an interval string.|  
|[WriteToString Method in Class SMS_ScheduleMethods](../../../../../develop/reference/core/servers/configure/writetostring-method-in-class-sms_schedulemethods.md)|Writes `SMS_ScheduleToken` objects to an interval string.|  

## Properties  
 None.  

## Remarks  
 The methods are used in packing and unpacking a schedule token.  

 Class qualifiers for this class include:  

- Abstract  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

  A Configuration Manager interval string is an internal representation of a schedule token, represented by an [SMS_ScheduleToken Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_scheduletoken-server-wmi-class.md) object. Configuration Manager interval strings are not of the same format as WMI interval strings.  

  This class is not used to convert schedule tokens to or from the friendly scheduling strings, for example, "Occurs every 1 day(s) effective 9:27AM Tuesday", found in the Configuration Manager console.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
