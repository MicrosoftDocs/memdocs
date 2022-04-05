---
title: "CCM_Policy_Expression Class"
titleSuffix: "Configuration Manager"
description: "aA client Windows Management Instruementation class that represents a policy expression, which evaluates to either true or false."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 2ad7dbc5-ee6f-40e2-a03f-413a8236153e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# CCM_Policy_Expression Client WMI Class
In Configuration Manager, the `CCM_Policy_Expression` class is a client Windows Management Instruementation (WMI) class that represents a policy expression that evaluates to either `true` or `false`.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class CCM_Policy_Expression : CCM_Policy_Config  
{  
      String ExpressionData;  
      String ExpressionLanguage;  
      Boolean ExpressionState;  
      String ExpressionType;  
};  
```  

## Methods  
 The `CCM_Policy_Expression` class does not define any methods.  

## Properties  
 `ExpressionData`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null:ToInstance]  

 Data representing the expression to evaluate. The actual format is specific to the expression type. For more information, see `ExpressionType`.  

 `ExpressionLanguage`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null:ToInstance]  

 The type of expression, which must map to an object that contains information about the handler responsible for evaluating this expression type.  

 `ExpressionState`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 Current state of the expression. This value indicates the result of the last expression evaluation, or `null` if the expression has never been evaluated.  

 `ExpressionType`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null:ToInstance]  

 Type that determines how the expression is evaluated. Possible values are:  


| Value | Description |
| ----- | ----------- |
|Once|The expression is evaluated only once.|  
|Until-true|The expression continues to be re-evaluated until evaluation returns `true`.|  
|Continuous|The expression is always re-evaluated.|  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Policy Agent Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/policy-agent-client-wmi-classes.md)
