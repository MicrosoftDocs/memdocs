---
title: "CCM_Policy Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 41ae8c45-e00d-4d98-905d-e5a1303bdc30
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# CCM_Policy Client WMI Class
In System Center Configuration Manager, the `CCM_Policy` class is a client Windows Management Instrumentation (WMI) class that represents a client policy.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class CCM_Policy  
{  
      String PolicyID;  
      String PolicyInstanceID;  
      UInt32 PolicyPrecedence;  
      String PolicyRuleID;  
      String PolicySource;  
      String PolicyVersion;  
};  
```  

## Methods  
 The `CCM_Policy` class does not define any methods.  

## Properties  
 `PolicyID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Unique ID of the policy.  

 `PolicyInstanceID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Unique ID of the policy instance.  

 `PolicyPrecedence`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Precedence is used to resolve conflicts between policies from the same policy authority. For example, this occurs in System Center Configuration Manager when using collection variables to override site-wide policy, or setting a value for a collection variable on multiple collections of which the same client is a member.  

 `PolicyRuleID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Unique ID of the rule used to create the policy.  

 `PolicySource`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Source of the policy.  

 `PolicyVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Version of the policy.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Policy Agent Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/policy-agent-client-wmi-classes.md)
