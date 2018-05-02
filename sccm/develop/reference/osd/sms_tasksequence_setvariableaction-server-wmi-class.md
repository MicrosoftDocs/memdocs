---
title: "SMS_TaskSequence_SetVariableAction Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 0fdecda3-7ed0-486f-a3a5-7a339979cad4
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_TaskSequence_SetVariableAction Server WMI Class
The `SMS_TaskSequence_SetVariableAction` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a task sequence action that sets the value of a task sequence environment variable.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_SetVariableAction : SMS_TaskSequence_Action  
{  
      SMS_TaskSequence_Condition Condition;  
      Boolean ContinueOnError;  
      String Description;  
      Boolean Enabled;  
      String Name;  
      String SupportedEnvironment;  
      UInt32 Timeout;  
      String VariableName;  
      String VariableValue;  
};  
```  

## Methods  
 The `SMS_TaskSequence_SetVariableAction` class does not define any methods.  

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

 `VariableName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [CommandLineArg(1), Not_Null, AllowedLen("1-256")]  

 Name of the task sequence environment variable to set. The name length must be between 1 and 256 characters.  

 `VariableValue`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [CommandLineArg(2), Not_Null, AllowedLen("0-4001")]  

 Value of the task sequence environment variable. The value length must be between 0 and 4,001 characters.  

## Remarks  
 Class qualifiers for this class include:  

 [CommandLine("tsenv.exe \\"%1=%2\\""),  

 ActionCategory{"General,7,1"},ActionUI{"AdminUI.TaskSequenceEditor.dll", "Microsoft.ConfigurationManagement.AdminConsole.TaskSequenceEditor", "SetSequenceVariableControl", "TaskSequenceOptionControl"}]  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Operating System Deployment Server WMI Classes](../../../develop/reference/osd/operating-system-deployment-server-wmi-classes.md)
