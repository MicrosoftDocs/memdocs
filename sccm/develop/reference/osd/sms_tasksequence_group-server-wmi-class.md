---
title: "SMS_TaskSequence_Group Class"
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
ms.assetid: 1f6c8938-6056-4057-9e28-3191ea9319d2searchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_TaskSequence_Group Server WMI Class
The `SMS_TaskSequence_Group` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a group of steps in a task sequence.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_Group : SMS_TaskSequence_Step  
{  
      SMS_TaskSequence_Condition Condition;  
      Boolean ContinueOnError;  
      String Description;  
      Boolean Enabled;  
      String Name;  
      SMS_TaskSequence_Step Steps[];  
};  
```  

## Methods  
 The `SMS_TaskSequence_Group` class does not define any methods.  

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

 `Steps`  
 Data type: `SMS_TaskSequence_Step` Array  

 Access type: Read/Write  

 Qualifiers: None  

 [SMS_TaskSequence_Step Server WMI Class](../../../develop/reference/osd/sms_tasksequence_step-server-wmi-class.md) objects representing the steps in the group.  

## Remarks  
 There are no class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 A group is a set of one or more task sequence actions or groups. Because a group can contain further groups, it is possible to create nested groups.  

 You can use groups to associate multiple steps with a condition. For example, you can restrict a group of steps to run only with Windows Vista.  

 Your application can set up a group of task sequence steps as described in How to Create an Operating System Deployment Task Sequence Group. Further information is provided in How to Add a Step to an Operating System Deployment Group.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Operating System Deployment Server WMI Classes](../../../develop/reference/osd/operating-system-deployment-server-wmi-classes.md)   
 [SMS_TaskSequence_Step Server WMI Class](../../../develop/reference/osd/sms_tasksequence_step-server-wmi-class.md)
