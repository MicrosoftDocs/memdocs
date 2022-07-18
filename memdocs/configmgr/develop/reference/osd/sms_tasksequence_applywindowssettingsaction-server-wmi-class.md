---
title: SMS_TaskSequence_ApplyWindowsSettingsAction class
description: The SMS_TaskSequence_ApplyWindowsSettingsAction WMI class is an SMS Provider server class in Configuration Manager. It represents a task sequence action that applies Windows settings configuration information for the target computer.
titleSuffix: Configuration Manager
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 62494ccd-da4c-430d-bad5-ed18c3067240
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
---

# SMS_TaskSequence_ApplyWindowsSettingsAction server WMI class

The `SMS_TaskSequence_ApplyWindowsSettingsAction` WMI class is an SMS Provider server class in Configuration Manager. It represents a task sequence action that applies Windows settings configuration information for the target computer.  

The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```MOF
Class SMS_TaskSequence_ApplyWindowsSettingsAction : SMS_TaskSequence_Action  
{  
    String AdminPassword;  
    String ComputerName;  
    SMS_TaskSequence_Condition Condition;  
    Boolean ContinueOnError;  
    String Description;  
    Boolean Enabled;  
    String InputLocale;
    String Name;  
    String ProductKey;  
    Boolean RandomAdminPassword;  
    String RegisteredOrgName;  
    String RegisteredUserName;  
    UInt32 ServerLicenseConnectionLimit;  
    String ServerLicenseMode;  
    String SystemLocale;
    String SupportedEnvironment;  
    UInt32 Timeout;  
    String TimeZone;  
    string UILanguage;
    string UILanguageFallback;
    string UserLocale;

};  
```  

## Methods

The `SMS_TaskSequence_ApplyWindowsSettingsAction` class doesn't define any methods.

## Properties

### `AdminPassword`

Data type: `String`  

Access type: Read/Write  

Qualifiers: `[VariableName("OSDLocalAdminPassword"), Secret, AllowedLen("0-255")]`

The local Administrator password. The name can be between 0 and 255 characters in length. This property must be set, but it's ignored if the `RandomAdminPassword` property is set to `true`.

The task sequence variable associated with this property is [OSDLocalAdminPassword](../../../osd/understand/task-sequence-variables.md#OSDLocalAdminPassword).

### `ComputerName`

Data type: `String`  

Access type: Read/Write  

Qualifiers: None  

Name assigned to the target computer. The default value is `"%_SMSTSMachineName%"`.

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

### `InputLocale`

Data type: `String`

Access type: Read/write

Specify the default keyboard layout. For more information on this Windows setup answer file value, see [Microsoft-Windows-International-Core](/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core).

### `Name`

Data type: `String`  

Access type: Read/Write  

Qualifiers: `[AllowedLen("1-100")]`

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

### `ProductKey`

Data type: `String`  

Access type: Read/Write  

Qualifiers: `[QuasiSecret]`

The product code for the new OS.

### `RandomAdminPassword`

Data type: `Boolean`  

Access type: Read/Write  

Qualifiers: `[not_null]`

- Set `true` (default) to set the Administrator password to a randomly generated value. It also disables the account in the new OS.
- Set `false` to enable the local Administrator account. It also sets the password as specified by the `AdminPassword` property.

This property is required.

### `RegisteredOrgName`

Data type: `String`  

Access type: Read/Write  

Qualifiers: `[Not_Null, AllowedLen("1-255")]`

Registered organization name in the new OS. The name length can be between 1 and 255 characters. This property is required.

### `RegisteredUserName`

Data type: `String`  

Access type: Read/Write  

Qualifiers: `[Not_Null, AllowedLen("1-255")]`

Registered user name in the new OS. The name length can be between 1 and 255 characters. This property is required.

### `ServerLicenseConnectionLimit`

Data type: `UInt32`  

Access type: Read/Write  

Qualifiers: `[ValueRange("5-9999")]`

Limit on server license connections. The value can be between 5 and 9999. Use this property to configure server licensing on Windows Server.

### `ServerLicenseMode`

Data type: `String`  

Access type: Read/Write  

Qualifiers: None  

The server licensing mode. Possible values for Windows Server are:  

- `PerSeat`  

- `PerServer`  

### `SystemLocale`

Data type: `String`

Access type: Read/write

Specify system locale. For more information on this Windows setup answer file value, see [Microsoft-Windows-International-Core](/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core).

### `SupportedEnvironment`

Data type: `String`  

Access type: Read/Write  

Qualifiers: `[Not_Null:ToInstance]`

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).

The default value of this property for this task sequence action is WinPE.

### `Timeout`

Data type: `UInt32`  

Access type: Read/Write  

Qualifiers: None  

For more information, see [SMS_TaskSequence_Action server WMI class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

### `TimeZone`

Data type: `String`  

Access type: Read/Write  

Qualifiers: `[Not_Null]`

Time zone for the new OS. Set this property to an English language string. A non-English localized string causes the time zone setting to fail and default to Universal Coordinated Time (UTC).  

### `UILanguage`

Data type: `String`

Access type: Read/write

Specify the Windows UI language. For more information on this Windows setup answer file value, see [Microsoft-Windows-International-Core](/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core).

### `UILanguageFallback`

Data type: `String`

Access type: Read/write

Specify the fallback language for the Windows UI. For more information on this Windows setup answer file value, see [Microsoft-Windows-International-Core](/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core).

### `UserLocale`

Data type: `String`

Access type: Read/write

Specify the user locale. For more information on this Windows setup answer file value, see [Microsoft-Windows-International-Core](/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core).

## Remarks

Class qualifiers for this class include:  

```
[CommandLine("osdwinsettings.exe /config"),VariablePrefix("OSD"),  

ActionCategory{"Settings,4,7"},ActionUI{"AdminUI.TaskSequenceEditor.dll", "Microsoft.ConfigurationManagement.AdminConsole.TaskSequenceEditor", "ApplyWindowsSettingsControl", "TaskSequenceOptionControl"}]  
```

For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager class and property     qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).

## Requirements  

### Runtime requirements

For more information, see [Configuration Manager server runtime requirements](../../../develop/core/reqs/server-runtime-requirements.md).

### Development requirements

For more information, see [Configuration Manager server development requirements](../../../develop/core/reqs/server-development-requirements.md).
