---
title: SMS_DPGroupDistributionStatusDetails Class
titleSuffix: Configuration Manager
description: The SMS_DPGroupDistributionStatusDetails WMI class is an SMS Provider server class, in Configuration Manager, that represents distribution point status details.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: b991ecb2-3061-45b0-b18a-424425983917
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_DPGroupDistributionStatusDetails Server WMI Class
The `SMS_DPGroupDistributionStatusDetails` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents distribution point status details.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DPGroupDistributionStatusDetails : SMS_BaseClass  
{  
    String ContentName;  
    String DPName;  
    String GroupID;  
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
    UInt32 MessageCategory;  
    UInt32 MessageFullID;  
    UInt32 MessageID;  
    UInt32 MessageSeverity;  
    UInt32 MessageState;  
    String ObjectID;  
    UInt32 ObjectType;  
    UInt32 ObjectTypeID;  
    String PackageID;  
    String SiteCode;  
    UInt64 StatusMsgID;  
    DateTime StatusTime;  
};  
```  

## Methods  
 The `SMS_DPGroupDistributionStatusDetails` class does not define any methods.  

## Properties  
 `ContentName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Name of the package or application.  

 `DPName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Name of the distribution point.  

 `GroupID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Unique identifier for the distribution point group.  

 `ID`  
 Data type: `UInt64`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Status message identifier.  

 `InsString1`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Insertion string for the given status message.  

 `InsString10`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Insertion string for the given status message.  

 `InsString2`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Insertion string for the given status message.  

 `InsString3`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Insertion string for the given status message.  

 `InsString4`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Insertion string for the given status message.  

 `InsString5`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Insertion string for the given status message.  

 `InsString6`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Insertion string for the given status message.  

 `InsString7`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Insertion string for the given status message.  

 `InsString8`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Insertion string for the given status message.  

 `InsString9`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Insertion string for the given status message.  

 `MessageCategory`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Status message category.  

 `MessageFullID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Status message full ID with severity.  

 `MessageID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Identifier for the status message.  

 `MessageSeverity`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, read]  

 Severity of the status message.  

|Value|Status message severity|  
|-|-|  
|0x40000000|Success|  
|0x80000000|Warning|  
|0xC0000000|Error|  

 `MessageState`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, read]  

 State of the message.  

|Value|Message state|  
|-|-|  
|1|Success|  
|2|InProgress|  
|3|Error|  

 `ObjectID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Name of the package or application.  

 `ObjectType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [enumeration]  

 Object type.  

|Value|Object type|  
|-|-|  
|Value|Description|  
|0|PKG_TYPE_REGULAR|  
|3|PKG_TYPE_DRIVER|  
|4|PKG_TYPE_TASK_SEQUENCE|  
|5|PKG_TYPE_SWUPDATES|  
|6|PKG_TYPE_DEVICE_SETTING|  
|8|PKG_CONTENT_PACKAGE|  
|257|PKG_TYPE_IMAGE|  
|258|PKG_TYPE_BOOTIMAGE|  
|259|PKG_TYPE_OSINSTALLIMAGE|  
|512|APPLICATION|  

 `ObjectTypeID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, read]  

 Secured object class ID.  

|Value|Object type|  
|-|-|  
|Value|Description|  
|2|SMS_Package|  
|14|SMS_OperatingSystemInstallPackage|  
|18|SMS_ImagePackage|  
|19|SMS_BootImagePackage|  
|23|SMS_DriverPackage|  
|24|SMS_SoftwareUpdatesPackage|  
|31|SMS_Application|  

 `PackageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Identifier for the package.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Source site for this status.  

 `StatusMsgID`  
 Data type: `UInt64`  

 Access type: Read/Write  

 Qualifiers: none  

 Status message instance identifier.  

 `StatusTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_StatusMessage Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statusmessage-server-wmi-class.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
