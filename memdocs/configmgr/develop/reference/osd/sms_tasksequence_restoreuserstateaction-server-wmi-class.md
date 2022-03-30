---
title: "SMS_TaskSequence_RestoreUserStateAction Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 616805c9-841d-44d4-b517-dcd4d57a13da
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
description: Learn about the simplified syntax, methods, properties, and requirements of the SMS_TaskSequence_RestoreUserStateAction server class.

---
# SMS_TaskSequence_RestoreUserStateAction Server WMI Class
The `SMS_TaskSequence_RestoreUserStateAction` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a task sequence action that initiates the User State Migration Tool (USMT) to restore user state and settings to a target computer.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_RestoreUserStateAction : SMS_TaskSequence_Action  
{  
      SMS_TaskSequence_Condition Condition;  
      String ConfigFiles[];  
      Boolean ContinueOnError;  
      Boolean ContinueOnRestore;  
      String Description;  
      Boolean Enabled;  
      Boolean EnableVerboseLogging;  
      String LocalAccountPassword;  
      Boolean LocalAccounts;  
      String Mode;  
      String Name;  
      String SupportedEnvironment;  
      UInt32 Timeout;  
      String UsmtRestorePackageID;  
};  
```  

## Methods  
 The `SMS_TaskSequence_RestoreUserStateAction` class does not define any methods.  

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

 Configuration files used to capture user profiles. Set this property for customized user profile migration.  

 `ContinueOnError`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `ContinueOnRestore`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null, VariableName("OSDMigrateContinueOnRestore")]  

 `true` (default) if user state restoration should continue even if some files cannot be restored.  

 The task sequence variable associated with this property is OSDMigrateContinueOnRestore. For more information, see [OS deployment task sequence variables](../../../osd/understand/task-sequence-variables.md).  

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

 `true` to enable USMT verbose logging. The default value is `false`.  

 `LocalAccountPassword`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [VariableName("OSDMigrateLocalAccountPassword"), Secret]  

 Password for the local user account to reset for restored local user profiles.  

 The task sequence variable associated with this property is OSDMigrateLocalAccountPassword. For more information, see [OS deployment task sequence variables](../../../osd/understand/task-sequence-variables.md).  

 `LocalAccounts`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [VariableName("OSDMigrateLocalAccounts"), Not_Null]  

 `true` to restore the local computer account. The default value is `false`.  

 The task sequence variable associated with this property is OSDMigrateLocalAccounts. For more information, see [OS deployment task sequence variables](../../../osd/understand/task-sequence-variables.md).  

 `Mode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null]  

 Mode for customizing the USMT file list. Possible values are shown below. The default value is Simple.  

- Simple  

- Advanced  

  `Name`  
  Data type: `String`  

  Access type: Read/Write  

  See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

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

  `UsmtRestorePackageID`  
  Data type: `String`  

  Access type: Read/Write  

  Qualifiers: [Not_Null, TaskSequencePackage, VariableName("_OSDMigrateUsmtRestorePackageID")]  

  ID of the task sequence package containing the USMT program.  

  The task sequence variable associated with this property is _OSDMigrateUsmtRestorePackageID. For more information, see [OS deployment task sequence variables](../../../osd/understand/task-sequence-variables.md).  

## Remarks  
 Class qualifiers for this class include:  

 [CommandLine("osdmigrateuserstate.exe /apply /continueOnError:%%OSDMigrateContinueOnRestore%%"),  

 VariablePrefix("OSDMigrate"),  

 ActionCategory{"UserState,3,4"},ActionUI{"AdminUI.TaskSequenceEditor.dll", "Microsoft.ConfigurationManagement.AdminConsole.TaskSequenceEditor", "RestoreUserStateControl", "TaskSequenceOptionControl"}]  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
