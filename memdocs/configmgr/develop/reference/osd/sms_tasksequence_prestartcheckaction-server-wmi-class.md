---
description: Learn how to represent a task sequence action to check the readiness of the target computer using SMS_TaskSequence_PrestartCheckAction class.
title: SMS_TaskSequence_PrestartCheckAction class
titleSuffix: Configuration Manager
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 6d4bf98c-7a2b-4747-9d7d-6b92b3af4fbc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
---

# SMS_TaskSequence_PrestartCheckAction server WMI class

The `SMS_TaskSequence_PrestartCheckAction` WMI class is an SMS Provider server class in Configuration Manager. It represents a task sequence action to check the readiness of the target computer.

The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.

## Syntax

```MOF
Class SMS_TaskSequence_PrestartCheckAction : SMS_TaskSequence_Action
{
    Boolean CheckCMClientMinVersion;
    Boolean CheckDeviceUEFI;
    Boolean CheckFreeDiskSpace;
    Boolean CheckMaxOSVersion;
    Boolean CheckMemory;
    Boolean CheckMinOSVersion;
    Boolean CheckNetworkConnected;
    Boolean CheckNetworkWired;
    Boolean CheckOSArchitecture;
    Boolean CheckOSLanguageID;
    Boolean CheckOSType;
    Boolean CheckPowerState;
    Boolean CheckProcessorSpeed;
    String  CMClientMinVersion;
    SMS_TaskSequence_Condition Condition;
    Boolean ContinueOnError;
    String Description;
    Boolean Enabled;
    UInt32  FreeDiskSpace;
    String  MaxOSVersion;
    UInt32 Memory;
    String  MinOSVersion;
    String Name;
    String  OSArchitecture;
    UInt32  OSLanguageID;
    String  OSType;
    UInt32  ProcessorSpeed;
    String SupportedEnvironment;
    UInt32 Timeout;
};
```

## Methods

The `SMS_TaskSequence_PrestartCheckAction` class doesn't define any methods.

## Properties

### `CheckCMClientMinVersion`

Data type: `Boolean`

Access type: Read/write

Qualifiers: `[VariableName("OSDCheckCMClientMinVersion")]`

Enable or disable the check for the minimum version of the Configuration Manager client. The default value is `false`. Set the minimum version with the **CMClientMinVersion** property.

### `CheckDeviceUEFI`

Data type: `Boolean`

Access type: Read/write

Qualifiers: `[VariableName("OSDCheckDeviceUEFI")]`

Enable or disable the check that the device is UEFI. The default value is `false`.

### `CheckFreeDiskSpace`

Data type: `Boolean`

Access type: Read/write

Qualifiers: `[VariableName("OSDCheckFreeDiskSpace"), Not_Null]`

Enable or disable the check for amount of free disk space on the device. The default value is `true`. Set the free disk space with the **FreeDiskSpace** property.

### `CheckMaxOSVersion`

Data type: `Boolean`

Access type: Read/write

Qualifiers: `[VariableName("OSDCheckMaxOsVersion")]`

Enable or disable the check for the maximum version of the OS. The default value is `false`. Set the maximum OS version with the **MaxOSVersion** property.

### `CheckMemory`

Data type: `Boolean`

Access type: Read/write

Qualifiers: `[VariableName("OSDCheckMemory"), Not_Null]`

Enable or disable the check for minimum memory on the device. The default value is `true`. Set the minimum memory size with the **Memory** property.

### `CheckMinOSVersion`

Data type: `Boolean`

Access type: Read/write

Qualifiers: `[VariableName("OSDCheckMinOSVersion")]`

Enable or disable the check for the minimum version of the OS. The default value is `false`. Set the minimum OS version with the **MinOSVersion** property.

### `CheckNetworkConnected`

Data type: `Boolean`

Access type: Read/write

Qualifiers: `[VariableName("OSDCheckNetworkConnected")]`

Enable or disable the check if the device has a network adapter that's connected to the network. The default value is `false`. Also see the dependent property **CheckNetworkWired**.

### `CheckNetworkWired`

Data type: `Boolean`

Access type: Read/write

Qualifiers: `CheckNetworkWired`

Enable or disable the check if the device has a network adapter that isn't wireless. The default value is `false`. To enable this property, enable the **CheckNetworkConnected** property.

### `CheckOSArchitecture`

Data type: `Boolean`

Access type: Read/write

Qualifiers: `[VariableName("OSDCheckOSArchitecture")]`

Enable or disable the check for whether the current OS is 32-bit or 64-bit. The default value is `false`. Set the architecture with the **OSArchitecture** property.

### `CheckOSLanguageID`

Data type: `Boolean`

Access type: Read/write

Qualifiers: `[VariableName("OSDCheckOSLanguageID")]`

Enable or disable the check for the OS language. The default value is `false`. Set the language code with the **OSLanguageID** property.

### `CheckOSType`

Data type: `Boolean`

Access type: Read/write

Qualifiers: `[VariableName("OSDCheckOSType"), Not_Null]`

Enable or disable the check for the type of device. The default value is `true`. Set the device type with the **OSType** property.

### `CheckPowerState`

Data type: `Boolean`

Access type: Read/write

Qualifiers: `[VariableName("OSDCheckPowerState")]`

Enable or disable the check if the device is plugged in to AC power and not on battery. The default value is `false`.

### `CheckProcessorSpeed`

Data type: `Boolean`

Access type: Read/write

Qualifiers: `[VariableName("OSDCheckProcessorSpeed"), Not_Null]`

Enable or disable the check for the minimum processor speed of the device. The default value is `true`. Set the minimum processor speed with the **ProcessorSpeed** property.

### `CMClientMinVersion`

Data type: `String`

Access type: Read/write

Qualifiers: `[VariableName("OSDCMClientMinVersion")]`

Set the minimum version of the Configuration Manager client. Specify the client version in the following format: `5.00.8913.1005`. To configure this property, enable the **CheckCMClientMinVersion** property.

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

### `FreeDiskSpace`

Data type: `UInt32`

Access type: Read/write

Qualifiers: `[VariableName("OSDFreeDiskSpace")]`

Set the amount of free disk space in MB on the device. The default value is `25000`. To configure this property, enable the **CheckFreeDiskSpace** property.

### `MaxOSVersion`

Data type: `String`

Access type: Read/write

Qualifiers: `[VariableName("OSDMaxOSVersion")]`

Set the maximum version of the OS. Specify the version with major version, minor version, and build number. For example, `10.0.18356`. To configure this property, enable the **CheckMaxOSVersion** property.

### `Memory`

Data type: `UInt32`

Access type: Read/write

Qualifiers: `[VariableName("OSDMemory")]`

Set the minimum memory in MB on the device. The default value is `512`. To configure this property, enable the **CheckMemory** property.

### `MinOSVersion`

Data type: `String`

Access type: Read/write

Qualifiers: `[VariableName("OSDMinOSVersion")]`

Set the minimum version of the OS. Specify the version with major version, minor version, and build number. For example, `10.0.16299`. To configure this property, enable the **CheckMinOSVersion** property.

### `Name`

Data type: `String`

Access type: Read/Write

Qualifiers: [AllowedLen("1-100")]

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).

### `OSArchitecture`

Data type: `String`

Access type: Read/write

Qualifiers: `[VariableName("OSDOSArchitecture"), ValueMap{"","32","64"}]`

Set the architecture of the OS, either `32` or `64`. The default value is `64`. To configure this property, enable the **CheckOSArchitecture** property.

### `OSLanguageID`

Data type: `UInt32`

Access type: Read/write

Qualifiers: `[VariableName("OSDOSLanguageID")]`

Set a language code to match against the OS language. For example, `1033` for **English (United States)**. This check compares the language that you set to the **OSLanguage** property of the **Win32_OperatingSystem** WMI class on the client. To configure this property, enable the **CheckOSLanguageID** property.

### `OSType`

Data type: `String`

Access type: Read/write

Qualifiers: `[VariableName("OSDOSType"), ValueMap{"CLIENT","SERVER"}]`

Set the type of device to check, either `CLIENT` or `SERVER`. The default value is `CLIENT`. To configure this property, enable the **CheckOSType** property.

### `ProcessorSpeed`

Data type: `UInt32`

Access type: Read/write

Qualifiers: `[VariableName("OSDProcessorSpeed")]`

Set the minimum processor speed in MHz for the device. The default value is `800`. To configure this property, enable the **CheckProcessorSpeed** property.

### `SupportedEnvironment`

Data type: `String`

Access type: Read/Write

Qualifiers: [Not_Null:ToInstance]

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).

The default value of this property for this task sequence action is FullOS.

### `Timeout`

Data type: `UInt32`

Access type: Read/Write

Qualifiers: None

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).

## Remarks

For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager class and property qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).

## Requirements

### Runtime requirements

For more information, see [Configuration Manager server runtime requirements](../../../develop/core/reqs/server-runtime-requirements.md).

### Development requirements

For more information, see [Configuration Manager server development requirements](../../../develop/core/reqs/server-development-requirements.md).
