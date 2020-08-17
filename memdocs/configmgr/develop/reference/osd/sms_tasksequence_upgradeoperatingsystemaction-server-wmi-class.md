---
title: SMS_TaskSequence_UpgradeOperatingSystemAction class
titleSuffix: Configuration Manager
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 4a5f6ade-6ab5-4324-ac0e-6348b9488712
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# SMS_TaskSequence_UpgradeOperatingSystemAction server WMI class

The `SMS_TaskSequence_UpgradeOperatingSystemAction` WMI class is an SMS provider server class in Configuration Manager. It represents a task sequence action that upgrades the OS. This step is only supported for Windows 10.

The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.

## Syntax

```MOF
Class SMS_TaskSequence_UpgradeOperatingSystemAction : SMS_TaskSequence_Action
{
    SMS_TaskSequence_Condition Condition;
    Boolean ContinueOnError;
    String Description;
    String DriverPackageID;
    String DynamicUpdateSettings;
    Boolean Enabled;
    Boolean IgnoreMessages;
    UInt32 InstallEditionIndex;
    String InstallPackageID;
    String InstallPath;
    String Name;
    String OsProductKey;
    String PreserveSettings;
    Boolean ScanOnly;
    UInt32 SetupTimeout;
    String StagedContent;
    String SupportedEnvironment;
    UInt32 Timeout;
};
```

## Methods

The `SMS_TaskSequence_UpgradeOperatingSystemAction` class doesn't define any methods.

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

### `DriverPackageID`

Data type: `String`

Access type: Read/Write

Qualifiers: `[TaskSequencePackage]`

The package ID of the driver package to use during upgrade.

### `DynamicUpdateSettings`

Data type: `string`

Access type: Read/Write

Qualifiers: `[ValueMap]`

Specifies whether to dynamically update Windows Setup with Windows Update.

Possible values:

- `Disable`
- `OveridePolicy`

### `Enabled`

Data type: `Boolean`

Access type: Read/Write

Qualifiers: None

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).

### `IgnoreMessages`

Data type: `Boolean`

Access type: Read/Write

Qualifiers: None

Ignores dismissible compatibility messages. The default value is `false`.

### `InstallEditionIndex`

Data type: `UInt32`

Access type: Read/Write

Qualifiers: None

The installation edition index. The default value is `1`.

### `InstallPackageID`

Data type: `String`

Access type: Read/Write

Qualifiers: `[TaskSequencePackage("image"), RequiredIfNull("InstallPath")]`

The ID of the OS upgrade package to use.

### `InstallPath`

Data type: `String`

Access type: Read/Write

Qualifiers: `[RequiredIfNull("InstallPackageID")]`

The path or environment variable to the OS upgrade package to use.

### `Name`

Data type: `String`

Access type: Read/Write

Qualifiers: `[AllowedLen("1-100")]`

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).

### `OsProductKey`

Data type: `String`

Access type: Read/Write

Qualifiers: `[QuasiSecret]`

The product key for the OS upgrade content.

### `PreserveSettings`

Data type: `String`

Access type: Read/Write

Qualifiers: `[ValueMap]`

Specifies what data to keep during an upgrade. The default value is `Upgrade`, which keeps applications, data, and settings. For best results, use the default value.

### `ScanOnly`

Data type: `Boolean`

Access type: Read/Write

Qualifiers: None

Runs a Windows Setup compatibility scan without starting the upgrade. The default value is `false`.

### `SetupTimeout`

Data type: `UInt32`

Access type: Read/Write

Qualifiers: None

The timeout that applies when running Windows Setup from the command line during an upgrade.

### `StagedContent`

Data type: `String`

Access type: Read/Write

Qualifiers: None

The path or environment variable to the driver content to use for the upgrade.

### `SupportedEnvironment`

Data type: `String`

Access type: Read/Write

Qualifiers: None

The default value is `FullOS`. For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).

### `Timeout`

Data type: `UInt32`

Access type: Read/Write

Qualifiers: None

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).

## Requirements

### Runtime requirements

For more information, see [Configuration Manager server runtime requirements](../../../develop/core/reqs/server-runtime-requirements.md).

### Development requirements

For more information, see [Configuration Manager server development requirements](../../../develop/core/reqs/server-development-requirements.md).
