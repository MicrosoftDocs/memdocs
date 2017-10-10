---
title: "SMS_TaskSequence_PartitionDiskAction Class"
titleSuffix: "Configuration Manager"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: 17c5d9c3-b561-432c-bd69-7277c94f347csearchScope: - ConfigMgr SDK
caps.latest.revision: 11
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_TaskSequence_PartitionDiskAction Server WMI Class
The `SMS_TaskSequence_PartitionDiskAction` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a task sequence action that formats and partitions a specified disk on a target computer.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_PartitionDiskAction : SMS_TaskSequence_Action  
{  
      SMS_TaskSequence_Condition Condition;  
      Boolean ContinueOnError;  
      String Description;  
      UInt32 DiskIndex;  
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
 The `SMS_TaskSequence_PartitionDiskAction` class does not define any methods.  

## Properties  
 `Condition`  
 Data type: `SMS_TaskSequence_Condition`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `ContinueOnError`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [AllowedLen("0-255")]  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `DiskIndex`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [Not_Null]  

 The number of the physical disk to partition and format.  

 `DiskpartBiosCompatibilityMode`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` to set registry keys to disable sector alignment when partitioning the disk for compatibility with the target computer BIOS. The default value is `false`.  

 `DiskType`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Deprecated and should not be used.  

 The type of disk. Possible values are:  

-   DYNAMIC  

-   BASIC  

 `Enabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `GPTBootDisk`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` to create an extensible firmware interface (EFI) partition so that an EFI system can boot from the disk. The default value is `false`. Set this property if `PartitionStyle` is set to GPT.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [AllowedLen("1-100")]  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `Partitions`  
 Data type: `SMS_TaskSequence_PartitionSettings`Array  

 Access type: Read/Write  

 Qualifiers: [Not_null]  

 [SMS_TaskSequence_PartitionSettings Server WMI Class](../../../develop/reference/osd/sms_tasksequence_partitionsettings-server-wmi-class.md) objects representing partition settings.  

 `PartitionStyle`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_null]  

 The partition style. Possible values are:  

-   GPT. GUID partition table format.  

-   MBR. Master boot record format.  

 `SupportedEnvironment`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null:ToInstance]  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 The default value of this property for this task sequence action is WinPE.  

 `Timeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

## Remarks  
 Class qualifiers for this class include:  

 [CommandLine("osddiskpart.exe"),VariablePrefix("OSD"),  

 ActionCategory{"Disks,1,3"},ActionUI{"AdminUI.TaskSequenceEditor.dll", "Microsoft.ConfigurationManagement.AdminConsole.TaskSequenceEditor", "PartitionDiskControl", "TaskSequenceOptionControl"}]  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Operating System Deployment Server WMI Classes](../../../develop/reference/osd/operating-system-deployment-server-wmi-classes.md)   
 [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md)   
 [SMS_TaskSequence_PartitionSettings Server WMI Class](../../../develop/reference/osd/sms_tasksequence_partitionsettings-server-wmi-class.md)
