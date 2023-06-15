---
description: Learn how to define a policy object rule used in the PolicyRules property with the CCM_Policy_Rule class.
title: CCM_Policy_Rule Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: d59fb097-6a80-418a-9779-2d6c7e547ab9
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# CCM_Policy_Rule Client WMI Class
In Configuration Manager, the `CCM_Policy_Rule` class is a client Windows Management Instrumentation (WMI) class that defines a policy object rule. Objects of this class are only used in the `PolicyRules` property in [CCM_Policy_Policy Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy_policy-client-wmi-class.md).  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class  CCM_Policy_Rule : CCM_Policy_Config  
{  
      String RuleID;  
      String RuleCondition;  
      Object RuleActions[];  
};  
```  

## Properties  
 `RuleID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key]  

 Unique ID of the rule within the policy object.  

 `RuleCondition`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Optional. Rule condition. If the condition is not NULL, set this property to the unique ID of a [CCM_Policy_Condition Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy_condition-client-wmi-class.md) object. The rule is only applied if the policy is active and the rule condition evaluates to TRUE.  

 `RuleActions`  
 Data type: `Object` Array  

 Access type: Read-only  

 Qualifiers: None  

 Array of [CCM_Policy_Action Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy_action-client-wmi-class.md) objects specifying the actions to perform when the rule is applied.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Policy Agent Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/policy-agent-client-wmi-classes.md)   
 [CCM_Policy_Condition Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy_condition-client-wmi-class.md)   
 [CCM_Policy_Action Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy_action-client-wmi-class.md)
