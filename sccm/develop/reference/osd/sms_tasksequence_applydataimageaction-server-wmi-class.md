---
title: "SMS_TaskSequence_ApplyDataImageAction Class"
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
ms.assetid: e790f092-2a4d-44ab-89a2-3ffb9102f7fbsearchScope: - ConfigMgr SDK
caps.latest.revision: 12
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_TaskSequence_ApplyDataImageAction Server WMI Class
The `SMS_TaskSequence_ApplyDataImageAction` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a task sequence action that applies an existing data image to a target computer.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_ApplyDataImageAction : SMS_TaskSequence_Action  
{  
      SMS_TaskSequence_Condition Condition;  
      Boolean ContinueOnError;  
      String Description;  
      UInt32 DestinationDisk;  
      String DestinationLogicalDrive;  
      UInt32 DestinationPartition;  
      String DestinationVariable;  
      Boolean Enabled;  
      UInt32 ImageIndex;  
      String ImagePackageID;  
      String Name;  
      String SupportedEnvironment;  
      UInt32 Timeout;  
      Boolean WipeDestinationPartition;  
};  
```  

## Methods  
 The `SMS_TaskSequence_ApplyDataImageAction` class does not define any methods.  

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

 `DestinationDisk`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [CommandLineArg(6), ValueRange("0-99")]  

 Index of the disk to which to apply the image. The index can have a value of 1 through 99. For more information, see Remarks.  

 `DestinationLogicalDrive`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [CommandLineArg(8)]  

 Logical drive letter of the volume to which the image is applied. For more information, see Remarks.  

 `DestinationPartition`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [CommandLineArg(7), RequiredIfNotNull("DestinationDisk"), ValueRange("1-99")]  

 Index of the partition on the target disk specified by `DestinationDisk` to which the image is applied. The index can have a value of 1 through 99. For more information, see Remarks.  

 `DestinationVariable`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [CommandLineArg(9)]  

 Task sequence variable containing the logical drive letter of the volume to which the image is applied. For more information, see the Remarks section later in this topic.  

 `Enabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `ImageIndex`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [Not_Null, ValueRange("1-2147483647"), VariableName("OSDDataImageIndex")]  

 Index of the image in the WIM file applied to the target computer. Possible index values are 1 through 2147483647. For more information, see the note in Remarks.  

 The task sequence variable associated with this property is OSDDataImageIndex. For more information, see the MSDN documentation for [Operating System Deployment Task Sequence Variables](http://go.microsoft.com/fwlink/?LinkId=100711).  

 `ImagePackageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null, CommandLineArg(1), TaskSequencePackage("image")]  

 Package ID of the image applied to the target computer. For more information, see [SMS_ImagePackage Server WMI Class](../../../develop/reference/osd/sms_imagepackage-server-wmi-class.md).  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [AllowedLen("1-100")]  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

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

 `WipeDestinationPartition`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null, VariableName("OSDWipeDestinationPartition")]  

 `true` (default) to wipe the contents of the destination partition before the image is applied.  

 The task sequence variable associated with this property is OSDWipeDestinationPartition. For more information, see the MSDN documentation for [Operating System Deployment Task Sequence Variables](http://go.microsoft.com/fwlink/?LinkId=100711).  

## Remarks  
 Class qualifiers for this class include:  

 [CommandLine("OSDApplyOS.exe /data:%1,%%OSDDataImageIndex%% \<?6: /target:%6,%7>\<?8: /target:%8>\<?9: /target:%%%9%%>"), ActionCategory{"Images,2,5"},ActionUI{"AdminUI.TaskSequenceEditor.dll", "Microsoft.ConfigurationManagement.AdminConsole.TaskSequenceEditor", "ApplyDataImageControl", "TaskSequenceOptionControl"}]  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 The following properties can be set for the target of this task sequence action:  

-   `DestinationDisk`  

-   `DestinationPartition`  

-   `DestinationLogicalDrive`  

-   `DestinationVariable`  

 To install to a specific disk or partition, set `DestinationDisk` and `DestinationPartition` and set the other destination properties to `null`.  

 To install to a logical volume, such as c:\\, set `DestinationLogicalDrive` and set the other properties to `null`.  

 `DestinationVariable` can be set to a task sequence variable that contains the destination in the form of "1,1" to target disk 1, partition 1, or contains "c:" to target a logical volume.  

 Set all the destination properties to `null` to use the "next available" formatted volume as the target.  

> [!NOTE]
>  The value supplied for the `ImageIndex` property can be problematic if your application must range-check the property against a maximum value that is greater than 0x7fffffff (2147483647). In this case, your application cannot use the range qualifier on the property.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Operating System Deployment Server WMI Classes](../../../develop/reference/osd/operating-system-deployment-server-wmi-classes.md)
