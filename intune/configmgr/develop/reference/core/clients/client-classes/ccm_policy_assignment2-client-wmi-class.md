---
description: Learn how to use the CCM_Policy_Assignment2 class to represent a policy assignment in Configuration Manager.
title: CCM_Policy_Assignment2 Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 2375c0fc-3867-4c96-8665-e4fd6adec600
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# CCM_Policy_Assignment2 Client WMI Class
In Configuration Manager, the `CCM_Policy_Assignment2` class is a client Windows Management Instrumentation (WMI) class that represents a policy assignment.

 This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.

## Syntax

```
Class CCM_Policy_Assignment2 : CCM_Policy_Config
{
      String AssignmentCondition;
      String AssignmentCookie;
      String AssignmentID;
      ref:CCM_Policy_Policy AssignmentPolicy;
      String AssignmentSource;
      String AssignmentVersion;
};
```

## Methods
 The `CCM_Policy_Assignment2` class does not define any methods.

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

 `AssignmentVersion`
 Data type: `String`

 Access type: Read/Write

 Qualifiers: [key, Not_Null:ToInstance ToSubClass]

 Version of the assignment.

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).

## See Also
 [Policy Agent Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/policy-agent-client-wmi-classes.md)
 [CCM_Policy_Condition Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy_condition-client-wmi-class.md)
