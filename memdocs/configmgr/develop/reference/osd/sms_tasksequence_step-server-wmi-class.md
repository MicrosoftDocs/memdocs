---
title: "SMS_TaskSequence_Step Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 8115f7ad-c818-437e-bab3-da7654c02b43
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_TaskSequence_Step Server WMI Class
The `SMS_TaskSequence_Step` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager. This class serves as an abstract base class that represents a single step in a task sequence.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_Step  
{  
      SMS_TaskSequence_Condition Condition;  
      Boolean ContinueOnError;  
      String Description;  
      Boolean Enabled;  
      String Name;  
};  
```  

## Methods  
 The `SMS_TaskSequence_Step` class does not define any methods.  

## Properties  
 `Condition`  
 Data type: `SMS_TaskSequence_Condition`  

 Access type: Read/Write  

 Qualifiers: None  

 Optional. An [SMS_TaskSequence_Condition Server WMI Class](../../../develop/reference/osd/sms_tasksequence_condition-server-wmi-class.md) object representing a condition that can be used to determine if the step should be processed.  

 `ContinueOnError`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` to continue the task sequence even if the step fails.  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [AllowedLen("0-255")]  

 Optional. The description of the step. The description length can be between 0 and 255 characters.  

 `Enabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if the step should be run. Set this property to `false` to ignore the step completely.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [AllowedLen("1-100")]  

 The name of the step. The name length can be between 1 and 100 characters.  

## Remarks  
 Class qualifiers for this class include:  

- Abstract  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

  Each step in the task sequence is one of the following:  

- An individual action that is run on a computer, represented by a [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md) or derived class. For example, the [SMS_TaskSequence_InstallSoftwareAction Server WMI Class](../../../develop/reference/osd/sms_tasksequence_installsoftwareaction-server-wmi-class.md) class represents an action that specifies a package and a program to install as part of a task sequence.  

- A set of actions in a group, represented by [SMS_TaskSequence_Group Server WMI Class](../../../develop/reference/osd/sms_tasksequence_group-server-wmi-class.md). Groups are useful ways to organize actions. For example, to conditionally process a set of actions, you could organize the actions into a group and add a condition to the group.  

  Each step can be associated with a condition, represented by [SMS_TaskSequence_Condition Server WMI Class](../../../develop/reference/osd/sms_tasksequence_condition-server-wmi-class.md) that determines whether the step is processed.  

  For more information, see Operating System Deployment Task Sequence Object Model.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_TaskSequence Server WMI Class](../../../develop/reference/osd/sms_tasksequence-server-wmi-class.md)   
 [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md)   
 [SMS_TaskSequence_Condition Server WMI Class](../../../develop/reference/osd/sms_tasksequence_condition-server-wmi-class.md)   
 [SMS_TaskSequence_Group Server WMI Class](../../../develop/reference/osd/sms_tasksequence_group-server-wmi-class.md)
