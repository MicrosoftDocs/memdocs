---
title: "SMS_ObjectContentExtraInfo Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 48828bbd-5c57-4bdf-8511-71d548039e81
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_ObjectContentExtraInfo Server WMI Class
The `SMS_ObjectContentExtraInfo` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents Application or Package Content Information.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ObjectContentExtraInfo : SMS_BaseClass  
{  
    DateTime DateCreated;  
    String Description;  
    UInt32 FeatureType;  
    DateTime LastUpdateDate;  
    UInt32 NumberErrors;  
    UInt32 NumberInProgress;  
    UInt32 NumberSuccess;  
    UInt32 NumberUnknown;  
    String ObjectID;  
    UInt32 ObjectType;  
    UInt32 ObjectTypeID;  
    String PackageID;  
    String SoftwareName;  
    String SourceSite;  
    UInt32 SourceSize;  
    UInt32 SourceVersion;  
    UInt32 Targeted;  
};  
```  

## Methods  
 The `SMS_ObjectContentExtraInfo` class does not define any methods.  

## Properties  
 `DateCreated`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Package creation time.  

 `Description`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Description for the package or application.  

 `FeatureType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Feature ID property for monitoring. The default value is 8.  

 `LastUpdateDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Package last updated time.  

 `NumberErrors`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Count of failed distribution point.  

 `NumberInProgress`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Count of pending distribution point.  

 `NumberSuccess`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Count of distribution point which was successfully deployed.  

 `NumberUnknown`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Count of distribution point with unknown state.  

 `ObjectID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 PackageID or ModelName.  

 `ObjectType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, read]  

 Object type. Possible values are listed below.  

| Value | Object type |
| ----- | ----------- |
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

 Secured object class ID. Possible values are listed below.  

| Value | Object type ID |
| ----- | -------------- |
|2|SMS_Package|  
|14|SMS_OperatingSystemInstallPackage|  
|18|SMS_ImagePackage|  
|19|SMS_BootImagePackage|  
|21|SMS_DeviceSettingPackage|  
|23|SMS_DriverPackage|  
|24|SMS_SoftwareUpdatesPackage|  
|31|SMS_Application|  

 `PackageID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Package ID.  

 `SoftwareName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Name of the package or application.  

 `SourceSite`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Package source site.  

 `SourceSize`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Package source size.  

 `SourceVersion`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Package source version.  

 `Targeted`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Count of targeted distribution point.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
