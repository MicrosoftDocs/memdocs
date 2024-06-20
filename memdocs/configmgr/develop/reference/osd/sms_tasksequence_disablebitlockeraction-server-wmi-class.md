---
title: SMS_TaskSequence_DisableBitLockerAction class
titleSuffix: Configuration Manager
description: An SMS Provider server class that represents a task sequence action, which disables the BitLocker encryption on the specified drive.
ms.date: 08/11/2020
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: f72e8ac9-1b99-408b-9462-bbbd6d673212
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# SMS_TaskSequence_DisableBitLockerAction server WMI class

The `SMS_TaskSequence_DisableBitLockerAction` WMI class is an SMS Provider server class in Configuration Manager. It represents a task sequence action that disables the BitLocker encryption on the specified drive.

The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.

## Syntax

```MOF
Class SMS_TaskSequence_DisableBitLockerAction : SMS_TaskSequence_Action
{
      SMS_TaskSequence_Condition Condition;
      Boolean ContinueOnError;
      String Description;
      Boolean Enabled;
      String Name;
      UInt32 RebootCount;
      String SupportedEnvironment;
      String TargetDrive;
      UInt32 Timeout;
};
```

## Methods

The `SMS_TaskSequence_DisableBitLockerAction` class doesn't define any methods.

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

### `RebootCount`

Data type: `UInt32`

Access type: Read/write

The default value is `1`. Specify the number of restarts to keep BitLocker disabled.

### `SupportedEnvironment`

Data type: `String`

Access type: Read/Write

Qualifiers: `[Not_Null:ToInstance]`

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).

The default value of this property for this task sequence action is `FullOS`.

### `TargetDrive`

Data type: `String`

Access type: Read/Write

Qualifiers: `[CommandLineArg(1)]`

Drive letter of the volume on which to disable the BitLocker encryption. To use the current OS volume, set this property to `null`.

### `Timeout`

Data type: `UInt32`

Access type: Read/Write

Qualifiers: None

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).

## Remarks

Class qualifiers for this class include:

```
[CommandLine("OSDBitLocker.exe /disable \<?1: /drive:%1>"),

ActionCategory{"Disks,5,3"},ActionUI{"AdminUI.TaskSequenceEditor.dll", "Microsoft.ConfigurationManagement.AdminConsole.TaskSequenceEditor", "DisableBitLockerControl", "TaskSequenceOptionControl"}, VariablePrefix("OSDBitLocker")]
```

For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager class and property qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).

## Requirements

### Runtime requirements

For more information, see [Configuration Manager server runtime requirements](../../../develop/core/reqs/server-runtime-requirements.md).

### Development requirements

For more information, see [Configuration Manager server development requirements](../../../develop/core/reqs/server-development-requirements.md).

## See also

[SMS_TaskSequence_Action server WMI class](sms_tasksequence_action-server-wmi-class.md)
