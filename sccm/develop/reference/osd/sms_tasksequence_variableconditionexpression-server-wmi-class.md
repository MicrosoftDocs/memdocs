---
title: "SMS_TaskSequence_VariableConditionExpression Class"
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
ms.assetid: 996dbc32-7d34-49f0-8a96-ccaf6585279dsearchScope: - ConfigMgr SDK
caps.latest.revision: 11
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_TaskSequence_VariableConditionExpression Server WMI Class
The `SMS_TaskSequence_VariableConditionExpression` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a condition expression to check for the existence of a variable and, optionally, compare the variable to a specific value.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_VariableConditionExpression : SMS_TaskSequence_ConditionExpression  
{  
      String Operator;  
      String Value;  
      String Variable;  
};  
```  

## Methods  
 The `SMS_TaskSequence_VariableConditionExpression` class does not define any methods.  

## Properties  
 `Operator`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null]  

 Operator to use in the verification. Possible values are:  

-   exists  

-   notExists  

-   equals  

-   notEquals  

-   less  

-   lessEqual  

-   greater  

-   greaterEqual  

 `Value`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Optional value to which the variable can be compared.  

 `Variable`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null]  

 The name of the variable to verify.  

## Remarks  
 There are no class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 This condition expression is used to test the value of a task sequence variable. For example, to perform a step only if the task sequence is not running under Windows PE, you would set the following:  

 `Variable` - _SMSTSInWinPE.  

 `Operator` - equals  

 `Value` - false  

 For more information about task sequence variables, see [Operating System Deployment Task Sequence Variables](http://go.microsoft.com/fwlink/?LinkId=100711).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Operating System Deployment Server WMI Classes](../../../develop/reference/osd/operating-system-deployment-server-wmi-classes.md)
