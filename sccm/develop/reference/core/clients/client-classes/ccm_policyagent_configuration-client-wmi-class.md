---
title: "CCM_PolicyAgent_Configuration Class"
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
ms.assetid: 72e377e9-0494-4ec6-a7b6-4361df7112e2searchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# CCM_PolicyAgent_Configuration Client WMI Class
In System Center Configuration Manager, the `CCM_PolicyAgent_Configuration` class is a client Windows Management Instrumentation (WMI) class that represents the Policy Agent configuration for a given authority.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class CCM_PolicyAgent_Configuration : CCM_Policy  
{  
      String AuthorityName;  
      Boolean PolicyDownloadByBatch;  
      String PolicyDownloadMethod;  
      UInt32 PolicyDownloadsPerBatch;  
      Boolean PolicyDownloadUsePeerCache;  
      Boolean PolicyEnableUserAuthForAllUserPolicies;  
      Boolean PolicyEnableUserGroupSupport; (Removed in SP1)  
      Boolean PolicyEnableUserPolicyOnInternet;  
      Boolean PolicyEnableUserPolicyPolling;  
      UInt32 PolicyExpirationTimeForDefaultPerUserRequestedConfig;  
      String PolicyID;  
      String PolicyInstanceID;  
      UInt32 PolicyPrecedence;  
      UInt32 PolicyRequestAssignmentTimeout;  
      String PolicyRuleID;  
      String PolicySource;  
      UInt32 PolicyTimeDelayBeforeUserPolicyRefreshAtLogonOrUnlock;  
      UInt32 PolicyTimeUntilAck;  
      UInt32 PolicyTimeUntilExpire;  
      UInt32 PolicyTimeUntilUpdateActualConfig;  
      String PolicyVersion;  
};  
```  

## Methods  
 The `CCM_PolicyAgent_Configuration` class does not define any methods.  

## Properties  
 `AuthorityName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [RealKey]  

 Name of the authority.  

 `PolicyDownloadsByBatch`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if . The default value is `true`.  

 `PolicyDownloadMethod`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [ToInstance ToSubClass]  

 Method used by the Policy Agent to download policy files. Possible values are listed below. This value can only be NULL if `PolicyRequestTarget` is NULL. This value should not be changed.  

|||  
|-|-|  
|FILECOPY|Copy policy files using standard file copy operations. Policy paths must be local or Universal Naming Convention (UNC) file paths. This value is intended for testing only.|  
|HTTP|Download policy files synchronously by using direct HTTP. Policy paths must be HTTP URLs.|  
|BITS|Drizzle policy files asynchronously by using the Data Transfer Service. Policy paths must be HTTP URLs.|  

 `PolicyDownloadsPerBatch`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: []  

 For batch policy download. The default value is 150.  

 `PolicyDownloadUsePeerCache`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: []  

 `true` to use peer cache.  

 `PolicyEnableUserAuthForAllUserPolicies`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: []  

 `true` to enable user policy polling.  

 `PolicyEnableUserGroupSupport`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [Not_Null:ToInstance ToSubClass]  

 `true` if the Policy Agent sends user group information when requesting a user policy.  

 This method/property has been removed or deprecated in System Center Configuration Manager SP1.  

 `PolicyEnableUserPolicyOnInternet`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: []  

 `true` to   

 `PolicyEnableUserPolicyPolling`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` to enable user policy polling.  

 `PolicyExpirationTimeForDefaultPerUserRequestedConfig`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  



 `PolicyID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 See [CCM_Policy Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy-client-wmi-class.md).  

 `PolicyInstanceID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 See [CCM_Policy Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy-client-wmi-class.md).  

 `PolicyPrecedence`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 See [CCM_Policy Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy-client-wmi-class.md).  

 `PolicyRequestAssignmentTimeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Timeout for the policy request assignment.  

 `PolicyRuleID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 See [CCM_Policy Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy-client-wmi-class.md).  

 `PolicySource`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 See [CCM_Policy Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy-client-wmi-class.md).  

 `PolicyTimeDelayBeforeUserPolicyRefreshAtLogonOrUnlock`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 PolicyTimeDelayBeforeUserPolicyRefreshAtLogonOrUnlock.   

 `PolicyTimeUntilAck`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The time that must elapse before the policy is acknowledged.  

 `PolicyTimeUntilExpire`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The number of days that the Policy Agent should wait since it last received a `ReplyAssignments` message from the authority before removing its policy. At half this time, the Policy Agent begins requesting acknowledgments. If this value is NULL, the policy never expires.  

 `PolicyTimeUntilUpdateActualConfig`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The time that must elapse before the actual configuration is updated.  

 `PolicyVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 See [CCM_Policy Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy-client-wmi-class.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Policy Agent Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/policy-agent-client-wmi-classes.md)   
 [CCM_Policy Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy-client-wmi-class.md)
