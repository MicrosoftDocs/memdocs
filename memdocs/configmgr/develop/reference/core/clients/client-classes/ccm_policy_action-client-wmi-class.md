---
title: "CCM_Policy_Action Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 6d51a235-ce91-43db-ac2a-a54dd06dc5fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# CCM_Policy_Action Client WMI Class
In Configuration Manager, the `CCM_Policy_Action` class is a client Windows Management Instrumentation (WMI) class that represents settings for a policy action.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class CCM_Policy_Action : CCM_Policy_Config  
{  
      String ActionData;  
      String ActionType;  
};  
```  

## Methods  
 The `CCM_Policy_Action` class does not define any methods.  

## Properties  
 `ActionData`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null:ToInstance]  

 Handler-specific data and policy settings defined in MOF to be compiled directly into the appropriate `RequestedConfig` namespace. The MOF text should only contain object definitions and should not include any class definitions or #pragma statements.  

 `ActionType`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null:ToInstance]  

 The type of the action, which must map to a registered action handler. The default value is WMI-MOF.  

## Remarks  
 This class is only used to support objects reflected in the `RuleActions` property in [CCM_Policy_Rule Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy_rule-client-wmi-class.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Policy Agent Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/policy-agent-client-wmi-classes.md)
