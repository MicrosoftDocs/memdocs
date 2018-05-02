---
title: "SMS_TaskSequence_CaptureUserStateAction Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: f039cd2e-95f6-4c34-b7f8-d0cc9779f610
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_TaskSequence_CaptureUserStateAction Server WMI Class
The `SMS_TaskSequence_CaptureUserStateAction` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a task sequence action that uses the User State Migration Tool (USMT) to capture user state and settings from the target computer.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_CaptureUserStateAction : SMS_TaskSequence_Action  
{  
      SMS_TaskSequence_Condition Condition;  
      String ConfigFiles[];  
      Boolean ContinueOnError;  
      Boolean ContinueOnLockedFiles;  
      String Description;  
      Boolean Enabled;  
      Boolean EnableVerboseLogging;  
      String FileAccess;  
      String Mode;  
      String Name;  
      Boolean OfflineUserState;  
      Boolean SkipEncryptedFiles;  
      String SupportedEnvironment;  
      UInt32 Timeout;  
      Boolean UseHardlinks;  
      String UsmtPackageID;  
};  
```  

## Methods  
 The `SMS_TaskSequence_CaptureUserStateAction` class does not define any methods.  

## Properties  
 `Condition`  
 Data type: `SMS_TaskSequence_Condition`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `ConfigFiles`  
 Data type: `String` Array  

 Access type: Read/Write  

 Qualifiers: None  

 The configuration files used to capture user profiles. Set this property for customized user profile migration.  

 `ContinueOnError`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `ContinueOnLockedFiles`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [Not_Null, VariableName("OSDMigrateContinueOnLockedFiles")]  

 `true` (default) to allow the capture user state action to proceed even if some files cannot be captured. This property is required.  

 The task sequence variable associated with this property is OSDMigrateContinueOnLockedFiles. For more information, see the MSDN documentation for [Operating System Deployment Task Sequence Variables](http://go.microsoft.com/fwlink/?LinkId=100711).  

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

 `EnableVerboseLogging`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [Not_Null]  

 `true` to enable verbose logging for the USMT. The default value is `false`. This property is required.  

 `FileAccess`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null]  

 FileAccess ….  Possible values are:  

-   Normal (default)  

-   VSS  

 `Mode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null]  

 Mode that allows customization of the files captured by the USMT. Possible values are:  

-   Simple (default)  

-   Advanced  

 This property is required.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [AllowedLen("1-100")]  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `OfflineUserState`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [Not_Null, VariableName("_OSDMigrateOfflineUserState")]  

 `true` to migrate offline user state.  The default value is `false`.  

 `SkipEncryptedFiles`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [Not_Null, VariableName("OSDMigrateSkipEncryptedFiles")]  

 `true` to skip encrypted files. The default value is `false`.  

 The task sequence variable associated with this property is OSDMigrateSkipEncryptedFiles. For more information, see the MSDN documentation for [Operating System Deployment Task Sequence Variables](http://go.microsoft.com/fwlink/?LinkId=100711).  

 `SupportedEnvironment`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null:ToInstance]  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 The default value of this property for this task sequence action is FullOS.  

 `Timeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `UseHardlinks`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [Not_Null, VariableName("_OSDMigrateUseHardlinks")]  

 `true` to ….  The default value is `false`.  

 `UsmtPackageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null, VariableName("_OSDMigrateUsmtPackageID"), TaskSequencePackage]  

 The ID of the Configuration Manager package that contains USMT binaries. This property is required.  

 The task sequence variable associated with this property is _OSDMigrateUsmtPackageID. For more information, see the MSDN documentation for [Operating System Deployment Task Sequence Variables](http://go.microsoft.com/fwlink/?LinkId=100711).  

## Remarks  
 Class qualifiers for this class include:  

 [CommandLine("osdmigrateuserstate.exe /collect /continueOnError:%%OSDMigrateContinueOnLockedFiles%% /skipefs:%%OSDMigrateSkipEncryptedFiles%%"),VariablePrefix("OSDMigrate"),  

 ActionCategory{"UserState,2,4"},ActionUI{"AdminUI.TaskSequenceEditor.dll", "Microsoft.ConfigurationManagement.AdminConsole.TaskSequenceEditor", "CaptureUserStateControl", "TaskSequenceOptionControl"}]  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Operating System Deployment Server WMI Classes](../../../develop/reference/osd/operating-system-deployment-server-wmi-classes.md)   
 [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md)
