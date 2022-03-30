---
title: "CCM_Policy_Assignment Class"
titleSuffix: "Configuration Manager"
description: "The CCM_Policy_Assignment class is a client Windows Management Instrumentation (WMI) class that represents a policy assignment."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 78fb45c2-f30b-4f24-b755-261e98880548
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# CCM_Policy_Assignment Client WMI Class
In Configuration Manager, the `CCM_Policy_Assignment` class is a client Windows Management Instrumentation (WMI) class that represents a policy assignment.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class CCM_Policy_Assignment : CCM_Policy_Config  
{  
      String AssignmentCondition;  
      String AssignmentCookie;  
      String AssignmentID;  
      ref:CCM_Policy_Policy AssignmentPolicy;  
      String AssignmentSource;  
};  
```  

## Methods  
 The `CCM_Policy_Assignment` class does not define any methods.  

## Properties  
 `AssignmentCondition`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Assignment condition that determines if the policy should be applied to the assignment. Set this property to NULL if the policy always applies, or to the ID of a particular policy condition, represented by [CCM_Policy_Condition Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy_condition-client-wmi-class.md).  

 `AssignmentCookie`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null:ToInstance]  

 Arbitrary data used by the source authority.  

 `AssignmentID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Unique ID of the assignment.  

 `AssignmentPolicy`  
 Data type: `ref:CCM_Policy_Policy`  

 Access type: Read-only  

 Qualifiers: [read, Not_Null:ToInstance]  

 Reference to the policy object to which the assignment applies.  

 `AssignmentSource`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key, Not_Null:ToInstance]  

 Source authority of the assignment.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Policy Agent Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/policy-agent-client-wmi-classes.md)   
 [CCM_Policy_Condition Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy_condition-client-wmi-class.md)
