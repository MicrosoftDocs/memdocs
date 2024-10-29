---
title: SMS_TaskSequence_CaptureWindowsSettingsAction Class
titleSuffix: Configuration Manager
description: The SMS_TaskSequence_CaptureWindowsSettingsAction WMI class that represents a task sequence action that identifies the settings of the Windows operating system to capture from the target computer.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 8f0098c3-161c-41fd-a109-c7d2018c2c17
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_TaskSequence_CaptureWindowsSettingsAction Server WMI Class
The `SMS_TaskSequence_CaptureWindowsSettingsAction` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a task sequence action that identifies the settings of the Windows operating system to capture from the target computer.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_CaptureWindowsSettingsAction : SMS_TaskSequence_Action  
{  
      SMS_TaskSequence_Condition Condition;  
      Boolean ContinueOnError;  
      String Description;  
      Boolean Enabled;  
      Boolean MigrateComputerName;  
      Boolean MigrateRegistrationInfo;  
      Boolean MigrateTimeZone;  
      String Name;  
      String SupportedEnvironment;  
      UInt32 Timeout;  
};  
```  

## Methods  
 The `SMS_TaskSequence_CaptureWindowsSettingsAction` class does not define any methods.  

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

 `MigrateComputerName`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null, VariableName("OSDMigrateComputerName")]  

 `true` (default) to migrate the computer name.  

 The task sequence variable associated with this property is OSDMigrateComputerName. For more information, see [OS deployment task sequence variables](../../../osd/understand/task-sequence-variables.md).  

 `MigrateRegistrationInfo`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null, VariableName("OSDMigrateRegistrationInfo")]  

 `true` (default) to migrate information about the registered owner or organization.  

 The task sequence variable associated with this property is OSDMigrateRegistrationInfo. For more information, see [OS deployment task sequence variables](../../../osd/understand/task-sequence-variables.md).  

 `MigrateTimeZone`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null, VariableName("OSDMigrateTimeZone")]  

 `true` (default) to migrate information about the time zone.  

 The task sequence variable associated with this property is OSDMigrateTimeZone. For more information, see [OS deployment task sequence variables](../../../osd/understand/task-sequence-variables.md).  

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

 `Timeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

## Remarks  
 Class qualifiers for this class include:  

 [CommandLine("osdwinsettings.exe /capture /name:%%OSDMigrateComputerName%% /reginfo:%%OSDMigrateRegistrationInfo%% /timezone:%%OSDMigrateTimeZone%%"),  

 ActionCategory{"Settings,2,7"},ActionUI{"AdminUI.TaskSequenceEditor.dll", "Microsoft.ConfigurationManagement.AdminConsole.TaskSequenceEditor", "CaptureWindowsSettingsControl", "TaskSequenceOptionControl"}]  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See also

[SMS_TaskSequence_Action server WMI class](sms_tasksequence_action-server-wmi-class.md)
