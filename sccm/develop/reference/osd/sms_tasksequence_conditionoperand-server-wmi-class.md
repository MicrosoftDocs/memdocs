---
title: "SMS_TaskSequence_ConditionOperand Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 4f0075f9-d759-4edb-b0cd-65cb64827aee
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_TaskSequence_ConditionOperand Server WMI Class
The `SMS_TaskSequence_ConditionOperand` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager. This class is the abstract base class for operators and expressions that are used by task sequence steps.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_ConditionOperand  
{  
};  
```  

## Methods  
 The `SMS_TaskSequence_ConditionOperand` class does not define any methods.  

## Properties  
 The `SMS_TaskSequence_ConditionOperand` class does not define any properties.  

## Remarks  
 Class qualifiers for this class include:  

-   Abstract  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 `SMS_TaskSequence_ConditionOperand` derived classes are used to define condition expressions and operators that determine whether a task sequence step should be run. There are two derived classes.  

## SMS_TaskSequence_ConditionExpression  
 [SMS_TaskSequence_ConditionExpression Server WMI Class](../../../develop/reference/osd/sms_tasksequence_conditionexpression-server-wmi-class.md) is the base class for an expression that must evaluate to `true` before the step can be processed. For example, the derived class [SMS_TaskSequence_RegistryConditionExpression Server WMI Class](../../../develop/reference/osd/sms_tasksequence_registryconditionexpression-server-wmi-class.md) defines an expression for the existence of a registry key.  

## SMS_TaskSequence_ConditionOperator  
 [SMS_TaskSequence_ConditionOperator Server WMI Class](../../../develop/reference/osd/sms_tasksequence_conditionoperator-server-wmi-class.md) defines a Boolean operator and the expressions that are used to evaluate nested expressions.  

 These classes can be used to define complex conditions such as `Expression1 and (Expression2 or Expression3)`. For more information, see Operating System Deployment Task Sequence Object Model.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Operating System Deployment Server WMI Classes](../../../develop/reference/osd/operating-system-deployment-server-wmi-classes.md)   
 [SMS_TaskSequence_ConditionOperator Server WMI Class](../../../develop/reference/osd/sms_tasksequence_conditionoperator-server-wmi-class.md)   
 [SMS_TaskSequence_ConditionExpression Server WMI Class](../../../develop/reference/osd/sms_tasksequence_conditionexpression-server-wmi-class.md)
