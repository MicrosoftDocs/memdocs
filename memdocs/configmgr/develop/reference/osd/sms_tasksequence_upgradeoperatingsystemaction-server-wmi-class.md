---
title: SMS_TaskSequence_UpgradeOperatingSystemAction class
titleSuffix: Configuration Manager
description: Details of the SMS_TaskSequence_UpgradeOperatingSystemAction server WMI class.
ms.date: 10/01/2021
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
---

# SMS_TaskSequence_UpgradeOperatingSystemAction server WMI class

The `SMS_TaskSequence_UpgradeOperatingSystemAction` WMI class is an SMS provider server class in Configuration Manager. It represents a task sequence action that upgrades the OS. This step is only supported for Windows 10 and Windows 11.

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
    String FeatureUpdateAssignmentId;
    String FeatureUpdateName
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

For more information, see [SMS_TaskSequence_Action server WMI class](sms_tasksequence_action-server-wmi-class.md).  

### `ContinueOnError`

Data type: `Boolean`

Access type: Read/Write

Qualifiers: None

For more information, see [SMS_TaskSequence_Action server WMI class](sms_tasksequence_action-server-wmi-class.md).

### `Description`

Data type: `String`

Access type: Read/Write

Qualifiers: `[AllowedLen("0-255")]`

For more information, see [SMS_TaskSequence_Action server WMI class](sms_tasksequence_action-server-wmi-class.md).

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

For more information, see [SMS_TaskSequence_Action server WMI class](sms_tasksequence_action-server-wmi-class.md).

### `FeatureUpdateAssignmentId`

Data type: `String`

Access type: Read/Write

Qualifiers: None

The deployment ID of a feature update used to upgrade the Window OS.

### `FeatureUpdateName`

Data type: `String`

Access type: Read/Write

Qualifiers: None

The name of a feature update used to upgrade the Window OS.

### `IgnoreMessages`

Data type: `Boolean`

Access type: Read/Write

Qualifiers: None

Ignores compatibility messages that can be dismissed. The default value is `false`.

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

For more information, see [SMS_TaskSequence_Action server WMI class](sms_tasksequence_action-server-wmi-class.md).

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

The default value is `FullOS`. For more information, see [SMS_TaskSequence_Action server WMI class](sms_tasksequence_action-server-wmi-class.md).

### `Timeout`

Data type: `UInt32`

Access type: Read/Write

Qualifiers: None

For more information, see [SMS_TaskSequence_Action server WMI class](sms_tasksequence_action-server-wmi-class.md).

## Requirements

### Runtime requirements

For more information, see [Configuration Manager server runtime requirements](../../core/reqs/server-runtime-requirements.md).

### Development requirements

For more information, see [Configuration Manager server development requirements](../../core/reqs/server-development-requirements.md).
