---
title: "CCM_Policy_Operator Class"
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
ms.assetid: 509e390b-cd50-44ae-8ed4-dacf59c512easearchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# CCM_Policy_Operator Client WMI Class
In System Center Configuration Manager, the `CCM_Policy_Operator` class is a client Windows Management Instrumentation (WMI) class that stores a compound expression that evaluates to either `true` or `false`.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
class CCM_Policy_Operator : CCM_Policy_Config  
{  
      String OperatorType;  
   Object Operands[];  
};  
```  

## Properties  
 `OperatorType`  
 Data type: `String`  

 Access type: Read-only  

 Qualifier: [Not_Null:ToInstance]  

 The type of operator. Possible values are:  

|||  
|-|-|  
|`AND`|A logical `AND` operator. The result of the compound expression is only `true` if all of its operands evaluate to `true`.|  
|`OR`|A logical `OR` operator. The result of the compound expression is `true` if any one of its operands evaluates to `true`.|  
|`NOT`|A logical `NOT` operator. This operator can only have a single operand. The result of the expression is `true` only if the operand evaluates to `false`.|  

 `Operands`  
 Data type: `Object`  

 Access type: Read-only  

 Qualifier: [Not_Null:ToInstance]  

 Operands for the compound expression. Each operand can be a [CCM_Policy_Expression Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy_expression-client-wmi-class.md) object or a `CCM_Policy_Operator` object if further nesting is required.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Policy Agent Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/policy-agent-client-wmi-classes.md)   
 [CCM_Policy_Expression Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy_expression-client-wmi-class.md)
