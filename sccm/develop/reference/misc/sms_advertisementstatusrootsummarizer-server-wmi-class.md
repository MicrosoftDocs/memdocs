---
title: "SMS_AdvertisementStatusRootSummarizer Class"
titleSuffix: "Configuration Manager"
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
ms.assetid: c82c9dd3-2d0a-4f9a-a7ee-b99de69963dfsearchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_AdvertisementStatusRootSummarizer Server WMI Class
The `SMS_AdvertisementStatusRootSummarizer` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that list the progress of each advertisement and program as it is advertised and run on the client computers. The reported advertisement status is for all sites in the SMS hierarchy.  

## Syntax  

```  
Class SMS_AdvertisementStatusRootSummarizer : SMS_BaseClass  
{  
      String AdvertisementID;  
      String AdvertisementName;  
      UInt32 AdvertisementsFailed;  
      UInt32 AdvertisementsReceived;  
      String CollectionID;  
      String CollectionName;  
      String DisplaySchedule;  
      DateTime ExpirationTime;  
      String PackageID;  
      String PackageLanguage;  
      String PackageManufacturer;  
      String PackageName;  
      String PackageVersion;  
      DateTime PresentTime;  
      String ProgramName;  
      UInt32 ProgramsFailed;  
      UInt32 ProgramsFailedMIF;  
      UInt32 ProgramsStarted;  
      UInt32 ProgramsSucceeded;  
      UInt32 ProgramsSucceededMIF;  
      String SourceSite;  
      UInt32 TimeEnableFlag;  
};  
```  

## Methods  
 The `SMS_AdvertisementStatusRootSummarizer` class does not define any methods.  

## Properties  
 `AdvertisementID`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: [key]  

 Unique ID that Configuration Manager assigns to each advertisement.  

 `AdvertisementName`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 Name of the advertisement.  

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

 `CollectionID`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 ID of the collection to which the advertisement is targeted.  

 `CollectionName`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 Name of the collection to which the advertisement is targeted.  

 `DisplaySchedule`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: [SizeLimit("16"), key]  

 Interval string that specifies the schedule for which the statistics apply. The statistics are reset to zero each time the schedule elapses. The interval string is generated from an `SMS_ScheduleToken` instance by using the `WriteToString` method.  

 `ExpirationTime`  
 Data type: `DateTime`  

 Access type: Read Only  

 Qualifiers: None  

 Date and time when the advertisement expires and is no longer available to clients. This can be in local or Universal Coordinated Time (UTC), depending on the setting of the `ExpirationTimeIsGMT` property in [SMS_Advertisement Server WMI Class](../../../develop/reference/core/servers/configure/sms_advertisement-server-wmi-class.md).  

 `PackageID`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 ID of the package with which the advertised program is associated.  

 `PackageLanguage`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 Language of the package, such as English or German.  

 `PackageManufacturer`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 Manufacturer of the package.  

 `PackageName`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 Name of the package.  

 `PackageVersion`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 Version of the package.  

 `PresentTime`  
 Data type: `DateTime`  

 Access type: Read Only  

 Qualifiers: None  

 Date and time when the advertisement is presented to the clients. This can be in local or UTC, depending on the setting of the `PresentTimeIsGMT` property in `SMS_Advertisement`.  

 `ProgramName`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 Name of the program (related to `PackageID`) that the advertisement advertises.  

 `ProgramsFailed`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 Total number of users, user groups, or client computers that reported errors while running the advertised program. A program is considered in error when it produces either:  

-   A nonzero exit code.  

-   An install status Management Information Format (MIF) file with a failure-status attribute. This file, if present, overrides an exit code.  

 `ProgramsFailedMIF`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 Programs that have failed relative to the install status MIF file.  

 `ProgramsStarted`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 Total number of users, user groups, or client computers in the site that were able to successfully start running the advertised program.  

 `ProgramsSucceeded`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 Total number of users, user groups, or client computers, or both, that are reporting that the program ran successfully. A program is considered successful when it produces either:  

-   An exit code of zero.  

-   An install status MIF file with a success-status attribute. This file, if present, overrides an exit code.  

 `ProgramsSucceededMIF`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 Programs that have succeeded relative to the install status MIF file.  

 `SourceSite`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Site code of the site where the advertisement originates.  

 `TimeEnableFlag`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 Reserved for future use.  

## Remarks  
 Class qualifiers for this class include:  

-   Read (read-only)  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Software Distribution Server WMI Classes](../../../develop/reference/core/servers/configure/software-distribution-server-wmi-classes.md)
