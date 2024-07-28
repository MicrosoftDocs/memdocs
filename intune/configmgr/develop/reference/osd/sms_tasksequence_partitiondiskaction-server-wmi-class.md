---
title: SMS_TaskSequence_PartitionDiskAction class
titleSuffix: Configuration Manager
description: The SMS_TaskSequence_PartitionDiskAction WMI class is an SMS Provider server class in Configuration Manager.
ms.date: 08/11/2020
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 17c5d9c3-b561-432c-bd69-7277c94f347c
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# SMS_TaskSequence_PartitionDiskAction server WMI class

The `SMS_TaskSequence_PartitionDiskAction` WMI class is an SMS Provider server class in Configuration Manager. It represents a task sequence action that formats and partitions a specified disk on a target computer.  

The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```MOF
Class SMS_TaskSequence_PartitionDiskAction : SMS_TaskSequence_Action  
{  
      SMS_TaskSequence_Condition Condition;  
      Boolean ContinueOnError;  
      String Description;  
      UInt32 DiskIndex;  
      String DiskIndexVariable;
      Boolean DiskpartBiosCompatibilityMode;  
      String DiskType;  
      Boolean Enabled;  
      Boolean GPTBootDisk;  
      String Name;  
      SMS_TaskSequence_PartitionSettings Partitions[];  
      String PartitionStyle;  
      String SupportedEnvironment;  
      UInt32 Timeout;  
};  
```  

## Methods

The `SMS_TaskSequence_PartitionDiskAction` class doesn't define any methods.

## Properties

### `Condition`

Data type: `SMS_TaskSequence_Condition`  

Access type: Read/Write  

Qualifiers: None  

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

### `ContinueOnError`

Data type: `Boolean`  

Access type: Read/Write  

Qualifiers: None  

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

### `Description`

Data type: `String`  

Access type: Read/Write  

Qualifiers: `[AllowedLen("0-255")]`

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

### `DiskIndex`

Data type: `UInt32`  

Access type: Read/Write  

Qualifiers: `[Not_Null]`

The number of the physical disk to partition and format.  

### `DiskIndexVariable`

Data type: `String`

Access type: Read/write

Use a task sequence variable to specify the disk to format and partition.

### `DiskpartBiosCompatibilityMode`

Data type: `Boolean`  

Access type: Read/Write  

Qualifiers: None  

Set `true` to disable sector alignment when partitioning the disk for compatibility with the target computer BIOS. The default value is `false`.

### `DiskType`

Data type: `String`  

Access type: Read/Write  

Qualifiers: None  

Deprecated, don't use.

### `Enabled`

Data type: `Boolean`  

Access type: Read/Write  

Qualifiers: None  

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

### `GPTBootDisk`

Data type: `Boolean`  

Access type: Read/Write  

Qualifiers: None  

Set `true` to create an extensible firmware interface (EFI) partition so that an EFI system can boot from the disk. The default value is `false`. Set this property if `PartitionStyle` is set to GPT.

### `Name`

Data type: `String`  

Access type: Read/Write  

Qualifiers: `[AllowedLen("1-100")]`

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

### `Partitions`

Data type: `SMS_TaskSequence_PartitionSettings` array  

Access type: Read/Write  

Qualifiers: `[Not_null]`

For more information on the objects representing partition settings, see [SMS_TaskSequence_PartitionSettings server WMI class](../../../develop/reference/osd/sms_tasksequence_partitionsettings-server-wmi-class.md).

### `PartitionStyle`

Data type: `String`  

Access type: Read/Write  

Qualifiers: `[Not_null]`

The partition style. Possible values are:  

- `GPT`: GUID partition table format.  

- `MBR`: Master boot record format.  

### `SupportedEnvironment`

Data type: `String`  

Access type: Read/Write  

Qualifiers: `[Not_Null:ToInstance]`

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

The default value of this property for this task sequence action is `WinPE`.  

### `Timeout`

Data type: `UInt32`  

Access type: Read/Write  

Qualifiers: None  

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

## Remarks

Class qualifiers for this class include:  

```
[CommandLine("osddiskpart.exe"),VariablePrefix("OSD"),  

ActionCategory{"Disks,1,3"},ActionUI{"AdminUI.TaskSequenceEditor.dll", "Microsoft.ConfigurationManagement.AdminConsole.TaskSequenceEditor", "PartitionDiskControl", "TaskSequenceOptionControl"}]  
```

For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager class and property qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).

## Requirements

### Runtime requirements

For more information, see [Configuration Manager server runtime requirements](../../../develop/core/reqs/server-runtime-requirements.md).

### Development requirements

For more information, see [Configuration Manager server development requirements](../../../develop/core/reqs/server-development-requirements.md).

## See also

- [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md)

- [SMS_TaskSequence_PartitionSettings server WMI class](../../../develop/reference/osd/sms_tasksequence_partitionsettings-server-wmi-class.md)
