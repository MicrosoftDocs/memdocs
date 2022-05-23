---
title: SMS_TaskSequence_ApplyDriverPackageAction class
titleSuffix: Configuration Manager
description: "The SMS Provider server class represents an action used in a task sequence to make all device drivers in a driver package available for use by Windows setup."
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: a84ea8fa-ba47-4e73-a946-9eb579feadd6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
---

# SMS_TaskSequence_ApplyDriverPackageAction server WMI class

The `SMS_TaskSequence_ApplyDriverPackageAction` WMI class is an SMS Provider server class in Configuration Manager. It represents an action used in a task sequence to make all device drivers in a driver package available for use by Windows setup.

The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.

## Syntax

```MOF
Class SMS_TaskSequence_ApplyDriverPackageAction : SMS_TaskSequence_Action
{
        String BootCriticalContentUniqueID;
        String BootCriticalDriverID;
        String BootCriticalHardwareComponent;
        String BootCriticalID;
        String BootCriticalINFFile;
        SMS_TaskSequence_Condition Condition;
        Boolean ContinueOnError;
        String Description;
        String DriverPackageID;
        Boolean Enabled;
        String Name;
        Boolean Recurse;
        String SupportedEnvironment;
        UInt32 Timeout;
        Boolean UnsignedDriver;
};
```

## Methods

The `SMS_TaskSequence_ApplyDriverPackageAction` class doesn't define any methods.

## Properties

### `BootCriticalContentUniqueID`

Data type: `String`

Access type: Read/Write

Qualifiers: `[RequiredIfNotNull]`

The unique ID of the content associated a boot-critical mass storage device driver. If this ID isn't specified, no mass-storage device driver is installed. The driver content can be obtained from the [SMS_CIToContent server WMI class](../../../develop/reference/sum/sms_citocontent-server-wmi-class.md) where the **CI_ID** property matches the driver ID. The default value is `null`.

> [!NOTE]
> This property is required if **BootCriticalDriverID** is set.

### `BootCriticalDriverID`

Data type: `String`

Access type: Read/Write

Qualifiers: `[CommandLineArg(2)]`

Optional ID specified by the **CI_UniqueID** property of the [SMS_Driver server WMI class](../../../develop/reference/osd/sms_driver-server-wmi-class.md) object to install for a boot-critical mass storage device driver. The default value is `null`.

### `BootCriticalHardwareComponent`

Data type: `String`

Access type: Read/Write

Qualifiers: `[RequiredIfNotNull]`

Hardware component used if a boot-critical mass storage device driver is being installed. The default value is `null`.

> [!NOTE]
> This property is required if **BootCriticalDriverID** is set.

### `BootCriticalID`

Data type: `String`

Access type: Read/Write

Qualifiers: `[RequiredIfNotNull]`

The boot-critical ID of the mass-storage device driver to be installed. The default value is `null`. This ID is listed in the "scsi" section of the device driver Txtsetup.oem file.

> [!NOTE]
> This property is required if **BootCriticalDriverID** is set.

### `BootCriticalINFFile`

Data type: `String`

Access type: Read/Write

Qualifiers: `[RequiredIfNotNull]`

The INF file of a boot-critical mass-storage device driver to be installed. The default value is `null`.

> [!NOTE]
> This property is required if **BootCriticalDriverID** is set.

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

Qualifiers: `[CommandLineArg(1), TaskSequencePackage, Not_Null]`

ID of the driver package to install. This value is indicated by the **PackageID** property of the specific [SMS_DriverPackage server WMI class](../../../develop/reference/osd/sms_driverpackage-server-wmi-class.md) object.

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

### `Recurse`

Data type: `Boolean`

Access type: Read/write

Values:

- `false` (default): Use the list of drivers from the driver package.
- `true`: Run DISM once to recurse on the entire driver package folder.

### `SupportedEnvironment`

Data type: `String`

Access type: Read/Write

Qualifiers: `[Not_Null:ToInstance]`

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).

The default value for this class is WinPE.

### `Timeout`

Data type: `UInt32`

Access type: Read/Write

Qualifiers: None

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).

### `UnsignedDriver`

Data type: `Boolean`

Access type: Read/Write

Qualifiers: `[Not_Null, VariableName("OSDAllowUnsignedDriver")]`

Set `true` to configure Windows to allow unsigned device drivers to be installed. The default value is `false`.

> [!NOTE]
> This property is required by the action. However, it's deprecated and not used by modern OS versions.

## Remarks

Class qualifiers for this class include:

```
[CommandLine("osddriverclient.exe /install:%1 \<?2:\\"/bootcritical:%%OSDApplyDriverBootCriticalContentUniqueID%%,%%OSDApplyDriverBootCriticalINFFile%%,%%OSDApplyDriverBootCriticalHardwareComponent%%,%%OSDApplyDriverBootCriticalID%%\\">/unsigned:%%OSDAllowUnsignedDriver%%"),ActionCategory{"Drivers,2,6"},ActionUI{"AdminUI.TaskSequenceEditor.dll", "Microsoft.ConfigurationManagement.AdminConsole.TaskSequenceEditor", "ApplyDriverPackageControl", "TaskSequenceOptionControl"}, VariablePrefix("OSDApplyDriver")]
```

For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager class and property qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).

## Requirements

### Runtime requirements

For more information, see [Configuration Manager server runtime requirements](../../../develop/core/reqs/server-runtime-requirements.md).

### Development requirements

For more information, see [Configuration Manager server development requirements](../../../develop/core/reqs/server-development-requirements.md).

## See also

- [SMS_Driver server WMI class](../../../develop/reference/osd/sms_driver-server-wmi-class.md)

- [SMS_DriverPackage server WMI class](../../../develop/reference/osd/sms_driverpackage-server-wmi-class.md)

- [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md)
