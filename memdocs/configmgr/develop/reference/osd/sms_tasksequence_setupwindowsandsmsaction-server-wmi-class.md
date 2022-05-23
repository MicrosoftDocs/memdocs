---
description: Learn how to use Configuration Manager SMS_TaskSequence_SetupWindowsAndSMSAction Windows Management Instrumentation (WMI) class to represent a task sequence action that specifies the additional installation properties.
title: "SMS_TaskSequence_SetupWindowsAndSMSAction Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 227e3d90-f685-48f8-b2fe-5950f7edadd3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_TaskSequence_SetupWindowsAndSMSAction Server WMI Class
The `SMS_TaskSequence_SetupWindowsAndSMSAction` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a task sequence action that specifies the additional installation properties that should be used when installing the Configuration Manager client.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_SetupWindowsAndSMSAction : SMS_TaskSequence_Action  
{  
      String ClientInstallProperties;  
      String ClientPackageID;  
      String ClientPreProductionPackageID;  
      SMS_TaskSequence_Condition Condition;  
      Boolean ContinueOnError;  
      String Description;  
      Boolean Enabled;  
      String Name;  
      String SupportedEnvironment;  
      UInt32 Timeout;  
};  
```  

## Methods  
 The `SMS_TaskSequence_SetupWindowsAndSMSAction` class does not define any methods.  

## Properties  
 `ClientInstallProperties`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [VariableName("SMSClientInstallProperties")]  

 List of Windows Installer properties to use when installing the Configuration Manager client.  

 The task sequence variable associated with this property is SMSClientInstallProperties. For more information, see [How to Set an Operating System Deployment Task Sequence Variable](../../../develop/osd/how-to-set-an-operating-system-deployment-task-sequence-variable.md).  

 `ClientPackageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null, TaskSequencePackage, VariableName("_SMSClientPackageID")]  

 ID of the package containing the Configuration Manager client.  

 The task sequence variable associated with this property is _SMSClientPackageID. For more information, see [How to Set an Operating System Deployment Task Sequence Variable](../../../develop/osd/how-to-set-an-operating-system-deployment-task-sequence-variable.md).  

 `ClientPreProductionPackageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [TaskSequencePackage, VariableName("_SMSClientPreProductionPackageID")]  

 ID of the pre-production package containing the Configuration Manager client. The default value is `null`.  

 The task sequence variable associated with this property is _SMSClientPreProductionPackageID. For more information, see [How to Set an Operating System Deployment Task Sequence Variable](../../../develop/osd/how-to-set-an-operating-system-deployment-task-sequence-variable.md).  

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

 `SupportedEnvironment`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null:ToInstance]  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `Timeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

## Remarks  
 Class qualifiers for this class include:  

 [CommandLine("OSDSetupWindows.exe"),  

 ActionCategory{"Images,3,5"},ActionUI{"AdminUI.TaskSequenceEditor.dll", "Microsoft.ConfigurationManagement.AdminConsole.TaskSequenceEditor", "SetupWindowsAndSmsControl", "TaskSequenceOptionControl"}]  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
