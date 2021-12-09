---
title: SMS_UserMachineRelationship class
titleSuffix: Configuration Manager
description: Use this server WMI class to manage user device affinity.
ms.date: 08/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 97f57654-c1d1-4a2f-b05f-9f16b22372b8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
---

# SMS_UserMachineRelationship server WMI class

The `SMS_UserMachineRelationship` WMI class contains relationships between a device and its primary users.

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
|[AddSource Method in Class SMS_UserMachineRelationship](addsource-method-in-class-sms_usermachinerelationship.md)|Adds a source for the relationship between the user and the device.|  
|[AddType Method in Class SMS_UserMachineRelationship](addtype-method-in-class-sms_usermachinerelationship.md)|Adds a type of the relationship between a user and a device.|  
|[CreateRelationship Method in Class SMS_UserMachineRelationship](createrelationship-method-in-class-sms_usermachinerelationship.md)|Creates a relationship between a user and a device.|  
|[RemoveSource Method in Class SMS_UserMachineRelationship](removesource-method-in-class-sms_usermachinerelationship.md)|Removes a source for the relationship between a user and a device.|  
|[RemoveType Method in Class SMS_UserMachineRelationship](removetype-method-in-class-sms_usermachinerelationship.md)|Removes a type of the relationship between a user and a device.|  

## Properties

 `CreationTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 The time that the relationship was created.

 `IsActive`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 **TRUE** if the relationship is active.

 `RelationshipResourceID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The unique identifier for this relationship.

 `ResourceClientType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Client type for computer.  

 `ResourceID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 The resource ID of the device.

 `ResourceName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 The resource name of the device.

 `Sources`  
 Data type: `UInt32` Array  

 Access type: Read-only  

 Qualifiers: [read]  

An array of sources for this relationship, with one of the following values:

|Value|Name|Description|  
|-|-|-|
|`1`|Self-service portal|The end user enabled the relationship by selecting the option in Software Center.|  
|`2`|Administrator|An administrator created the relationship manually in the console.|  
|`3`|User|Unused/deprecated.|  
|`4`|Usage agent|The threshold of activity triggered a relationship to be created.|  
|`5`|Device management|The user and device were tied together during on-prem MDM enrollment.|  
|`6`|OSD|The user and device were tied together as part of an OS deployment task sequence.|  
|`7`|Fast install|The user/device were tied together temporarily to enable an on-demand install from the catalog if no UDA relationship installed before the Install was triggered.|  
|`8`|Exchange Server connector|The device was provisioned through Exchange ActiveSync.|  
|`9`|Secure usage agent||

 `Types`  
 Data type: `UInt32` Array  

 Access type: Read-only  

 Qualifiers: [read]  

 An array of types for this relationship. For a value of `1`, the **UniqueUserName** is the primary user. If the value is null, they aren't the primary user.

 `UniqueUserName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 User name in domain\user format.

## Remarks  

## Requirements  

### Runtime requirements

For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development requirements

For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
