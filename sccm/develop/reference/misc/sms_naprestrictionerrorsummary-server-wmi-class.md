---
title: "SMS_NAPRestrictionErrorSummary Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 2cda7350-8683-4d7a-9ae0-f9e0ba2993f3
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_NAPRestrictionErrorSummary Server WMI Class
The `SMS_NAPRestrictionErrorSummary` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a Network Access Protection (NAP) restriction error summary.  

> [!NOTE]
>  This data comes from a mixture of discovery and inventory data. By default, inventory runs every week, so this information may be out-of-date.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_NAPRestrictionErrorSummary : SMS_BaseClass  
{  
      String Description;  
      String ErrorCode;  
      UInt32 Last30DaysCount;  
      UInt32 Last7DaysCount;  
      UInt32 LastDayCount;  
      DateTime LastSummaryTime;  
};  
```  

## Methods  
 The `SMS_NAPRestrictionErrorSummary` class does not define any methods.  

## Properties  
 `Description`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Description of the error that occurred while clients were in restriction. See `ErrorCode`.  

 `ErrorCode`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Error that occurred while clients were in restriction.  

 `Last30DaysCount`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The number of computers that reported this error message in the last 30 days.  

 `Last7DaysCount`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The number of computers that reported this error message in the last 7 days.  

 `LastDayCount`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The number of computers that reported this error message in the last 24 hours.  

 `LastSummaryTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 The last date and time when the summary ran.  

## Remarks  
 Class qualifiers for this class include:  

- Read (read-only)  

- Secured  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [NAP Server WMI Classes](../../../develop/reference/misc/nap-server-wmi-classes.md)
