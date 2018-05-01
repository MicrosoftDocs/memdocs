---
title: "CCM_Policy_Policy Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: ba718ec2-df70-426d-a6df-997a8e98483d
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# CCM_Policy_Policy Client WMI Class
In System Center Configuration Manager, the `CCM_Policy_Policy` class is a client Windows Management Instrumentation (WMI) class that defines a policy object for a client policy.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class CCM_Policy_Policy : CCM_Policy_Config  
{  
      String DownloadSource;  
      String PolicyCookie;  
      String PolicyHash;  
      String PolicyID;  
      CCM_Policy_Rule PolicyRules[];  
      String PolicySource;  
      String PolicyState;  
      String PolicyVersion;  
};  
```  

## Methods  
 The `CCM_Policy_Policy` class does not define any methods.  

## Properties  
 `DownloadSource`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null:ToInstance]  

 Location from which the policy is downloaded.  

 `PolicyCookie`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Arbitrary data used by the source authority.  

 `PolicyHash`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Reserved.  

 `PolicyID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Unique ID of the policy object.  

 `PolicyRules`  
 Data type: `CCM_Policy_Rule` Array  

 Access type: Read/Write  

 Qualifiers: None  

 Array of [CCM_Policy_Rule Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy_rule-client-wmi-class.md) objects describing rules reflecting actions of the policy object. Set this property to NULL if the policy object contains no actions.  

 `PolicySource`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Source authority of the policy object.  

 `PolicyState`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [ToInstance]  

 Current state of the policy object. Possible values are:  

|||  
|-|-|  
|NULL|The policy object is inactive and has not been downloaded. This is the default value.|  
|DownloadPending|The evaluator has determined that the policy object needs to be applied and should be downloaded. This is a temporary state used during the evaluation process.|  
|DownloadStarted|The policy object has been requested from the management point and is in the process of being downloaded.|  
|DownloadComplete|The policy object has finished downloading from the management point but has not been compiled into WMI yet.|  
|Inactive|The policy object is downloaded and compiled, but has no active assignments.|  
|Applied|The policy object is currently active, but pending re-valuation. This is a temporary state used during the evaluation process. If the evaluation determines that the policy object should no longer be active, its actions must be revoked.|  
|ApplyPending|The policy object is currently inactive, but now has active assignments and actions that should be applied. This is a temporary state used during the evaluation process.|  
|Active|The policy object is currently active and has been applied.|  
|NotApplicable|The policy object is not applicable. <br /><br /> This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.|  

 `PolicyVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Version of the policy object.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Policy Agent Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/policy-agent-client-wmi-classes.md)   
 [CCM_Policy_Rule Client WMI Class](../../../../../develop/reference/core/clients/client-classes/ccm_policy_rule-client-wmi-class.md)
