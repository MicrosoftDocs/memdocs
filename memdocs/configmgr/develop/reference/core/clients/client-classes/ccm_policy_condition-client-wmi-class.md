---
description: Learn how to represent a policy condition in Configuration Manager using CCM_Policy_Condition.
title: CCM_Policy_Condition Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 6a7f9c94-ccbd-43ef-9adb-ed620ba3fe5f
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# CCM_Policy_Condition Client WMI Class
In Configuration Manager, the `CCM_Policy_Condition` class is a client Windows Management Instrumentation (WMI) class that represents a policy condition.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class CCM_Policy_Condition : CCM_Policy_Config  
{  
      String ConditionID;  
      Boolean ConditionState;  
      Object ConditionExpression;  
};  
```  

## Properties  
 `ConditionID`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [key]  

 Condition ID.  

 `ConditionState`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 Current state of the condition. This value indicates the result of the last condition evaluation, or it is `null` if the condition has never been evaluated.  

 `ConditionExpression`  
 Data type: `Object`  

 Access type: Read-only  

 Qualifiers: [read]  

 Actual expression to evaluate. The value is a [CCM_Policy_Expression Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy_expression-client-wmi-class.md) object for a simple expression or a [CCM_Policy_Operator Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy_operator-client-wmi-class.md) object for a compound expression.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Policy Agent Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/policy-agent-client-wmi-classes.md)   
 [CCM_Policy_Expression Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy_expression-client-wmi-class.md)   
 [CCM_Policy_Operator Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy_operator-client-wmi-class.md)
