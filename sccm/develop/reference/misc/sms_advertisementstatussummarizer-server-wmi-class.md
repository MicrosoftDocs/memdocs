---
title: "SMS_AdvertisementStatusSummarizer Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: bcb41ff8-561e-4f11-a1dc-e150d6b90855
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_AdvertisementStatusSummarizer Server WMI Class
The `SMS_AdvertisementStatusSummarizer` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that summarizes the progress of each advertisement as it is advertised and run on the client computers for an individual site.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_AdvertisementStatusSummarizer : SMS_BaseClass  
{  
      String AdvertisementID;  
      UInt32 AdvertisementsFailed;  
      UInt32 AdvertisementsReceived;  
      String DisplaySchedule;  
      DateTime LastUpdate;  
      UInt32 ProgramsFailed;  
      UInt32 ProgramsFailedMIF;  
      UInt32 ProgramsStarted;  
      UInt32 ProgramsSucceeded;  
      UInt32 ProgramsSucceededMIF;  
      String SiteCode;  
};  
```  

## Methods  
 The `SMS_AdvertisementStatusSummarizer` class does not define any methods.  

## Properties  
 `AdvertisementID`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: [key]  

 Unique ID that Configuration Manager assigns to each advertisement.  

 `AdvertisementsFailed`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 Total number of users, user groups, or client computers that experienced an error in processing the advertisement or its associated program, or that attempted to run the advertised program but failed before the program could be started.  

 `AdvertisementsReceived`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 Total number of users, user groups, or client computers that are reporting the successful receipt of the advertisement.  

 `DisplaySchedule`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: [SizeLimit("16"), key]  

 The schedule for which the statistics apply. The statistics are reset to zero each time the schedule elapses. The interval string is generated from an [SMS_ScheduleToken Server WMI Class](../../../develop/reference/core/servers/configure/sms_scheduletoken-server-wmi-class.md) object by using the [WriteToString Method in Class SMS_ScheduleMethods](../../../develop/reference/core/servers/configure/writetostring-method-in-class-sms_schedulemethods.md)  

 `LastUpdate`  
 Data type: `DateTime`  

 Access type: Read Only  

 Qualifiers: None  

 Date and time, in Universal Coordinated Time (UTC), when the site reported a change in the status for the advertisement.  

 `ProgramsFailed`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 Total number of users, user groups, or client computers that reported errors while running the advertised program. A program is considered in error when it produces either:  

- A nonzero exit code.  

- An install status Management Information Format (MIF) file with a failure-status attribute. This file, if present, overrides an exit code.  

  `ProgramsFailedMIF`  
  Data type: `UInt32`  

  Access type: Read Only  

  Qualifiers: None  

  Programs failing relative to the install status MIF file.  

  `ProgramsStarted`  
  Data type: `UInt32`  

  Access type: Read Only  

  Qualifiers: None  

  Total number of users, user groups, or client computers in the site that were able to successfully start running the advertised program.  

  `ProgramsSucceeded`  
  Data type: `UInt32`  

  Access type: Read Only  

  Qualifiers: None  

  Total number of users (user groups) or client computers, or both, that are reporting that the advertisement ran successfully. A program is considered successful when it produces either:  

- An exit code of zero.  

- An install status MIF file with a success-status attribute. This file, if present, overrides an exit code.  

  `SiteCode`  
  Data type: `String`  

  Access type: Read Only  

  Qualifiers: [key, SizeLimit("3")]  

  Site code of the site that is offering the advertisement.  

## Remarks  
 Class qualifiers for this class include:  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Software Distribution Server WMI Classes](../../../develop/reference/core/servers/configure/software-distribution-server-wmi-classes.md)
