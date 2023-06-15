---
title: SMS_DPContentInfo Class
description: Learn how to use the SMS_DPContentInfo class in Configuration Manager to describe package information for a given distribution point.
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 95e54f24-0e0e-4b64-88ae-572393c964ad
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_DPContentInfo Server WMI Class
The `SMS_DPContentInfo` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that describes package information for a given distribution point.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DPContentInfo : SMS_BaseClass  
{  
    String Description;  
    Boolean IsPredefinedPackage;  
    String NALPath;  
    String Name;  
    String ObjectID;  
    UInt32 ObjectType;  
    UInt32 ObjectTypeID;  
    String PackageID;  
    UInt32 SourceSize;  
};  
```  

## Methods  
 The `SMS_DPContentInfo` class does not define any methods.  

## Properties  
 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Description for the package or application.  

 `IsPredefinedPackage`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `True` if this package is a predefined package.  

 `NALPath`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Distribution point NALPath.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Name of the package or application.  

 `ObjectID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The identifier of the package or the unique identifier of the configuration item.  

 `ObjectType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, read]  

 Object type.  

|value|Object type|  
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

 `SourceSize`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Source size of the package.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
