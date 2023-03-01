---
title: SMS_DistributionPointDriveInfo Class
titleSuffix: Configuration Manager
description: The SMS_DistributionPointDriveInfo WMI class is an SMS Provider server class that represents the basic information about the drives on a distribution point site system role.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 325e64e8-86d4-4f92-83f9-ace4630d0a4c
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_DistributionPointDriveInfo Server WMI Class
The `SMS_DistributionPointDriveInfo` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the basic information about the drives on a distribution point site system role.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DistributionPointDriveInfo : SMS_BaseClass  
{  
    SInt64 BytesFree;  
    SInt64 BytesTotal;  
    SInt32 ConttentLibPriority;  
    String Drive;  
    String NALPath;  
    SInt32 ObjectType;  
    SInt32 PercentFree;  
    SInt32 PkgSharePriority;  
    String SiteCode;  
    SInt32 Status;  
};  
```  

## Methods  
 The `SMS_DistributionPointDriveInfo` class does not define any methods.  

## Properties  
 `BytesFree`  
 Data type: `SInt64`  

 Access type: Read/Write  

 Qualifiers: none  

 Amount of free, unused storage space, in kilobytes, for the storage object.  

 `BytesTotal`  
 Data type: `SInt64`  

 Access type: Read/Write  

 Qualifiers: none  

 Maximum amount of storage space, in kilobytes, of the storage object. A negative value indicates that information is currently unavailable.  

 `ConttentLibPriority`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The order of preference for distributing content to this drive when copying packages to the Configuration Manager content library on the distribution point system. Lower values are preferred over higher values.  

 `Drive`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Drive that is used by the distribution point.  

 `NALPath`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Network abstraction layer (NAL) path to the distribution point.  

 `ObjectType`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Object type. Possible values are:  

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

 `PercentFree`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Percentage of free storage space available on the storage object.  

 `PkgSharePriority`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The order of preference for distributing packages to this drive when coping packages to package share location. Lower values are preferred over higher values.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Site code of the role.  

 `Status`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The last returned error code from attempts to copy content to this drive. A status of 0 indicates success.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
