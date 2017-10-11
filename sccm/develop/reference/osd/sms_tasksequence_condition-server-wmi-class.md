---
title: "SMS_TaskSequence_Condition Class"
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
ms.assetid: e0d3dae7-c185-4915-8a3a-e45e529cca9asearchScope: - ConfigMgr SDK
caps.latest.revision: 12
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_TaskSequence_Condition Server WMI Class
The `SMS_TaskSequence_Condition Server WMI Class` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that defines a condition for an operating system deployment step. This class is the base class for all conditions.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_Condition  
{  
      SMS_TaskSequence_ConditionOperand Operands[];  
};  
```  

## Methods  
 The `SMS_TaskSequence_Condition` class does not define any methods.  

## Properties  
 `Operands`  
 Data type: `SMS_TaskSequence_ConditionOperand` Array  

 Access type: Read/Write  

 Qualifiers: [Not_Null:ToInstance]  

 [SMS_TaskSequence_ConditionOperand Server WMI Class](../../../develop/reference/osd/sms_tasksequence_conditionoperand-server-wmi-class.md) objects indicating condition operands. For example, the array can contain a single expression, such as an [SMS_TaskSequence_WMIConditionExpression Server WMI Class](../../../develop/reference/osd/sms_tasksequence_wmiconditionexpression-server-wmi-class.md) object. A more complicated condition array can contain a combination of expressions, operators, and operating system condition groups.  

## Remarks  
 There are no class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 This class is the root for a hierarchy of operator and expression objects that represent the condition that determines whether a step or group or action should be executed. This class implies an AND operator. Therefore, all child operands in the array must be `true` for the overall condition to be `true`.  

 For example, you might want to process a step on a computer that must have Microsoft Office 2007 and Windows Vista installed. In this case, you add to the `Operands` property array, a [SMS_TaskSequence_SoftwareConditionExpression Server WMI Class](../../../develop/reference/osd/sms_tasksequence_softwareconditionexpression-server-wmi-class.md) that defines Microsoft Office 2007 and a [SMS_TaskSequence_OSConditionGroup Server WMI Class](../../../develop/reference/osd/sms_tasksequence_osconditiongroup-server-wmi-class.md) that defines Windows Vista. The overall condition evaluates to `true` only when the two operands are `true`. That is, when Microsoft Office 2007 is installed on a computer with Windows Vista installed.  

 For more information about conditions, see Operating System Deployment Task Sequence Object Model.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Operating System Deployment Server WMI Classes](../../../develop/reference/osd/operating-system-deployment-server-wmi-classes.md)   
 [SMS_TaskSequence_ConditionOperand Server WMI Class](../../../develop/reference/osd/sms_tasksequence_conditionoperand-server-wmi-class.md)   
 [SMS_TaskSequence_WMIConditionExpression Server WMI Class](../../../develop/reference/osd/sms_tasksequence_wmiconditionexpression-server-wmi-class.md)
