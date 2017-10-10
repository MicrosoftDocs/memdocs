---
title: "SMS_DistributionDPStatus Class"
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
ms.assetid: 23765a2f-a6be-45d7-bb8b-ad78bd8dbe22searchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_DistributionDPStatus Server WMI Class
The `SMS_DistributionDPStatus` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a status message reported by a distribution point site system role.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DistributionDPStatus : SMS_BaseClass  
{  
    UInt32 GroupCount;  
    UInt64 ID;  
    String InsString1;  
    String InsString10;  
    String InsString2;  
    String InsString3;  
    String InsString4;  
    String InsString5;  
    String InsString6;  
    String InsString7;  
    String InsString8;  
    String InsString9;  
    Boolean IsPeerDP;  
    UInt64 LastStatusID;  
    DateTime LastUpdateDate;  
    UInt32 MessageCategory;  
    UInt32 MessageFullID;  
    UInt32 MessageID;  
    UInt32 MessageSeverity;  
    UInt32 MessageState;  
    String NalPath;  
    String Name;  
    String ObjectID;  
    UInt32 ObjectTypeID;  
    String PackageID;  
    String ResourceType;  
    String SiteCode;  
};  
```  

## Methods  
 The `SMS_DistributionDPStatus` class does not define any methods.  

## Properties  
 `GroupCount`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The number of distribution point groups.   

 `ID`  
 Data type: `UInt64`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Distribution point ID. This value is stored in the database.  

 `InsString1`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Inserted string 1.  

 `InsString10`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Inserted string 10.  

 `InsString2`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Inserted string 2.  

 `InsString3`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Inserted string 3.  

 `InsString4`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Inserted string 4.  

 `InsString5`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Inserted string 5.  

 `InsString6`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Inserted string 6.  

 `InsString7`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Inserted string 7.  

 `InsString8`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Inserted string 8.  

 `InsString9`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Inserted string 9.  

 `IsPeerDP`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if this is a branch distribution point.  

 `LastStatusID`  
 Data type: `UInt64`  

 Access type: Read-only  

 Qualifiers: [read]  

 Last status ID.  

 `LastUpdateDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Date of the last status update.  

 `MessageCategory`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Status message category.  

 `MessageFullID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Status message full ID with severity.  

 `MessageID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Status message ID.  

 `MessageSeverity`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, read]  

 Status message severity.  

|||  
|-|-|  
|0x40000000|Success|  
|0x80000000|Warning|  
|0xC0000000|Error|  

 `MessageState`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, read]  

 Message state.  

|||  
|-|-|  
|1|Success|  
|2|InProgress|  
|3|Error|  

 `NalPath`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Distribution point NALPath.  

 `Name`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Distribution point name.  

 `ObjectID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 PackageID or ModelName.   

 `ObjectTypeID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, read]  

 Secured object class ID.  

|||  
|-|-|  
|2|SMS_Package|  
|14|SMS_OperatingSystemInstallPackage|  
|18|SMS_ImagePackage|  
|19|SMS_BootImagePackage|  
|23|SMS_DriverPackage|  
|24|SMS_SoftwareUpdatesPackage|  
|31|SMS_Application|  

 `PackageID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Package ID deployed to this distribution point.  

 `ResourceType`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Resource type.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Source site for this status.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
