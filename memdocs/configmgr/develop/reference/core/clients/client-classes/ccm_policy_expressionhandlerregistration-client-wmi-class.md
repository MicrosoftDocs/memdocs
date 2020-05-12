---
title: "CCM_Policy_ExpressionHandlerRegistration Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 41fc3f3c-7f32-471e-9005-d697eed4983f
author: aczechowski
ms.author: aaroncz
manager: dougeby


---
# CCM_Policy_ExpressionHandlerRegistration Client WMI Class
> [!IMPORTANT]
>  This class supports the Configuration Manager 2007 infrastructure and is not intended to be used directly from your code.  

 in Configuration Manager, the `CCM_Policy_ExpressionHandlerRegistration` class is a client Windows Management Instrumentation (WMI) class that describes a registered expression handler for a policy. An expression handler is a COM object that implements the `ICcmPolicyExpressionHandler` interface.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class CCM_Policy_ExpressionHandlerRegistration : CCM_Policy_Config  
{  
      String Clsid;  
      String Name;  
};  
```  

## Methods  
 The `CCM_Policy_ExpressionHandlerRegistration` class does not define any methods.  

## Properties  
 `Clsid`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null:ToInstance]  

 Class ID of the expression handler COM object, in registry format.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Name of the expression handler. The name is the same as the value of the `ExpressionType` property in [CCM_Policy_Expression Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy_expression-client-wmi-class.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Policy Agent Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/policy-agent-client-wmi-classes.md)   
 [CCM_Policy_Expression Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy_expression-client-wmi-class.md)
