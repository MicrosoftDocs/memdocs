---
title: SMS_TaskSequence_InstallUpdateAction Class
titleSuffix: Configuration Manager
description: An SMS Provider server class in configuration Manager. It represents a task sequence that installs software updates on a target computer.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: eff7df77-4356-4357-8a69-149a6d7a55a7
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_TaskSequence_InstallUpdateAction Server WMI Class
The `SMS_TaskSequence_InstallUpdateAction` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a task sequence action that installs software updates on a target computer.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_InstallUpdateAction : SMS_TaskSequence_Action  
{  
      SMS_TaskSequence_Condition Condition;  
      Boolean ContinueOnError;  
      String Description;  
      Boolean Enabled;  
      String Name;  
      String RetryCount;  
      String SupportedEnvironment;  
      String Target;  
      UInt32 Timeout;  
      Boolean UseCache;  
};  
```  

## Methods  
 The `SMS_TaskSequence_InstallUpdateAction` class does not define any methods.  

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

 `Enabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [AllowedLen("1-100")]  

 [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `RetryCount`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [retrycount]  

 The number of retries. The default value is 2.  

 `SupportedEnvironment`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null:ToInstance]  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 The default value of this property for this task sequence action is FullOS.  

 `Target`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null, VariableName("SMSInstallUpdateTarget")]  

 Designator for installing assigned software updates on the target computer. Possible values are:  

- Mandatory. Install all software updates flagged in Configuration Manager as mandatory for the computers targeted by this task sequence action.  

- All. Install all software updates for the computers targeted by this task sequence action.  

  The task sequence variable associated with this property is SMSInstallUpdateTarget. For more information, see [OS deployment task sequence variables](../../../osd/understand/task-sequence-variables.md).  

  `Timeout`  
  Data type: `UInt32`  

  Access type: Read/Write  

  Qualifiers: None  

  See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

  `UseCache`  
  Data type: `Boolean`  

  Access type: Read/Write  

  Qualifiers: [not_null, variablename("SMSTSSoftwareUpdateScanUseCache")]  

  Indicates whether the cache is used. The default value is `true`.  

## Remarks  
 Class qualifiers for this class include:  

 [CommandLine("TSInstallSWUpdate.exe /target:%%SMSInstallUpdateTarget%%"),  

 ActionCategory{"Software,3,2"},ActionUI{"AdminUI.TaskSequenceEditor.dll", "Microsoft.ConfigurationManagement.AdminConsole.TaskSequenceEditor", "InstallSoftwareUpdateControl", "TaskSequenceOptionControl"}]  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md)
