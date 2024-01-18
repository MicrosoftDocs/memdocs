---
title: SMS_TaskSequencePackageReference Class
titleSuffix: Configuration Manager
description: An SMS Provider server class, in Configuration Manager, that represents a Configuration Manager application or package in the task sequence.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: c0fc7232-fd4e-44f2-8aec-f1ae80d6fc90
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_TaskSequencePackageReference Server WMI Class
The `SMS_TaskSequencePackageReference` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a Configuration Manager application or package in the task sequence.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequencePackageReference : SMS_BaseClass  
{  
    String Description;  
    String ObjectID;  
    String ObjectName;  
    UInt32 ObjectType;  
    String PackageID;  
    String Version;  
};  
```  

## Methods  
 The `SMS_TaskSequencePackageReference` class does not define any methods.  

## Properties  
 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Reference object description.  

 `ObjectID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Reference object ID.  

 `ObjectName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Reference object name.  

 `ObjectType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [enumeration]  

 Reference object type.  

| Value | Object type |
| ----- | ----------- |  
|0|PKG_TYPE_REGULAR|  
|3|PKG_TYPE_DRIVER|  
|5|PKG_TYPE_SWUPDATES|  
|257|PKG_TYPE_IMAGE|  
|258|PKG_TYPE_BOOTIMAGE|  
|259|PKG_TYPE_OSINSTALLIMAGE|  
|512|Application|  

 `PackageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Task sequence package ID.  

 `Version`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Reference object version.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
