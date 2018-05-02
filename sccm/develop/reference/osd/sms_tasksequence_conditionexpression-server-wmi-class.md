---
title: "SMS_TaskSequence_ConditionExpression Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 91221db4-0420-4e3a-ac58-7d016ae4467f
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_TaskSequence_ConditionExpression Server WMI Class
The `SMS_TaskSequence_ConditionExpression` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that is the abstract base class for all condition expressions.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_ConditionExpression : SMS_TaskSequence_ConditionOperand  
{  
};  
```  

## Methods  
 The `SMS_TaskSequence_ConditionExpression` class does not define any methods.  

## Properties  
 The `SMS_TaskSequence_ConditionExpression` class does not define any properties.  

## Remarks  
 Class qualifiers for this class include:  

-   Abstract  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 `SMS_TaskSequence_ConditionExpression` is the abstract base class for an expression that must evaluate to `true`, for the task sequence step to be processed. For example, the derived class [SMS_TaskSequence_RegistryConditionExpression Server WMI Class](../../../develop/reference/osd/sms_tasksequence_registryconditionexpression-server-wmi-class.md) defines an expression for the existence of a registry key.  

 An `SMS_TaskSequence_ConditionExpression` is stored in a condition's ([SMS_TaskSequence_Condition Server WMI Class](../../../develop/reference/osd/sms_tasksequence_condition-server-wmi-class.md)) `Operands` array property, which defines the list of condition operands.  

> [!NOTE]
>  In a task sequence step ([SMS_TaskSequence_Step Server WMI Class](../../../develop/reference/osd/sms_tasksequence_step-server-wmi-class.md)), the condition is defined in the `Condition` property.  

 Alternatively, more complex conditions are created by adding a [SMS_TaskSequence_ConditionOperator Server WMI Class](../../../develop/reference/osd/sms_tasksequence_conditionoperator-server-wmi-class.md) object to the condition's `Operands` array property, and by adding expressions and operators to the added [SMS_TaskSequence_ConditionOperator Server WMI Class](../../../develop/reference/osd/sms_tasksequence_conditionoperator-server-wmi-class.md)`Operands` array.  

 For more information, see Operating System Deployment Task Sequence Object Model.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Operating System Deployment Server WMI Classes](../../../develop/reference/osd/operating-system-deployment-server-wmi-classes.md)   
 [SMS_TaskSequence_ConditionOperator Server WMI Class](../../../develop/reference/osd/sms_tasksequence_conditionoperator-server-wmi-class.md)   
 [SMS_TaskSequence_Condition Server WMI Class](../../../develop/reference/osd/sms_tasksequence_condition-server-wmi-class.md)   
 [SMS_TaskSequence_ConditionOperand Server WMI Class](../../../develop/reference/osd/sms_tasksequence_conditionoperand-server-wmi-class.md)
