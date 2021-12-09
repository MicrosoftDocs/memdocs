---
title: "SMS_TaskSequence_ConditionOperator Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 9a648643-1b62-4776-a1f4-9699e72ecc2e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_TaskSequence_ConditionOperator Server WMI Class
The `SMS_TaskSequence_ConditionOperator` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents an operator to use when evaluating task sequence condition operands.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_ConditionOperator : SMS_TaskSequence_ConditionOperand  
{  
      SMS_TaskSequence_ConditionOperand Operands[];  
      String OperatorType;  
};  
```  

## Methods  
 The `SMS_TaskSequence_ConditionOperator` class does not define any methods.  

## Properties  
 `Operands`  
 Data type: `SMS_TaskSequence_ConditionOperand` Array  

 Access type: Read/Write  

 Qualifiers: [Not_Null:ToInstance]  

 [SMS_TaskSequence_ConditionOperand Server WMI Class](../../../develop/reference/osd/sms_tasksequence_conditionoperand-server-wmi-class.md) objects to test.  

 `OperatorType`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null:ToInstance]  

 Type of operator to use in testing the conditions. Possible values are:  

-   and  

-   or  

-   not  

## Remarks  
 There are no class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

> [!NOTE]
>  Task sequence step conditions are defined in [SMS_TaskSequence_Condition Server WMI Class](../../../develop/reference/osd/sms_tasksequence_condition-server-wmi-class.md).  

 `SMS_TaskSequence_ConditionOperator` is used to create complete complex conditions that determine if a task sequence step should be processed. The `Operands` array property holds one or more expression ([SMS_TaskSequence_ConditionExpression Server WMI Class](../../../develop/reference/osd/sms_tasksequence_conditionexpression-server-wmi-class.md)) or operator (`SMS_TaskSequence_ConditionOperator`) operands to evaluate.  

> [!NOTE]
>  Both of these classes derive from SMS[SMS_TaskSequence_ConditionOperand Server WMI Class](../../../develop/reference/osd/sms_tasksequence_conditionoperand-server-wmi-class.md), the type for the  `Operands` property.  

 The operator used to evaluate the operands is defined by the `OperatorType` property.  

 For more information, see Operating System Deployment Task Sequence Object Model.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_TaskSequence_ConditionExpression Server WMI Class](../../../develop/reference/osd/sms_tasksequence_conditionexpression-server-wmi-class.md)   
 [SMS_TaskSequence_ConditionOperand Server WMI Class](../../../develop/reference/osd/sms_tasksequence_conditionoperand-server-wmi-class.md)   
 [SMS_TaskSequence_Condition Server WMI Class](../../../develop/reference/osd/sms_tasksequence_condition-server-wmi-class.md)
