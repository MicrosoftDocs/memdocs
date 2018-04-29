---
title: "SMS_UserMachineRelationship Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 97f57654-c1d1-4a2f-b05f-9f16b22372b8
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_UserMachineRelationship Server WMI Class
The `SMS_UserMachineRelationship` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents …..   

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_UserMachineRelationship : SMS_BaseClass  
{  
    DateTime CreationTime;  
    Boolean IsActive;  
    UInt32 RelationshipResourceID;  
    UInt32 ResourceClientType;  
    UInt32 ResourceID;  
    String ResourceName;  
    UInt32 Sources[];  
    UInt32 Types[];  
    String UniqueUserName;  
};  
```  

## Methods  
 The `SMS_UserMachineRelationship` class defines the following methods.  

|Method|Description|  
|------------|-----------------|  
|[AddSource Method in Class SMS_UserMachineRelationship](../../../../../develop/reference/core/clients/manage/addsource-method-in-class-sms_usermachinerelationship.md)|Adds a source for the relationship between the user and the device.|  
|[AddType Method in Class SMS_UserMachineRelationship](../../../../../develop/reference/core/clients/manage/addtype-method-in-class-sms_usermachinerelationship.md)|Adds a type of the relationship between a user and a device.|  
|[CreateRelationship Method in Class SMS_UserMachineRelationship](../../../../../develop/reference/core/clients/manage/createrelationship-method-in-class-sms_usermachinerelationship.md)|Creates a relationship between a user and a device.|  
|[RemoveSource Method in Class SMS_UserMachineRelationship](../../../../../develop/reference/core/clients/manage/removesource-method-in-class-sms_usermachinerelationship.md)|Removes a source for the relationship between a user and a device.|  
|[RemoveType Method in Class SMS_UserMachineRelationship](../../../../../develop/reference/core/clients/manage/removetype-method-in-class-sms_usermachinerelationship.md)|Removes a type of the relationship between a user and a device.|  

## Properties  
 `CreationTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 CreationTime.   

 `IsActive`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 IsActive.   

 `RelationshipResourceID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 RelationshipResourceID.   

 `ResourceClientType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Client type for computer.  

 `ResourceID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Resource ID for machine.  

 `ResourceName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Resource Name for machine.  

 `Sources`  
 Data type: `UInt32` Array  

 Access type: Read-only  

 Qualifiers: [read]  

 Sources.   

 `Types`  
 Data type: `UInt32` Array  

 Access type: Read-only  

 Qualifiers: [read]  

 Types.    

 `UniqueUserName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 User name in domain\user format.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
