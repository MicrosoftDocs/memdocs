---
title: "SMS_TaskSequence_PartitionSettings Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 0eb0d627-d1c6-4cee-a426-7753dd2f5d74
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_TaskSequence_PartitionSettings Server WMI Class
The `SMS_TaskSequence_PartitionSettings` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that specifies the settings to use when creating and formatting a partition on a hard disk drive.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_PartitionSettings  
{  
      Boolean AssignVolumeLetter;  
      Boolean Bootable;  
      String FileSystem;  
      Boolean QuickFormat;  
      UInt32 Size;  
      String SizeUnits;  
      String Type;  
      String VolumeLetterVariable;  
      String VolumeName;  
};  
```  

## Methods  
 The `SMS_TaskSequence_PartitionSettings` class does not define any methods.  

## Properties  
 `AssignVolumeLetter`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if a volume letter will be assigned to the partition. The default value is `true`.  

 This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.  

 `Bootable`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 `true` to set the partition as the active partition. The default value is `false`.  

 `FileSystem`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 File system to use when formatting the partition. Possible values are:  

-   FAT32  

-   NTFS  

 `QuickFormat`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 `true` to perform a quick format. Set this property to `false` to perform a full format.  

 `Size`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Size of the partition to create. The units are defined by the `SizeUnits` property.  

 `SizeUnits`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Units in which the `Size` property is specified. Possible values are:  

|||  
|-|-|  
|MB|Megabytes|  
|GB|Gigabytes|  
|Percent|Percentage of free space remaining on disk|  

 `Type`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 Type of partition to create. Possible values are:  

-   Primary  

-   Extended  

-   Logical  

-   Hidden  

-   EFI  

-   MSR  

 `VolumeLetterVariable`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of a task sequence variable that receives the drive letter of the newly created partition.  

 `VolumeName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name to assign to the volume when it is formatted.  

## Remarks  
 There are no class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Operating System Deployment Server WMI Classes](../../../develop/reference/osd/operating-system-deployment-server-wmi-classes.md)
