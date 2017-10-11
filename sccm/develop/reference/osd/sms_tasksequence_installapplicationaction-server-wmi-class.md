---
title: "SMS_TaskSequence_InstallApplicationAction Class"
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
ms.assetid: a22fb031-891f-44ef-86d2-32291a2c64fdsearchScope: - ConfigMgr SDK
caps.latest.revision: 13
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_TaskSequence_InstallApplicationAction Server WMI Class
The `SMS_TaskSequence_InstallApplicationAction` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a task sequence action that installs an application.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_InstallApplicationAction : SMS_TaskSequence_Action  
{  
    SMS_TaskSequence_ApplicationInfo AppInfo[];  
    String ApplicationName;  
    String BaseVariableName;  
    SMS_TaskSequence_Condition Condition;  
    Boolean ContinueOnError;  
    Boolean ContinueOnInstallError;  
    String Description;  
    Boolean Enabled;  
    String Name;  
    UInt32 NumApps;  
    String RetryCount;  
    String SupportedEnvironment;  
    UInt32 Timeout;  
};  
```  

## Methods  
 The `SMS_TaskSequence_InstallApplicationAction` class does not define any methods.  

## Properties  
 `AppInfo`  
 Data type: `SMS_TaskSequence_ApplicationInfo` Array  

 Access type: Read/Write  

 Qualifiers: [variablename]  

 An array of [SMS_TaskSequence_ApplicationInfo Server WMI Class](../../../develop/reference/osd/sms_tasksequence_applicationinfo-server-wmi-class.md) class objects. Each element contains application details, such as display name, name (model name of the application) and description.  

 `ApplicationName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [commandlinearg, tasksequenceapplication]  

 Comma separated list of applications (application model names) that needs to be installed as part of the step.  

 `BaseVariableName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [commandlinearg, requiredifnull]  

 This variable specifies the base name for a set of task sequence variables that are defined for a collection or for a computer. These variables specify the applications that will be installed for that collection or computer. Each variable name consists of its common base name plus a numerical suffix starting at 01. The value for each variable must contain the name of the application and nothing else.  

 `Condition`  
 Data type: `SMS_TaskSequence_Condition`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `ContinueOnError`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `ContinueOnInstallError`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [commandlinearg, requiredifnotnull]  

 `true` to continue if there is an installation error. This property is required.  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [allowedlen]  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `Enabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [allowedlen]  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `NumApps`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [variablename]  

 Size of the array indicated by the `AppInfo` property. The task sequence variable associated with this property is `OSDAppCount`.  

 `RetryCount`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [retrycount]  

 The number of retries. The default value is 2.  

 `SupportedEnvironment`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null, valuemap]  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `Timeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

## Remarks  
 Class qualifiers for this class include:  

 [CommandLine("smsappinstall.exe /app:%1 /basevar:%2 /continueOnError:%3"),  

 ActionCategory{"Software,1,2"},     ActionUI{"AdminUI.TaskSequenceEditor.dll", "Microsoft.ConfigurationManagement.AdminConsole.TaskSequenceEditor", "InstallApplicationControl", "TaskSequenceOptionControl"}]  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
