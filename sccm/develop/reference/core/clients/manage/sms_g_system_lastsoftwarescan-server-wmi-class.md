---
title: "SMS_G_System_LastSoftwareScan Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 58be5b96-6237-4fe5-aca9-3b665aff201e
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_G_System_LastSoftwareScan Server WMI Class
The `SMS_G_System_LastSoftwareScan` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in System Center Configuration Manager, that represents information about the most recent software inventory scan on the client computer.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_G_System_LastSoftwareScan : SMS_G_System  
{  
     UInt32 ResourceID;  
     DateTime LastScanDate;  
     UInt32 LastScanOpcode;  
     DateTime LastCollectedFileScanDate;  
};  
```  

## Methods  
 The `SMS_G_System_LastSoftwareScan` class does not define any methods.  

## Properties  
 `ResourceID`  
 Data type: **UInt32**  

 Access type: Read/Write  

 Qualifiers: [key]  

 See [SMS_G_System Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system-server-wmi-class.md).  

 `LastCollectedFileScanDate`  
 Data type: **DateTime**  

 Access type: Read/Write  

 Qualifiers: None  

 The date and time of the last scan for collected files.  

 `LastScanDate`  
 Data type: **DateTime**  

 Access type: Read/Write  

 Qualifiers: None  

 Date and time of the most recent System Center Configuration Manager software inventory scan.  

 `LastScanOpcode`  
 Data type: **UInt32**  

 Access type: Read/Write  

 Qualifiers: None  

 Not used.  

## Remarks  
 Class qualifiers for this class include:  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Resource Management Server WMI Classes](../../../../../develop/reference/core/clients/manage/configuration-manager-resource-management-server-wmi-classes.md)   
 [SMS_G_System Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system-server-wmi-class.md)
