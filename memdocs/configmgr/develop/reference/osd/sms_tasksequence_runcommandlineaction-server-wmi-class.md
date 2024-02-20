---
title: SMS_TaskSequence_RunCommandLineAction class
titleSuffix: Configuration Manager
description: an SMS Provider server class in Configuration Manager. It represents a task sequence action that runs a user-specified command line.
ms.date: 08/11/2020
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: b0f7d2c6-ca63-4f73-82d9-1f7f3efbca25
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# SMS_TaskSequence_RunCommandLineAction server WMI class

The `SMS_TaskSequence_RunCommandLineAction` WMI class is an SMS Provider server class in Configuration Manager. It represents a task sequence action that runs a user-specified command line.

The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```MOF
Class SMS_TaskSequence_RunCommandLineAction : SMS_TaskSequence_Action
{
      String CommandLine;
      SMS_TaskSequence_Condition Condition;
      Boolean ContinueOnError;
      String Description;
      Boolean DisableWow64Redirection;
      Boolean Enabled;
      String Name;
      String PackageID;
      String OutputVariableName;
      Boolean RunAsUser;
      String SuccessCodes;
      String SupportedEnvironment;
      UInt32 Timeout;
      String UserName;
      String UserPassword;
      String WorkingDirectory;
};  
```  

## Methods

The `SMS_TaskSequence_RunCommandLineAction` class doesn't define any methods.

## Properties

### `CommandLine`

Data type: `String`  

Access type: Read/Write  

Qualifiers: `[Not_Null, CommandLineArg(2), AllowedLen("1-32000")]`

Specify a command-line. The length can be between 1 and 32,000 characters. For example: `cmd /c ipconfig > c:\ipconfig.txt`

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

### `DisableWow64Redirection`

Data type: `Boolean`  

Access type: Read/Write  

Qualifiers: `[Not_Null, VariableName("SMSTSDisableWow64Redirection")]`

Set `true` if the task sequence engine disables Wow64 file redirection and 64-bit registry redirection. It uses this behavior when it evaluates file, folder, and registry conditions on a 64-bit OS. The default value is `false`.

The task sequence variable associated with this property is [SMSTSDisableWow64Redirection](../../../osd/understand/task-sequence-variables.md#SMSTSDisableWow64Redirection).

### `Enabled`

Data type: `Boolean`  

Access type: Read/Write  

Qualifiers: None  

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

### `Name`

Data type: `String`  

Access type: Read/Write  

Qualifiers: `[AllowedLen("1-100")]`

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

### `PackageID`

Data type: `String`  

Access type: Read/Write  

Qualifiers: `[TaskSequencePackage, CommandLineArg(1)]`

The ID of a package associated with the action.

### `OutputVariableName`

Data type: `String`

Access type: Read/write

Qualifiers: None

Specify a task sequence variable to store the output of the script.

### `RunAsUser`

Data type: `Boolean`

Access type: Read/Write  

Qualifiers: `[VariableName("_SMSTSRunCommandLineAsUser"), RequireR2]`

When set to `true`, the command line runs under the credentials specified by the `UserName` property. The default value is: `false`

### `SuccessCodes`

Data type: `String`  

Access type: Read/Write

Qualifiers: `[SuccessCodes, Not_Null]`

Exit codes that indicate success. The default setting is `"0 3010"`.

### `SupportedEnvironment`

Data type: `String`  

Access type: Read/Write  

Qualifiers: `[Not_Null:ToInstance]`

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

### `Timeout`

Data type: `UInt32`  

Access type: Read/Write  

Qualifiers: `[Not_Null:ToInstance]`

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

### `UserName`

Data type: `String`  

Access type: Read/Write  

Qualifiers: `[VariableName("SMSTSRunCommandLineUserName"]`

The user account to run the command line under when the `RunAsUser` property is set to `true`.  

### `UserPassword`

Data type: `String`  

Access type: Read/Write  

Qualifiers: `[VariableName("SMSTSRunCommandLineUserPassword", Secret]`

Masked password associated with the user account that is used to run the command line when the `RunAsUser` property is set to `true`.  

### `WorkingDirectory`

Data type: `String`  

Access type: Read/Write  

Qualifiers: `[AllowedLen("0-255")]`

The directory from which to run the command line. Set this property to an absolute path or a relative path. The path length must be between 0 and 255 characters.  

## Remarks

Class qualifiers for this class include:  

```
[CommandLine("smsswd.exe /run:%1 %2"),  

ActionCategory("General,1,1"),ActionUI{"AdminUI.TaskSequenceEditor.dll", "Microsoft.ConfigurationManagement.AdminConsole.TaskSequenceEditor", "RunCommandLineControl", "TaskSequenceOptionControl"}]  
```

For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager class and property qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).

## Requirements

### Runtime requirements

For more information, see [Configuration Manager server runtime requirements](../../../develop/core/reqs/server-runtime-requirements.md).

### Development requirements

For more information, see [Configuration Manager server development requirements](../../../develop/core/reqs/server-development-requirements.md).
