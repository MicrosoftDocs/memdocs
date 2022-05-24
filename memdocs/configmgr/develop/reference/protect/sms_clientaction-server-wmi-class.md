---
title: "SMS_ClientAction Class"
description: The SMS_ClientAction Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the client action.
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: a00af5d1-dc44-4361-a927-b3c0a3479f27
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_ClientAction Server WMI Class
The `SMS_ClientAction` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the client action.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ClientAction :    
{  
    UInt32 DwordValue;  
    UInt32 ID;  
    UInt32 LinkedObjectType;  
    String LinkedObjectUniqueID;  
    UInt32 State;  
    String StringValue;  
    String StringValues[];  
    String TargetObjectID;  
    UInt32 TargetObjectType;  
    UInt32 Type;  
    String UniqueID;  
};  
```  

## Methods  
 The `SMS_ClientAction` class does not define any methods.  

## Properties  
 `DwordValue`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The DWORD string value of action.  

 `ID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Identifier for this instance.  

 `LinkedObjectType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The linked object type. Possible values are:  

| Value | Object type |  
| ----- | ----------- |  
|1|AM Policy|  

 `LinkedObjectUniqueID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Unique ID of the linked object.  

 `State`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 State of the client action. Possible values are:  

| Value | Action state |  
| ----- | ------------ |  
|0|Inactive|  
|1|Active|  
|2|Decommission|  

 `StringValue`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The parameter for the client action, for instance the threat name to restore.  

 `StringValues`  
 Data type: `String` Array  

 Access type: Read/Write  

 Qualifiers: none  

 The parameter for the client action (in string array), for instance the excluded scan paths.  

 `TargetObjectID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The unique identifier of the target object.  

 `TargetObjectType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The target object type. Possible values are:  

| Value | Object type |  
| ----- | ----------- |  
|1|Threat|  

 `Type`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Action type. Possible values are:  

| Value | Action type |  
| ----- | ----------- |  
|1|Full Scan|  
|2|Quick Scan|  
|3|Download Definition|  
|4|Evaluate Software Update|  
|5|Exclude Scan Path|  
|6|Override Default Action|  
|7|Restore Quarantine Items|  
|8|Request Policy Now|  

 `UniqueID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Unique identifier for this instance.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
