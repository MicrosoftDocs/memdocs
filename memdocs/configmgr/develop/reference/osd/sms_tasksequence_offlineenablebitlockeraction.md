---
title: SMS_TaskSequence_OfflineEnableBitLockerAction class
titleSuffix: Configuration Manager
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 596e92ca-fc30-47b2-b249-cf61d5c76121
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
---

# SMS_TaskSequence_OfflineEnableBitLockerAction server WMI class

The `SMS_TaskSequence_OfflineEnableBitLockerAction` WMI class is an SMS Provider server class in Configuration Manager. It represents a task sequence action that pre-provisions BitLocker for the OS drive.

The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.

## Syntax

```MOF
Class SMS_TaskSequence_OfflineEnableBitLockerAction : SMS_TaskSequence_Action
{
    Object Condition;
    Boolean ContinueOnError;
    String Description;
    UInt32 DestinationDisk;
    String DestinationLogicalDrive;
    UInt32 DestinationPartition;
    String DestinationVariable;
    Boolean Enabled;
    Boolean EncryptFullDisk;
    UInt32 EncryptMethod;
    String Name;
    Boolean SkipWhenTPMInvalid;
    String SupportedEnvironment;
    UInt32 Timeout;
};
```

## Methods

The `SMS_TaskSequence_OfflineEnableBitLockerAction` class doesn't define any methods.

## Properties

### `Condition`

Data type: `Object`

Access type: Read/Write

Qualifiers: none

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).

### `ContinueOnError`

Data type: `Boolean`

Access type: Read/Write

Qualifiers: none

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).

### `Description`

Data type: `String`

Access type: Read/Write

Qualifiers: `[allowedlen]`

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).

### `DestinationDisk`

Data type: `UInt32`

Access type: Read/Write

Qualifiers: `[commandlinearg(1), valuerange("0-99")]`

Index of the disk for which to pre-provision BitLocker. The index can have a value of 1 through 99.

### `DestinationLogicalDrive`

Data type: `String`

Access type: Read/Write

Qualifiers: `[commandlinearg(3), valuemap {"C:","D:","E:","F:","G:","H:","I:","J:","K:","L:","M:","N:","O:","P:","Q:","R:","S:","T:","U:","V:","W:","X:","Y:","Z:"}]`

Logical drive letter of the volume to which to provision BitLocker. Possible values are A-Z.

### `DestinationPartition`

Data type: `UInt32`

Access type: Read/Write

Qualifiers: `[commandlinearg(2), requiredifnotnull("DesinationDisk"), valuerange("1-99")]`

Index of the partition on the target disk specified by `DestinationDisk` to which to pre-provision BitLocker. The index can have a value of 1 through 99.

### `DestinationVariable`

Data type: `String`

Access type: Read/Write

Qualifiers: `[commandlinearg]`

Task sequence variable containing the logical drive letter of the volume to which to pre-provision BitLocker.

### `Enabled`

Data type: `Boolean`

Access type: Read/Write

Qualifiers: none

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).

### `EncryptFullDisk`

Data type: `Boolean`

Access type: Read/write

Configure the step to use full disk encryption. The default value is `false`.

### `EncryptMethod`

Data type: `UInt32`

Access type: Read/write

Specify the disk encryption mode. Set `0` to not specify the mode, which is the default.

### `Name`

Data type: `String`

Access type: Read/Write

Qualifiers: `[allowedlen("1-100")]`

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).

### `SkipWhenTPMInvalid`

Data type: `Boolean`

Access type: Read/Write

Qualifiers: `[commandlinearg(5), not_null]`

Set `true` to skip this step for computers that don't have a TPM or when TPM isn't enabled.

### `SupportedEnvironment`

Data type: `String`

Access type: Read/Write

Qualifiers: `[not_null, valuemap]`

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).

The default value of this property for this task sequence action is `WinPE`.

### `Timeout`

Data type: `UInt32`

Access type: Read/Write

Qualifiers: none

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).

## Remarks

Class qualifiers for this class include:

```
[CommandLine(     "OSDOfflineBitlocker.exe /enable \<?1: /disk:%1>\<?2: /part:%2>\<?3: /drive:%3>\<?4: /drive:%%%4%%>\<?5: /ignoretpm:%5>"     ),

ActionCategory{"Disks,6,3"},     ActionUI{"AdminUI.TaskSequenceEditor.dll", "Microsoft.ConfigurationManagement.AdminConsole.TaskSequenceEditor", "OfflineBitlockerControl", "TaskSequenceOptionControl"},     VariablePrefix("OSDBitLocker")     ]
```

For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager class and property qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).

## Requirements

## Runtime requirements

For more information, see [Configuration Manager server runtime requirements](../../../develop/core/reqs/server-runtime-requirements.md).

## Development requirements

For more information, see [Configuration Manager server development requirements](../../../develop/core/reqs/server-development-requirements.md).

## See also

[SMS_TaskSequence_ApplyDataImageAction server WMI class](../../../develop/reference/osd/sms_tasksequence_applydataimageaction-server-wmi-class.md)
