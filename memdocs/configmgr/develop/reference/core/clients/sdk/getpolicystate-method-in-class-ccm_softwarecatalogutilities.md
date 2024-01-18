---
title: GetPolicyState Method
titleSuffix: Configuration Manager
description: A Windows Management Instrumentation (WMI) class method that returns the state of a policy object.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 8f5ac399-40bb-4133-9d87-da7f5f3ec46d
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# GetPolicyState Method in Class CCM_SoftwareCatalogUtilities
The `GetPolicyState` Windows Management Instrumentation (WMI) class method in Configuration Manager that returns the state of a policy object.   

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

|Value|State|  
|-|-|  
|NULL|The policy object is inactive and hasn't been downloaded. This value is the default value.|  
|DownloadPending|The evaluator determines that the policy object needs to be applied and should be downloaded. This state is a temporary one used during the evaluation process.|  
|DownloadStarted|The policy object has been requested from the management point and is in the process of being downloaded.|  
|DownloadComplete|The policy object finished downloading from the management point but hasn't been compiled into WMI yet.|  
|Inactive|The policy object is downloaded and compiled, but has no active assignments.|  
|Applied|The policy object is currently active, but pending revaluation. This state is a temporary one used during the evaluation process. If the evaluation determines that the policy object should no longer be active, its actions must be revoked.|  
|ApplyPending|The policy object is currently inactive, but now has active assignments and actions that should be applied. This state is a temporary one used during the evaluation process.|  
|Active|The policy object is currently active and has been applied.|  
|NotApplicable|The policy object isn't applicable. <br /><br /> This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.|  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
