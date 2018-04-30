---
title: "SMS_TaskSequence_ApplyWindowsSettingsAction Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 62494ccd-da4c-430d-bad5-ed18c3067240
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_TaskSequence_ApplyWindowsSettingsAction Server WMI Class
The `SMS_TaskSequence_ApplyWindowsSettingsAction` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a task sequence action that applies Windows settings configuration information for the target computer.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_ApplyWindowsSettingsAction : SMS_TaskSequence_Action  
{  
    String AdminPassword;  
    String ComputerName;  
    SMS_TaskSequence_Condition Condition;  
    Boolean ContinueOnError;  
    String Description;  
    Boolean Enabled;  
    String Name;  
    String ProductKey;  
    Boolean RandomAdminPassword;  
    String RegisteredOrgName;  
    String RegisteredUserName;  
    UInt32 ServerLicenseConnectionLimit;  
    String ServerLicenseMode;  
    String SupportedEnvironment;  
    UInt32 Timeout;  
    String TimeZone;  
};  
```  

## Methods  
 The `SMS_TaskSequence_ApplyWindowsSettingsAction` class does not define any methods.  

## Properties  
 `AdminPassword`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [VariableName("OSDLocalAdminPassword"), Secret, AllowedLen("0-255")]  

 Local administrator password. The name can be between 0 and 255 characters in length. This property must be set, but it is ignored if the `RandomAdminPassword` property is set to `e`.  

 The task sequence variable associated with this property is OSDLocalAdminPassword. For more information, see the MSDN documentation for [Operating System Deployment Task Sequence Variables](http://go.microsoft.com/fwlink/?LinkId=100711).  

 `ComputerName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name assigned to the target computer. The default name is "%_SMSTSMachineName%".  

 `Condition`  
 Data type: `SMS_TaskSequence_Condition`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `ContinueOnError`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [AllowedLen("0-255")]  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `Enabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [AllowedLen("1-100")]  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `ProductKey`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [QuasiSecret]  

 The product code for the new operating system.  

 `RandomAdminPassword`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 `true` (default) to set the administrator password to a randomly generated value and disable the account in the operating system that is being deployed. The local administrator account, specified by `AdminPassword`, is disabled on the target computer. Set this property to `false` to enable the local administrator account and set the password as specified by the `AdminPassword` property. This property must be set.  

 `RegisteredOrgName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null, AllowedLen("1-255")]  

 Registered organization name in the new operating system. The name length can be between 1 and 255 characters. This property must be set.  

 `RegisteredUserName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null, AllowedLen("1-255")]  

 Registered user name in the new operating system. The name length can be between 1 and 255 characters. This property must be set.  

 `ServerLicenseConnectionLimit`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [ValueRange("5-9999")]  

 Limit on server license connections. The value can be between 5 and 9999. Use this property to configure server licensing on Windows Server 2003.  

 `ServerLicenseMode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The server licensing mode. Possible values for Windows Server 2003 are:  

-   PerSeat  

-   PerServer  

 `SupportedEnvironment`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null:ToInstance]  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 The default value of this property for this task sequence action is WinPE.  

 `Timeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `TimeZone`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null]  

 Time zone for the new operating system. This property must be set to an English language string. A non-English localized string causes the time zone setting to fail and default to Universal Coordinated Time (UTC).  

## Remarks  
 Class qualifiers for this class include:  

 [CommandLine("osdwinsettings.exe /config"),VariablePrefix("OSD"),  

 ActionCategory{"Settings,4,7"},ActionUI{"AdminUI.TaskSequenceEditor.dll", "Microsoft.ConfigurationManagement.AdminConsole.TaskSequenceEditor", "ApplyWindowsSettingsControl", "TaskSequenceOptionControl"}]  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Operating System Deployment Server WMI Classes](../../../develop/reference/osd/operating-system-deployment-server-wmi-classes.md)
