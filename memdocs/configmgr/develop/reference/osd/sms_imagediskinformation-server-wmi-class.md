---
title: SMS_ImageDiskInformation Class
titleSuffix: Configuration Manager
description: The SMS_ImageDiskInformation WMI class is an SMS Provider server class, in Configuration Manager, that represents all disks and partition information in an operating system image and installer.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 8e189e99-5a5f-41c9-91ee-14a69cc5fe58
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_ImageDiskInformation Server WMI Class
The `SMS_ImageDiskInformation` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents all disks and partition information in an operating system image and operating system installer.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ImageDiskInformation : SMS_BaseClass  
{  
    UInt32 DiskIndex;  
    String DiskStyle;  
    String PackageID;  
    String PartitionFileSystem;  
    UInt32 PartitionIndex;  
    Boolean PartitionIsBoot;  
    String PartitionLabel;  
    SInt64 PartitionOffset;  
    SInt64 PartitionSize;  
    String PartitionStyle;  
    String PartitionType;  
};  
```  

## Methods  
 The `SMS_ImageDiskInformation` class does not define any methods.  

## Properties  
 `DiskIndex`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Disk Index of this image.  

 `DiskStyle`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Disk style.   

 `PackageID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 ID of the image package.  

 `PartitionFileSystem`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Partition file system.  

 `PartitionIndex`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Partition index of this image.  

 `PartitionIsBoot`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 Whether the partition is the boot partition.  

 `PartitionLabel`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Partition label.  

 `PartitionOffset`  
 Data type: `SInt64`  

 Access type: Read-only  

 Qualifiers: [read]  

 Partition offset.  

 `PartitionSize`  
 Data type: `SInt64`  

 Access type: Read-only  

 Qualifiers: [read]  

 Partition size.  

 `PartitionStyle`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Partition style.   

 `PartitionType`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Partition type.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
