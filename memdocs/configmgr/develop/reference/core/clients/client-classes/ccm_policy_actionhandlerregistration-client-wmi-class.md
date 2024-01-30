---
title: CCM_Policy_ActionHandlerRegistration Class
titleSuffix: Configuration Manager
description: A class that supports the Configuration Manager 2007 infrastructure and isn't intended to be used directly from your code.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 9d86a6af-6735-4e6a-bb51-21985323fa1a
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# CCM_Policy_ActionHandlerRegistration Client WMI Class
> [!IMPORTANT]
>  This class supports the Configuration Manager 2007 infrastructure and is not intended to be used directly from your code.  

 in Configuration Manager, the `CCM_Policy_ActionHandlerRegistration` class is a client Windows Management Instrumentation (WMI) class that represents an action handler registration for a policy. An action handler is a COM object that applies a particular type of policy.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class CCM_Policy_ActionHandlerRegistration : CCM_Policy_Config  
{  
      String Clsid;  
      String Name;  
      String Type;  
};  
```  

## Methods  
 The `CCM_Policy_ActionHandlerRegistration` class does not define any methods.  

## Properties  
 `Clsid`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null:ToInstance]  

 Class ID of the action handler COM object in registry format.  

 `Name`  
 Data type`: String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Name of the action handler. This name is the same as the value of the `ActionType` property in [CCM_Policy_Action Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy_action-client-wmi-class.md).  

 `Type`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null:ToInstance]  

 The type of the action handler, which defaults to WMI. The handler implements the `ICcmPolicyWmiActionHandler` interface for creating WMI objects in the `RequestConfig` namespace.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Policy Agent Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/policy-agent-client-wmi-classes.md)   
 [CCM_Policy_Action Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy_action-client-wmi-class.md)
