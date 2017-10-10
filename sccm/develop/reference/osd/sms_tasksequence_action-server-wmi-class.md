---
title: "SMS_TaskSequence_Action Class"
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
ms.assetid: 12a29d69-ac46-45ea-b540-52a85c4c885fsearchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_TaskSequence_Action Server WMI Class
The `SMS_TaskSequence_Action` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that serves as the abstract base class for all task sequence actions.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_Action : SMS_TaskSequence_Step  
{  
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
 The `SMS_TaskSequence_Action` class does not define any methods.  

## Properties  
 `Condition`  
 Data type: `SMS_TaskSequence_Condition`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Step Server WMI Class](../../../develop/reference/osd/sms_tasksequence_step-server-wmi-class.md).  

 `ContinueOnError`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Step Server WMI Class](../../../develop/reference/osd/sms_tasksequence_step-server-wmi-class.md).  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [AllowedLen("0-255")]  

 See [SMS_TaskSequence_Step Server WMI Class](../../../develop/reference/osd/sms_tasksequence_step-server-wmi-class.md).  

 `Enabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Step Server WMI Class](../../../develop/reference/osd/sms_tasksequence_step-server-wmi-class.md).  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [AllowedLen("1-100")]  

 See [SMS_TaskSequence_Step Server WMI Class](../../../develop/reference/osd/sms_tasksequence_step-server-wmi-class.md).  

 `SupportedEnvironment`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null:ToInstance]  

 The environment required to run the task sequence action. Possible values are:  

-   WinPE  

-   FullOS  

-   WinPEandFullOS  

 The default value is WinPEandFullOS.  

 `Timeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The user-specified timeout value, in seconds. If the step does not finish in the specified time period, the client execution engine explicitly terminates the step.  

## Remarks  
 Class qualifiers for this class include:  

-   Abstract  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 Configuration Manager supports a number of built-in action classes that are derived from `SMS_TaskSequence_Action` that represent operations available to the administrator in the Configuration Manager console. An example is [SMS_TaskSequence_ApplyDataImageAction Server WMI Class](../../../develop/reference/osd/sms_tasksequence_applydataimageaction-server-wmi-class.md).  

 By using the Operating System Deployment task sequence object model, your application can create and use task sequences that use the built-in actions. For more information, see About Operating System Deployment Task Sequences.  

 You also use this class to create a custom task sequence action. For more information, see About Configuration Manager Custom Actions  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Operating System Deployment Server WMI Classes](../../../develop/reference/osd/operating-system-deployment-server-wmi-classes.md)   
 [SMS_TaskSequence_Step Server WMI Class](../../../develop/reference/osd/sms_tasksequence_step-server-wmi-class.md)   
 [Configuration Manager Operating System Deployment](../../../develop/reference/osd/operating-system-deployment-classes.md)
