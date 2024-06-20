---
title: SMS_TaskSequence_CaptureSystemImageAction Class
titleSuffix: Configuration Manager
description: The SMS_TaskSequence_CaptureSystemImageAction class represents a task sequence action that specifies an existing network share and WIM file to use when saving the image.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: e6e66344-a49d-4718-90e8-002e21c8aca5
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_TaskSequence_CaptureSystemImageAction Server WMI Class
The `SMS_TaskSequence_CaptureSystemImageAction` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a task sequence action that specifies an existing network share and WIM file to use when saving the image.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_CaptureSystemImageAction : SMS_TaskSequence_Action  
{  
      String CaptureDestination;  
      String CapturePassword;  
      String CaptureUsername;  
      SMS_TaskSequence_Condition Condition;  
      Boolean ContinueOnError;  
      String Description;  
      Boolean Enabled;  
      String ImageCreator;  
      String ImageDescription;  
      String ImageVersion;  
      String Name;  
      String SupportedEnvironment;  
      UInt32 Timeout;  
};  
```  

## Methods  
 The `SMS_TaskSequence_CaptureSystemImageAction` class does not define any methods.  

## Properties  
 `CaptureDestination`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null, AllowedLen("1-255")]  

 The path where the captured image is saved. This path is overwritten if the file exists already. The path length can be between 1 and 255 characters. This property is required.  

 `CapturePassword`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers:  

 [VariableName("OSDCaptureAccountPassword"), Secret]  

 Password of the account specified by the `CaptureUsername` property.  

 The task sequence variable associated with this property is OSDCaptureAccountPassword. For more information, see [OS deployment task sequence variables](../../../osd/understand/task-sequence-variables.md#OSDCaptureAccountPassword).  

 `CaptureUsername`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [VariableName("OSDCaptureAccount")]  

 A Windows account name that has permissions to the network share where the captured image will be stored, specified by `CaptureDestination`. This name is specified in "domain\username" format. To set this property, you must have write access to the destination folder.  

 The task sequence variable associated with this property is OSDCaptureAccount. For more information, see [OS deployment task sequence variables](../../../osd/understand/task-sequence-variables.md#OSDCaptureAccount).  

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

 `Enabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `ImageCreator`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [AllowedLen("0-255")]  

 Name of the creator of the image. The creation information is stored in the image header. The name length can be between 0 and 255 characters.  

 `ImageDescription`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [AllowedLen("0-255")]  

 Description of the image as supplied by the creator and stored in the image header. The description length can be between 0 and 255 characters.  

 `ImageVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null, AllowedLen("0-32")]  

 Version of the image as supplied by the creator and stored in the image header. The version length can be between 0 and 32 characters. This property is required.  

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

## Remarks  
 Class qualifiers for this class include:  

 [CommandLine("osdcapturesystemimage.exe"),VariablePrefix("OSD"),  

 ActionCategory{"Images,8,5"},ActionUI{"AdminUI.TaskSequenceEditor.dll", "Microsoft.ConfigurationManagement.AdminConsole.TaskSequenceEditor", "CaptureSystemImageControl", "TaskSequenceOptionControl"}, SequenceCategory("OSD")]  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See also

[SMS_TaskSequence_Action server WMI class](sms_tasksequence_action-server-wmi-class.md)
