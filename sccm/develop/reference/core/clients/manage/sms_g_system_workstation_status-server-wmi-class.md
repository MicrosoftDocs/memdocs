---
title: "SMS_G_System_WORKSTATION_STATUS Class"
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
ms.assetid: 93fe5065-2e1a-44be-8890-73cf8f0b769fsearchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_G_System_WORKSTATION_STATUS Server WMI Class
The `SMS_G_System_WORKSTATION_STATUS` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in System Center Configuration Manager, that contains information about the last time inventory was collected on a client computer.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_G_System_WORKSTATION_STATUS : SMS_G_System_Current  
{  
     UInt32 GroupID;  
     DateTime LastHardwareScan;  
     String LastReportVersion;  
     UInt32 ResourceID;  
     UInt32 RevisionID;  
     UInt32 SystemDefaultLocaleID;  
     DateTime TimeStamp;  
     UInt32 TimeZoneOffset  
};  
```  

## Methods  
 The `SMS_G_System_WORKSTATION_STATUS` class does not define any methods.  

## Properties  
 `GroupID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 See [SMS_G_System_Current Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system_current-server-wmi-class.md).  

 For this class, the default value of this property is NULL.  

 `LastHardwareScan`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 Date and time when System Center Configuration Manager inventoried the client computer hardware.  

 `LastReportVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Version of the last report.  

 `ResourceID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 See [SMS_G_System_Current Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system_current-server-wmi-class.md).  

 For this class, the default value of this property is `null`.  

 `RevisionID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_G_System_Current Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system_current-server-wmi-class.md).  

 For this class, the default value of this property is `null`.  

 `SystemDefaultLocaleID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 System default locale ID.  

 `TimeStamp`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_G_System_Current Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system_current-server-wmi-class.md).  

 For this class, the default value of this property is `null`.  

 `TimeZoneOffset`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 System default time zone offset.  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## See Also  
 [Hardware Inventory Server WMI Classes](../../../../../develop/reference/core/clients/manage/hardware-inventory-server-wmi-classes.md)   
 [SMS_G_System_Current Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system_current-server-wmi-class.md)
