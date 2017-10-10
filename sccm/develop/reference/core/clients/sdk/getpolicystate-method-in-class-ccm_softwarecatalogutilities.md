---
title: "GetPolicyState Method"
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
ms.assetid: 8f5ac399-40bb-4133-9d87-da7f5f3ec46dsearchScope: - ConfigMgr SDK
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# GetPolicyState Method in Class CCM_SoftwareCatalogUtilities
The `GetPolicyState` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that returns the state of a policy object.   

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 GetPolicyState   
{  
    [IN]    String Id  
    [OUT]   UInt32 Status  
    [OUT]   UInt32 State  
};  
```  

## Parameters  
 `Id`  
 Data type: `String`  

 Qualifiers: [id("0"), in]  

 Unique ID of the policy object.   

 `Status`  
 Data type: `UInt32`  

 Qualifiers: [id("1"), out]  

 Current status.  

 `State`  
 Data type: `UInt32`  

 Qualifiers: [id("2"), out]  

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

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
