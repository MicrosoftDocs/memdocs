---
title: "GetClientConfigPolicies Method"
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
ms.assetid: b28b0e20-24d3-4d0c-88fa-c870a927dbc1searchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# GetClientConfigPolicies Method in Class SMS_TaskSequencePackage
The `GetClientConfigPolicies` Windows Management Instrumentation (WMI) class method, in System Center Configuration Manager, gets all site-wide client configuration policies and their corresponding policy assignments.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 GetClientConfigPolicies(  
      String PolicyXmls[],  
      String PolicyAssignmentXmls[]  
);  
```  

#### Parameters  
 `PolicyXmls`  
 Data type: `String` Array  

 Qualifiers: [out]  

 The XML representations of all site-wide client configuration policies.  

 `PolicyAssignmentXmls`  
 Data type: `String` Array  

 Qualifiers: [out]  

 The XML representations of all site-wide client configuration policy assignments. This parameter and `PolicyXmls` are aligned, with the nth element of one corresponding to the nth element of the other.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_TaskSequencePackage Server WMI Class](../../../develop/reference/osd/sms_tasksequencepackage-server-wmi-class.md)
