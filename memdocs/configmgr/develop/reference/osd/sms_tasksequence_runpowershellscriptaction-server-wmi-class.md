---
title: SMS_TaskSequence_RunPowerShellScriptAction Class
titleSuffix: Configuration Manager
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: b0f7d2c6-ca63-4f73-82d9-1f7f3efbca25
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
---

# SMS_TaskSequence_RunPowerShellScriptAction server WMI class

The `SMS_TaskSequence_RunPowerShellScriptAction` WMI class is an SMS Provider server class in Configuration Manager. It represents a task sequence action that runs a user-specified Windows PowerShell script.

The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.

## Syntax

```MOF
Class SMS_TaskSequence_RunPowerShellScriptAction : SMS_TaskSequence_Action
{
    SMS_TaskSequence_Condition Condition;
    Boolean ContinueOnError;
    String Description;
    Boolean Enabled;
    string ExecutionPolicy;
    String Name;
    string OutputVariableName;
    string PackageID;
    string Parameters;
    boolean RunAsUser;
    string ScriptName;
    string SourceScript;
    string SuccessCodes;
    string SupportedEnvironment;
    UInt32 Timeout;
    string UserName;
    string UserPassword;
    string WorkingDirectory;
};
```

## Methods

The `SMS_TaskSequence_RunPowerShellScriptAction` class doesn't define any methods.

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

Qualifiers: [AllowedLen("0-255")]

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).

### `Enabled`

Data type: `Boolean`

Access type: Read/Write

Qualifiers: None

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).

### `ExecutionPolicy`

Data type: `String`

Access type: Read/write

Qualifiers: `[ValueMap{"Restricted", "AllSigned", "RemoteSigned", "Unrestricted", "Bypass", "Undefined"}, Not_Null:ToInstance]`

Specify the PowerShell execution policy. By default the value is `Restricted`.

### `Name`

Data type: `String`

Access type: Read/Write

Qualifiers: [AllowedLen("1-100")]

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).

### `OutputVariableName`

Data type: `String`

Access type: Read/write

Qualifiers: None

Specify a task sequence variable to store the output of the script.

### `PackageID`

Data type: `String`

Access type: Read/write

Qualifiers: `[RequiredIfNull("SourceScript"), TaskSequencePackage]`

The ID of a package that includes the script.

### `Parameters`

Data type: `String`

Access type: Read/write

Qualifiers: [Not_Null]

Specify any parameters to pass on the PowerShell command line for the script.

### `RunAsUser`

Data type: `Boolean`

Access type: Read/write

Qualifiers: [VariableName("_SMSTSRunPowerShellAsUser"), RequireR2]

When set to `true`, the command line runs under the credentials specified by the `UserName` property.

The default value is: `false`

### `ScriptName`

Data type: `String`

Access type: Read/write

Qualifiers: `[RequiredIfNull("SourceScript")]`

The name of the source PowerShell script.

### `SourceScript`

Data type: `String`

Access type: Read/write

Qualifiers: `[RequiredIfNull("PackageID")]`

Specify the package ID of the source script to import.

### `SuccessCodes`

Data type: `String`

Access type: `Read/Write`

Qualifiers: `[SuccessCodes, Not_Null]`

Exit codes that indicate success. The default value is `"0 3010"`.

### `SupportedEnvironment`

Data type: `String`

Access type: Read/Write

Qualifiers: [Not_Null:ToInstance]

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).

The default value is `WinPEandFullOS`.

### `Timeout`

Data type: `UInt32`

Access type: Read/Write

Qualifiers: [Not_Null:ToInstance]

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).

### `UserName`

Data type: `String`

Access type: Read/Write

Qualifiers: `[VariableName("SMSTSRunPowerShellUserName"]`

The user account to run the command line under when the `RunAsUser` property is set to `true`.

### `UserPassword`

Data type: `String`

Access type: Read/Write

Qualifiers: `[VariableName("SMSTSRunPowerShellUserPassword", Secret]`

Masked password associated with the user account that is used to run the command line when the `RunAsUser` property is set to `true`.

### `WorkingDirectory`

Data type: `String`

Access type: Read/Write

Qualifiers: [AllowedLen("0-255")]

The directory from which to run the command line. Set this property to an absolute path or a relative path. The path length must be between 0 and 255 characters.

## Remarks

For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager class and property qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).

## Requirements

### Runtime requirements

For more information, see [Configuration Manager server runtime requirements](../../../develop/core/reqs/server-runtime-requirements.md).

### Development requirements

For more information, see [Configuration Manager server development requirements](../../../develop/core/reqs/server-development-requirements.md).
