---
title: "SMS_SCI_SQLTask Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 92b5c389-ae47-4a77-8dbc-181926f23ba8
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_SCI_SQLTask Server WMI Class
The `SMS_SCI_SQLTask` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that defines a SQL task to be run periodically.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SCI_SQLTask : SMS_SiteControlItem   
{  
     DateTime BeginTime;  
     UInt32 DaysOfWeek;  
     UInt32 DeleteOlderThan;  
     String DeviceName;  
     Boolean Enabled;  
     UInt32 FileType;  
     String ItemName;  
     String ItemType;  
     DateTime LatestBeginTime;  
     UInt32 NumRefreshDays;  
     String SiteCode;  
     String TaskName;  
     UInt32 TaskType;  
};  
```  

## Methods  
 The `SMS_SCI_SQLTask` class does not define any methods.  

## Properties  
 `BeginTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 Beginning time for execution of the SQL task. The default value is "00000000000000.000000+***". Only the hours and minutes of this property are used.  

 `DaysOfWeek`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [bits]  

 Days of the week on which the SQL task executes. Possible values are listed below. The default value is 0.  

|||  
|-|-|  
|0|SUNDAY|  
|1|MONDAY|  
|2|TUESDAY|  
|3|WEDNESDAY|  
|4|THURSDAY|  
|5|FRIDAY|  
|6|SATURDAY|  

 `DeleteOlderThan`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Number of days after which records are deleted if the `TaskType` property is set to DELETE. The default value is 0.  

 `DeviceName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Device name if the `TaskType` property is set to BACKUP. The default value is "".  

 `Enabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 TRUE if the task is active.  

 `FileType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, enumeration:ToSubClass]  

 See [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

 `ItemName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 See [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

 `ItemType`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 See [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

 `LatestBeginTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 Latest beginning time of execution for the SQL command. The default value is "00000000000000.000000+***". Only the hours and minutes of this property are used.  

 `NumRefreshDays`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Number of days between task executions. The default value is 0.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key, SizeLimit("3")]  

 See [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

 `TaskName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [StringEnumeration]  

 Configuration Manager-defined task name. Possible values are listed below. The default value is "".  

||  
|-|  
|Backup SMS Site Server|  
|Check Application Title with Inventory Information|  
|Clear Undiscovered Clients|  
|Delete Aged Application Request Data|  
|Delete Aged Application Revisions|  
|Delete Aged Client Operations|  
|Delete Aged Collected Files|  
|Delete Aged Computer Association Data|  
|Delete Aged Delete Detection Data|  
|Delete Aged Device Wipe Record|  
|Delete Aged Discovery Data|  
|Delete Aged Enrolled Devices|  
|Delete Aged EP Health Status History Data|  
|Delete Aged Exchange Partnership|  
|Delete Aged Inventory History|  
|Delete Aged Log Data|  
|Delete Aged Metering Data|  
|Delete Aged Metering Summary Data|  
|Delete Aged Replication Data|  
|Delete Aged Status Messages|  
|Delete Aged Threat Data|  
|Delete Aged User Device Affinity Data|  
|Delete Inactive Client Discovery Data|  
|Delete Obsolete Alerts|  
|Delete Obsolete Client Discovery Data|  
|Delete Obsolete Forest Discovery Sites And Subnets|  
|Evaluate Provisioned AMT Computer Certificates|  
|Monitor Keys|  
|Rebuild Indexes|  
|Summarize File Usage Metering Data|  
|Summarize Installed Software Data|  
|Summarize Monthly Usage Metering Data|  

 `TaskType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Task type. Possible values are listed below. The default value is 0.  

|||  
|-|-|  
|1|BACKUP|  
|2|PERIOD|  
|3|DELETE|  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)   
 [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md)   
 [SMS_SCI_SQLCmd Server WMI Class](../../../../../develop/reference/misc/sms_sci_sqlcmd-server-wmi-class.md)
