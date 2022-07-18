---
title: "SMS_TaskSequence_JoinDomainWorkgroupAction Class"
titleSuffix: "Configuration Manager"
description: "The SMS_TaskSequence_JoinDomainWorkgroupAction WMI class is an SMS Provider server class that represents a task sequence action that joins a Windows domain or a Windows workgroup."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 43d47e35-4093-4aa8-9d8e-5c02fd209373
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_TaskSequence_JoinDomainWorkgroupAction Server WMI Class
The `SMS_TaskSequence_JoinDomainWorkgroupAction` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a task sequence action that joins a Windows domain or a Windows workgroup.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_JoinDomainWorkgroupAction : SMS_TaskSequence_Action  
{  
      SMS_TaskSequence_Condition Condition;  
      Boolean ContinueOnError;  
      String Description;  
      String DomainName;  
      String DomainOUName;  
      String DomainPassword;  
      String DomainUsername;  
      Boolean Enabled;  
      String Name;  
      Boolean SkipReboot;  
      String SupportedEnvironment;  
      UInt32 Timeout;  
      UInt32 Type;  
      String WorkgroupName;  
};  
```  

## Methods  
 The `SMS_TaskSequence_JoinDomainWorkgroupAction` class does not define any methods.  

## Properties  
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

 `DomainName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [AllowedLen("1-255")]  

 Name of the domain for the target computer. The name length can be between 1 and 255 characters. Set this property if the `Type` property is set to 0.  

 `DomainOUName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [AllowedLen("0-32767")]  

 The name of the Active Directory organizational unit (OU) to join. The name length can be between 0 and 32767 characters. Set this property if the `Type` property is set to 0.  

 `DomainPassword`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [VariableName("OSDJoinPassword"), Secret]  

 Password of the account specified by `DomainUsername`. Set this property if the `Type` property is set to 0.  

 The task sequence variable associated with this property is OSDJoinPassword. For more information, see [OS deployment task sequence variables](../../../osd/understand/task-sequence-variables.md).  

 `DomainPassword` might be required to disjoin from the computer's domain.  

 `DomainUsername`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [VariableName("OSDJoinAccount")]  

 Account that should be used by the target computer to join a Windows domain, with appropriate domain join rights. Set this property if the `Type` property is set to 0.  

 The task sequence variable associated with this property is OSDJoinAccount. For more information, see [OS deployment task sequence variables](../../../osd/understand/task-sequence-variables.md).

 `DomainUserName` may be required to disjoin from the computer's domain.  

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

 `SkipReboot`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` to skip reboot after the network join action is complete.  

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

 `Type`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null, VariableName("OSDJoinType")]  

 The type of network join action required of the target computer. Possible values are:  

| Value | Network join type |  
| ----- | ----------------- |  
|0|Domain|  
|1|Workgroup|  

 The task sequence variable associated with this property is OSDJoinType. For more information, see [OS deployment task sequence variables](../../../osd/understand/task-sequence-variables.md).

 `WorkgroupName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [AllowedLen("1-32")]  

 Name of the workgroup to join. The name length can be between 1 and 32 characters. Set this property if the `Type` property is set to 1.  

## Remarks  
 Class qualifiers for this class include:  

 [CommandLine("osdjoin.exe /type:%%OSDJoinType%%"), VariablePrefix("OSDJoin"),  

 ActionCategory{"General,4,1"},ActionUI{"AdminUI.TaskSequenceEditor.dll", "Microsoft.ConfigurationManagement.AdminConsole.TaskSequenceEditor", "JoinDomainControl", "TaskSequenceOptionControl"}]  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md)
