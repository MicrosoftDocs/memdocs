---
description: Learn how to represent a task sequence action that specifies the Sysprep options to use when capturing Windows settings from the reference computer.
title: SMS_TaskSequence_PrepareOSAction class
titleSuffix: Configuration Manager
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 8227372d-303d-4c6e-bee5-da20bd443437
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
---

# SMS_TaskSequence_PrepareOSAction server WMI class

The `SMS_TaskSequence_PrepareOSAction` WMI class is an SMS Provider server class in Configuration Manager. It represents a task sequence action that specifies the Sysprep options to use when capturing Windows settings from the reference computer.

The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.

## Syntax

```MOF
Class SMS_TaskSequence_PrepareOSAction : SMS_TaskSequence_Action
{
      Boolean BuildStorageDriverList;
      SMS_TaskSequence_Condition Condition;
      Boolean ContinueOnError;
      String Description;
      Boolean Enabled;
      Boolean KeepActivation;
      String Name;
      boolean ShutdownPreparedOs;
      String SupportedEnvironment;
      UInt32 Timeout;
};
```

## Methods

The `SMS_TaskSequence_PrepareOSAction` class doesn't define any methods.

## Properties

### `BuildStorageDriverList`

Data type: `Boolean`

Access type: Read/Write

Qualifiers: `[not_null, VariableName("OSDBuildStorageDriverList")]`

Set `true` to build a mass-storage device driver list. The default value is `false`.

This property is deprecated. It only applies to Windows XP and Windows Server 2003.

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

### `KeepActivation`

Data type: `Boolean`

Access type: Read/Write

Qualifiers: `[not_null, VariableName("OSDKeepActivation")]`

Set `true` to keep the current product activation flag. Set `false` to reset it. The default value is `false`.

The task sequence variable associated with this property is [OSDKeepActivation](../../../osd/understand/task-sequence-variables.md#OSDKeepActivation).

### `Name`

Data type: `String`

Access type: Read/Write

Qualifiers: `[AllowedLen("1-100")]`

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).

### `ShutdownPreparedOs`

Data type: `Boolean`

Access type: Read/write

Corresponds to the following setting in the task sequence editor: **Shutdown the computer after running this action**. The default value is `false`.

### `SupportedEnvironment`

Data type: `String`

Access type: Read/Write

Qualifiers: `[Not_Null:ToInstance]`

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).

The default value of this property for this task sequence action is `FullOS`.

### `Timeout`

Data type: `UInt32`

Access type: Read/Write

Qualifiers: None

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).

## Remarks

Class qualifiers for this class include:

```
[CommandLine("osdprepareos.exe /activate:%%OSDKeepActivation%% /bmsd:%%OSDBuildStorageDriverList%%"),

ActionCategory{"Images,7,5"},ActionUI{"AdminUI.TaskSequenceEditor.dll", "Microsoft.ConfigurationManagement.AdminConsole.TaskSequenceEditor", "WindowsCaptureControl", "TaskSequenceOptionControl"}]
```

For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager class and property qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).

## Requirements

### Runtime requirements

For more information, see [Configuration Manager server runtime requirements](../../../develop/core/reqs/server-runtime-requirements.md).

### Development requirements

For more information, see [Configuration Manager server development requirements](../../../develop/core/reqs/server-development-requirements.md).
