---
description: Learn how to use Configuration Manager SMS_TaskSequence_OSConditionGroup Windows Management Instrumentation (WMI) class  to represent an evaluation of a group of operating system platforms.
title: SMS_TaskSequence_OSConditionGroup Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 89182703-07ff-410a-9406-f2424eca5550
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_TaskSequence_OSConditionGroup Server WMI Class
The `SMS_TaskSequence_OSConditionGroup` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents an evaluation of a group of operating system platforms, for example, Windows Vista, in a task sequence.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_OSConditionGroup : SMS_TaskSequence_ConditionOperator  
{  
      SMS_TaskSequence_OSExpressionGroup Operands[];  
      String OperatorType;  
};  
```  

## Methods  
 The `SMS_TaskSequence_OSConditionGroup` class does not define any methods.  

## Properties  
 `Operands`  
 Data type: `SMS_TaskSequence_OSExpressionGroup`Array  

 Access type: Read/Write  

 Qualifiers: [Not_NULL]  

 An array of supported operating system platforms to evaluate. Stored in a  

 [SMS_TaskSequence_OSExpressionGroup Server WMI Class](../../../develop/reference/osd/sms_tasksequence_osexpressiongroup-server-wmi-class.md) array. There must be at least one array member.  

 `OperatorType`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_NULL]  

 See [SMS_TaskSequence_ConditionOperator Server WMI Class](../../../develop/reference/osd/sms_tasksequence_conditionoperator-server-wmi-class.md).  

 Only the operator "or" is supported.  

## Remarks  
 There are no class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_TaskSequence_ConditionOperator Server WMI Class](../../../develop/reference/osd/sms_tasksequence_conditionoperator-server-wmi-class.md)   
 [SMS_TaskSequence_OSExpressionGroup Server WMI Class](../../../develop/reference/osd/sms_tasksequence_osexpressiongroup-server-wmi-class.md)
