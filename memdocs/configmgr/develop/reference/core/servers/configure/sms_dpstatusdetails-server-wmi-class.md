---
title: SMS_DPStatusDetails Class
titleSuffix: Configuration Manager
description: In Configuration Manager, the SMS_DPStatusDetails WMI class is an SMS Provider server class that represents distribution point status details.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: a40a11e4-80b8-40d3-b64b-576b4c6ff6e5
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_DPStatusDetails Server WMI Class
The `SMS_DPStatusDetails` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents distribution point status details.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DPStatusDetails : SMS_BaseClass  
{  
    String DPName;  
    SInt64 ID;  
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
    DateTime LastStatusTime;  
    UInt32 MessageCategory;  
    UInt32 MessageFullID;  
    UInt32 MessageID;  
    UInt32 MessageSeverity;  
    UInt32 MessageState;  
    String NALPath;  
    String PackageID;  
    String SiteCode;  
    SInt64 StatusMsgID;  
};  
```  

## Methods  
 The `SMS_DPStatusDetails` class does not define any methods.  

## Properties  
 `DPName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Name of the distribution point.  

 `ID`  
 Data type: `SInt64`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Identifier for the distribution point.  

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

 `LastStatusTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Time of the status message.  

 `MessageCategory`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Status message category.  

 `MessageFullID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Status message full ID with severity.  

 `MessageID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Identifier of the status message.  

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

 Qualifiers: [not_null, read]  

 State of the message.  

|Value|Message state|  
|-|-|  
|1|Success|  
|2|InProgress|  
|3|Error|  

 `NALPath`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 The site's definition of the distribution point's location.

 `PackageID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Identifier for the package.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Source site for this status.  

 `StatusMsgID`  
 Data type: `SInt64`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Status message instance identifier. Link to `SMS_StatusMessage RecordID`.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
