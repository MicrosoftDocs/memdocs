---
title: SMS_SiteControlDaySchedule Class
titleSuffix: Configuration Manager
description: An SMS Provider server class, in Configuration Manager, that represents usage information for each hour of the day.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: c8e1830a-2963-4a56-abdc-ab09cf63e3a1
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_SiteControlDaySchedule Server WMI Class
The `SMS_SiteControlDaySchedule` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents usage information for each hour of the day.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SiteControlDaySchedule   
{  
     Boolean Backup[24];  
     UInt32 HourUsage[24];  
     Boolean update;  
};  
```  

## Methods  
 The `SMS_SiteControlDaySchedule` class does not define any methods.  

## Properties  
 `Backup`  
 Data type: `Boolean` Array  

 Access type: Read/Write  

 Qualifiers: None  

 Array containing 24 elements, one for each hour of the day. A value of `true` indicates that the address (sender) embedding `SMS_SiteControlDaySchedule` can be used as a backup.  

 `HourUsage`  
 Data type: `UInt32` Array  

 Access type: Read/Write  

 Array containing 24 elements, one for each hour of the day. This property specifies the type of usage for each hour. Possible values are:  

|Value|Usage type|  
|-|-|  
|1|ALL_PRIORITY|  
|2|ALL_BUT_LOW|  
|3|HIGH_ONLY|  
|4|CLOSED|  

 `update`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if the usage data is saved when the parent address object is saved.  

## Remarks  
 Class qualifiers for this class include:  

- Embedded  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)   
 [SMS_SCI_Address Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sci_address-server-wmi-class.md)
