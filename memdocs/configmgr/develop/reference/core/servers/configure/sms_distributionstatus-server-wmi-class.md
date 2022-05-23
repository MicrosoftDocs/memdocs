---
description: The SMS_DistributionStatus WMI class is an SMS Provider server class, in Configuration Manager, that represents the status of a package that has been assigned to a distribution point.
title: "SMS_DistributionStatus Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 25f4054e-d371-498f-8feb-c1f1cc8688c0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_DistributionStatus Server WMI Class
The `SMS_DistributionStatus` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the status of a package that has been assigned to a distribution point.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DistributionStatus : SMS_BaseClass  
{  
    UInt32 Assets;  
    DateTime LastUpdateDate;  
    UInt32 MessageCategory;  
    String ObjectID;  
    UInt32 ObjectTypeID;  
    String PackageID;  
    UInt32 Type;  
};  
```  

## Methods  
 The `SMS_DistributionStatus` class does not define any methods.  

## Properties  
 `Assets`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Number of distribution points in this status.  

 `LastUpdateDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Last status update date.  

 `MessageCategory`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Status message category.  

 `ObjectID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 PackageID or ModelName.  

 `ObjectTypeID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, read]  

 Secured object class ID.  

|Value|Object type|  
|-|-|  
|2|SMS_DistributionStatus|  
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

 PackageID.  

 `Type`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, read]  

 Status Type.  

|Value|Status type|  
|-|-|  
|1|Success|  
|2|InProgress|  
|3|Error|  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
