---
title: SMS_TaskSequence_EnableBitLockerAction class
titleSuffix: Configuration Manager
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 5093946d-e8a5-458f-9af7-6618cf202385
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
---

# SMS_TaskSequence_EnableBitLockerAction server WMI class

The `SMS_TaskSequence_EnableBitLockerAction` WMI class is an SMS Provider server class in Configuration Manager. It represents a task sequence action that enables the BitLocker encryption on the specified drive.

The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```MOF
Class SMS_TaskSequence_EnableBitLockerAction : SMS_TaskSequence_Action  
{  
      SMS_TaskSequence_Condition Condition;  
      Boolean ContinueOnError;  
      String CreateRecoveryPassword;  
      String Description;  
      Boolean Enabled;  
      UInt32 EncryptMethod;
      String Mode;  
      String Name;  
      String PIN;  
      Boolean SkipWhenNoValidTPM;
      String StartupKeyDrive;  
      String SupportedEnvironment;  
      String TargetDrive;  
      UInt32 Timeout;  
      Boolean WaitForEncryption;  
};  
```  

## Methods

The `SMS_TaskSequence_EnableBitLockerAction` class doesn't define any methods.

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

### `CreateRecoveryPassword`

Data type: `String`  

Access type: Read/Write  

Qualifiers: `[CommandLineArg(5), Not_Null]`

Indicates whether a recovery password should be created in Active Directory. Possible values are:

- `None`

- `AD` (default)

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

### `EncryptMethod`

Data type: `UInt32`

Access type: Read/write

Specify the disk encryption mode. Set `0` to not specify the mode, which is the default.

### `Mode`

Data type: `String`  

Access type: Read/Write  

Qualifiers: `[CommandLineArg(3), RequiredIfNull("TargetDrive")]`

Key protector mode. Possible values are:  

- `TPM`

- `Key`

- `TPMAndKey`

- `TPMAndPIN`

The default value is `null`. This property is required if `TargetDrive` is set to `null`.

### `Name`

Data type: `String`

Access type: Read/Write  

Qualifiers: `[AllowedLen("1-100")]`

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

### `PIN`

Data type: `String`  

Access type: Read/Write  

Qualifiers: `[VariableName("OSDBitLockerPIN"), Secret, AllowedLen("0-255")]`

The PIN for BitLocker encryption. Only valid if the **Mode** property is set to `"TPMAndPIN"`.

### `SkipWhenNoValidTPM`

Data type: `Boolean`

Access type: Read/write

Set `true` to skip this step for computers that don't have a TPM or when TPM isn't enabled. By default the value is `false`.

### `StartupKeyDrive`

Data type: `String`  

Access type: Read/Write  

Qualifiers: `[CommandLineArg(4)]`

Drive letter of removable USB drive on which to store key protectors. This property is ignored unless the **Mode** property is set to `Key` or `TPMAndKey`. Set this property to `null` (default) to use the first available USB drive.  

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

Drive letter of the volume on which to enable the BitLocker encryption. Set this property to `null` (default) to use the current OS volume.

### `Timeout`

Data type: `UInt32`  

Access type: Read/Write  

Qualifiers: None  

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

### `WaitForEncryption`

Data type: `Boolean`  

Access type: Read/Write  

Qualifiers: `[CommandLineArg(2), Not_Null]`

Set `true` to wait for disk encryption to complete before continuing with the task sequence. Set this property to `false` (default) to continue the task sequence while encryption proceeds in the background.

## Remarks

Class qualifiers for this class include:  

```
[CommandLine("OSDBitLocker.exe /enable \<?1: /drive:%1>\<?2: /wait:%2>\<?3: /mode:%3>\<?4: /keydrive:%4>\<?5: /pwd:%5>"),  

ActionCategory{"Disks,4,3"},ActionUI{"AdminUI.TaskSequenceEditor.dll", "Microsoft.ConfigurationManagement.AdminConsole.TaskSequenceEditor", "EnableBitLockerControl", "TaskSequenceOptionControl"},  

VariablePrefix("OSDBitLocker")]  
```

For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager class and property qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).

BitLocker requires at least two partitions on the hard drive. The first partition contains the Windows bootstrap code, and the second partition contains the OS. The bootstrap partition must remain unencrypted.

The variable prefix for this class is "OSDBitLocker".  

## Requirements

### Runtime requirements

For more information, see [Configuration Manager server runtime requirements](../../../develop/core/reqs/server-runtime-requirements.md).

### Development requirements

For more information, see [Configuration Manager server development requirements](../../../develop/core/reqs/server-development-requirements.md).

## See also

[SMS_TaskSequence_Action server WMI class](sms_tasksequence_action-server-wmi-class.md)
