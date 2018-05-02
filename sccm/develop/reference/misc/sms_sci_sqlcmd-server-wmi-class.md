---
title: "SMS_SCI_SQLCmd Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: ea2baeeb-6d74-4c40-9452-0b4ae7b4b961
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_SCI_SQLCmd Server WMI Class
The `SMS_SCI_SQLCmd` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that defines a Structured Query Language (SQL) command to be run periodically directly in the SQL Server database.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SCI_SQLCmd : SMS_SiteControlItem   
{  
     DateTime BeginTime;  
     UInt32 DaysOfWeek;  
     UInt32 FileType;  
     String ItemName;  
     String ItemType;  
     DateTime LatestBeginTime;  
     String LogFile;  
     String Name;  
     UInt32 NumRefreshDays;  
     Boolean On;  
     String SiteCode;  
     String SQLCmd;  
};  
```  

## Methods  
 The `SMS_SCI_SQLCmd` class does not define any methods.  

## Properties  
 `BeginTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 Beginning time for execution of the SQL command. The default value is "00000000000000.000000+***". Only the hours and minutes of this property are used.  

 `DaysOfWeek`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [bits]  

 Days of the week on which the command executes. Possible values are listed below.  

|||  
|-|-|  
|0|SUNDAY|  
|1|MONDAY|  
|2|TUESDAY|  
|3|WEDNESDAY|  
|4|THURSDAY|  
|5|FRIDAY|  
|6|SATURDAY|  

 `FileType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key, enumeration:ToSubClass]  

 See [SMS_SiteControlItem Server WMI Class](../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

 `ItemName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 See [SMS_SiteControlItem Server WMI Class](../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

 `ItemType`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 See [SMS_SiteControlItem Server WMI Class](../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

 `LatestBeginTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 Latest beginning time of execution for the SQL command. The default value is "00000000115900.000000+***". Only the hours and minutes of this property are used.  

 `LogFile`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Log file to which to write the output. The default value is "".  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 User-defined name given to the SQL command. The default value is "".  

 `NumRefreshDays`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Number of days between SQL task executions. The default value is 0.  

 `On`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` (default) if the SQL command is activated.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key, SizeLimit("3")]  

 See [SMS_SiteControlItem Server WMI Class](../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

 `SQLCmd`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 SQL command to execute. The default value is "".  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)   
 [SMS_SiteControlItem Server WMI Class](../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md)   
 [SMS_SCI_SQLTask Server WMI Class](../../../develop/reference/core/servers/configure/sms_sci_sqltask-server-wmi-class.md)
