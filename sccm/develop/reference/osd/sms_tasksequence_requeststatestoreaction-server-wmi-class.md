---
title: "SMS_TaskSequence_RequestStateStoreAction Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: ba604e66-6252-4856-8f2f-6b4e105fbe00
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_TaskSequence_RequestStateStoreAction Server WMI Class
The `SMS_TaskSequence_RequestStateStoreAction` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a task sequence action that requests access to a state migration point when capturing a state from a computer or restoring a state to a computer.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_RequestStateStoreAction : SMS_TaskSequence_Action  
{  
      SMS_TaskSequence_Condition Condition;  
      Boolean ContinueOnError;  
      String Description;  
      Boolean Enabled;  
      Boolean FallbackToNAA;  
      String Name;  
      String RequestType;  
      UInt32 SMPRetryCount;  
      UInt32 SMPRetryTime;  
      String SupportedEnvironment;  
      UInt32 Timeout;  
};  
```  

## Methods  
 The `SMS_TaskSequence_RequestStateStoreAction` class does not define any methods.  

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

 `Enabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `FallbackToNAA`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if the action should use the network access account (NAA) as a fallback when the computer account fails to connect to the state migration point. The default value is `false`.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [AllowedLen("1-100")]  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `RequestType`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [CommandLineArg(1), Not_Null]  

 Type of state migration point (SMP) request. Possible values are:  

-   capture  

-   restore  

 `SMPRetryCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [Global, ValueRange("0-30")]  

 The number of times that the action should try to find a state migration point before failing (global setting). The value must be between 0 and 30.  

 `SMPRetryTime`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [Global, ValueRange("0-600")]  

 The time, in seconds, that the action should wait between retry attempts (global setting).The value must be between 0 and 600.  

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

 [CommandLine("osdsmpclient.exe /%1"),VariablePrefix("OSDState"),  

 ActionCategory("UserState,1,4"),ActionUI{"AdminUI.TaskSequenceEditor.dll", "Microsoft.ConfigurationManagement.AdminConsole.TaskSequenceEditor", "RequestStateStoreControl", "TaskSequenceOptionControl"}]  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Operating System Deployment Server WMI Classes](../../../develop/reference/osd/operating-system-deployment-server-wmi-classes.md)
