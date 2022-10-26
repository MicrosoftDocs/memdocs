---
title: CreateRelationship method
titleSuffix: Configuration Manager
description: Use this WMI class method to add a user device affinity.
ms.date: 08/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 17717f11-feaa-413c-aeae-948c1492c836
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# CreateRelationship method in class SMS_UserMachineRelationship

The `CreateRelationship` WMI class method creates a relationship between a user and a device.

The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```
sint32 CreateRelationship (  
     uint32 MachineResourceId,  
     string UserAccountName,  
     uint32 SourceId,  
     uint32 TypeId  
);  
```  

## Parameters

 `MachineResourceId`  
 Data type: `UInt32`  

 Qualifiers: `[in]`  

 Unique Configuration Manager-supplied identifier for the resource.  

 `UserAccountName`  
 Data type: `String`  

 Qualifiers: `[in]`  

 User account name. For example, `contoso\jqpublic`.

 `SourceId`  
 Data type: `UInt32`  

 Qualifiers: `[in]`  

 Source object identifier for dependency.  

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

 `TypeId`  
 Data type: `UInt32`  

 Qualifiers: `[in, optional]`  

An array of types for this relationship. For a value of `1`, the **UniqueUserName** is the primary user. If the value is null, they aren't the primary user.

## Return values

 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

### Runtime requirements

For more information, see [Configuration Manager server runtime requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development requirements

For more information, see [Configuration Manager server development requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See also

[SMS_Application server WMI class](../../../../../develop/reference/apps/sms_application-server-wmi-class.md)
