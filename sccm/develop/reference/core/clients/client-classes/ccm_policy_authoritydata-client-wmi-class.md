---
title: "CCM_Policy_AuthorityData Class"
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
ms.assetid: 1cbfd6ec-21ef-45c0-ad62-ea3d78768616searchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# CCM_Policy_AuthorityData Client WMI Class
In System Center Configuration Manager, the `CCM_Policy_AuthorityData` class is a client Windows Management Instrumentation (WMI) class that stores information about policy from a particular authority.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class CCM_Policy_AuthorityData : CCM_Policy_Config  
{  
      DateTime LastReplyTime;  
      String Name;  
      String ServerCookie;  
};  
```  

## Methods  
 The `CCM_Policy_AuthorityData` class does not define any methods.  

## Properties  
 `LastReplyTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 The last date and time when the authority replied to a request for policy assignments. If this value is older than the value of `PolicyTimeUntilAck` in the authority's [CCM_PolicyAgent_Configuration Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policyagent_configuration-client-wmi-class.md) object, the policy requests an acknowledgment. If the value is older than the value of `PolicyTimeUntilExpire`, the policy is expired.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Name of the authority to which the data applies.  

 `ServerCookie`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The last `ServerCookie` value received from the authority in a `ReplyAssignments` message.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Policy Agent Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/policy-agent-client-wmi-classes.md)   
 [CCM_PolicyAgent_Configuration Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policyagent_configuration-client-wmi-class.md)
