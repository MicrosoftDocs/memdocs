---
title: "SMS_TaskSequence_InstallSoftwareAction Class"
titleSuffix: "Configuration Manager"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: e6679d3b-6019-4404-bdb1-62ec5ae17eddsearchScope: - ConfigMgr SDK
caps.latest.revision: 11
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_TaskSequence_InstallSoftwareAction Server WMI Class
The `SMS_TaskSequence_InstallSoftwareAction` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a task sequence action that installs software.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_InstallSoftwareAction : SMS_TaskSequence_Action  
{  
      String BaseVariableName;  
      SMS_TaskSequence_Condition Condition;  
      Boolean ContinueOnError;  
      Boolean ContinueOnInstallError;  
      String Description;  
      Boolean Enabled;  
      String Name;  
      String PackageID;  
      String ProgramName;  
      String SupportedEnvironment;  
      UInt32 Timeout;  
};  
```  

## Methods  
 The `SMS_TaskSequence_InstallSoftwareAction` class does not define any methods.  

## Properties  
 `BaseVariableName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [RequiredIfNull("PackageID"), CommandLineArg(3)]  

 The base task sequence variable name. This property is required for installing multiple programs if `PackageID` is set to `null`.  

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

 `ContinueOnInstallError`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [RequiredIfNotNull("BaseVariableName"), CommandLineArg(4)]  

 `true` to continue if there is an installation error. This property is required if `BaseVariableName` is not set to `null`.  

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

 `PackageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [CommandLineArg(1), TaskSequencePackage]  

 The ID of the task sequence package to use for installing the program. Set this property to `null` to install multiple programs.  

 `ProgramName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [RequiredIfNotNull("PackageID"), VariableName("_SMSSWDProgramName"), TaskSequenceProgram("PackageID")]  

 The program in the package to install. This property is required if `PackageID` is not set to `null`.  

 The task sequence variable associated with this property is _SMSSWDProgramName. For more information, see the MSDN documentation for [Operating System Deployment Task Sequence Variables](http://go.microsoft.com/fwlink/?LinkId=100711).  

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

## Remarks  
 Class qualifiers for this class include:  

 [CommandLine("smsswd.exe /pkg:%1 /install /basevar:%3 /continueOnError:%4"),  

 ActionCategory{"Software,2,2"},ActionUI{"AdminUI.TaskSequenceEditor.dll", "Microsoft.ConfigurationManagement.AdminConsole.TaskSequenceEditor", "InstallSoftwareDistributionControl", "TaskSequenceOptionControl"}]  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Operating System Deployment Server WMI Classes](../../../develop/reference/osd/operating-system-deployment-server-wmi-classes.md)   
 [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md)
