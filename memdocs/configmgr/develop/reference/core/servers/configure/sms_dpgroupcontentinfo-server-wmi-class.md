---
title: "SMS_DPGroupContentInfo Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: b4b254cb-4bb0-41c5-9510-8e8ecfef5509
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_DPGroupContentInfo Server WMI Class
The `SMS_DPGroupContentInfo` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that describes package information for a given distribution point group.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DPGroupContentInfo : SMS_BaseClass  
{  
    String Description;  
    String GroupID;  
    Boolean IsPredefinedPackage;  
    String Name;  
    String ObjectID;  
    UInt32 ObjectType;  
    UInt32 ObjectTypeID;  
    String PackageID;  
    UInt32 SourceSize;  
};  
```  

## Methods  
 The `SMS_DPGroupContentInfo` class does not define any methods.  

## Properties  
 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Description for the package or application.  

 `GroupID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Unique identifier for the distribution point group.  

 `IsPredefinedPackage`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `True` if this package is a predefined package.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Name of the package or application.  

 `ObjectID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The identifier of the package or the unique identifier of the configuration item.  

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

 Qualifiers: [key]  

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
