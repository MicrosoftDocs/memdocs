---
title: "SMS_MeterData Class"
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
ms.assetid: 5e7733bb-3c1f-4b84-a7ff-9c100411b7cbsearchScope: - ConfigMgr SDK
caps.latest.revision: 11
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_MeterData Server WMI Class
The `SMS_MeterData` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in System Center Configuration Manager, that represents captured software metering data.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_MeterData : SMS_BaseClass  
{  
      Boolean EndNotCaptured;  
      DateTime EndTime;  
      UInt32 EndTimeOffset;  
      SInt64 FileID;  
      Boolean InTSSession;  
      String MeterDataID;  
      UInt32 MeteredUserID;  
      Boolean Released;  
      UInt32 ResourceID;  
      Boolean Started;  
      Boolean StartNotCaptured;  
      DateTime StartTime;  
      UInt32 StartTimeOffset;  
      Boolean StillRunning;  
      UInt32 TimeSerial;  
};  
```  

## Methods  
 The `SMS_MeterData` class does not define any methods.  

## Properties  
 `EndNotCaptured`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if the metering agent could not capture the actual end time of the process.  

 `EndTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The date and time, in Universal Coordinated Time (UTC), when the process stopped running, if `StillRunning` is `false`. If it is `true`, `EndTime` represents the time at which the data was reported.  

 `EndTimeOffset`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The offset from UTC, in minutes, of the local time for the client at the time the data was reported.  

 `FileID`  
 Data type: `SInt64`  

 Access type: Read/Write  

 Qualifiers: None  

 ID of the file that was metered. To find the file information, match `FileID` with the ID in [SMS_ProductFileInfo Server WMI Class](../../../develop/reference/apps/sms_productfileinfo-server-wmi-class.md). To find the rules that caused the file to be metered, match `FileID` with the ID in [SMS_MeteredFiles Server WMI Class](../../../develop/reference/apps/sms_meteredfiles-server-wmi-class.md).  

 `InTSSession`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if the file was used in a Terminal Server session. Set the property to `false` if the file was used in a console session.  

 `MeterDataID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Unique ID of a particular instance of a running process on a particular computer. A record with this ID is created every time the client reports on the same instance of a running program.  

 `MeteredUserID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 ID of the Windows user account of the programs user. To find the user name, the application finds the record with the same `MeteredUserID` property in the [SMS_MeteredUser Server WMI Class](../../../develop/reference/apps/sms_metereduser-server-wmi-class.md) class.  

 `Released`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 Internal flag used by the metering system and signifying that the record can be deleted by the Delete Aged Software Metering Data site maintenance task.  

 `ResourceID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 ID of the computer that executed the metered program. To find the computer information, your application finds the record with the same resource ID in the [SMS_R_System Server WMI Class](../../../develop/reference/core/clients/manage/sms_r_system-server-wmi-class.md) class.  

 `Started`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if this is the first record reporting on a particular instance of a running program. If this property is set to `true`, `StartTime` represents the actual time when the program started.  

 `StartNotCaptured`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if the metering agent was not able to capture the actual start time of the process.  

 `StartTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 The date and time, in Universal Coordinated Time (UTC), when the program started, if `Started` is `true`. If it is `false`, `StartTime` is the end time (`EndTime`) of the previous report for this program.  

 `StartTimeOffset`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The offset from UTC, in minutes, of the local time for the client at the time the data was reported.  

 `StillRunning`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if the program is still running. Set this property to `false` if `EndTime` represents the actual end time of the metered program.  

 `TimeSerial`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 A rough ordering of the time used to process the record. Records with a smaller `TimeSerial` value were processed before a record with a larger `TimeSerial` value. This property is not unique across records.  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 Each record represents a report of a running program on a computer. If a program runs over several reporting cycles, there are several instances of `SMS_MeterData` that report on it, all with the same `MeterDataID` value. The time periods specified by `StartTime` and `EndTime` are consecutive and do not overlap. The full period of program execution can be found by the earliest `StartTime` value (where `Started` = 1) and the latest `EndTime` value (where `StillRunning` = 0).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Software Metering Server WMI Classes](../../../develop/reference/apps/software-metering-server-wmi-classes.md)
