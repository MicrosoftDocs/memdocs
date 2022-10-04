---
title: CCM_EvaluationState Class
titleSuffix: Configuration Manager
description: The CCM_EvaluationState WMI class is an SMS Provider server class in Configuration Manager.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: cee8005f-1db4-4978-ae16-51901fd0ff1c
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# CCM_EvaluationState Client WMI Class

The `CCM_EvaluationState` Windows Management Instrumentation (WMI) class is an SMS Provider server class in Configuration Manager.

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class CCM_EvaluationState :    
{  
    UInt32 ErrorCode;  
    UInt32 EvaluationState;  
    UInt32 PercentComplete;  
};  
```  

## Methods  
 The `CCM_EvaluationState` class does not define any methods.  

## Properties  
 `ErrorCode`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Error code.    

 `EvaluationState`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Evaluation state. Possible values are:  

|Evaluation State Value|Description|  
|----------------------------|-----------------|  
|0|No state information is available.|  
|1|Application is enforced to desired/resolved state.|  
|2|Application is not required on the client.|  
|3|Application is available for enforcement (install or uninstall based on resolved state). Content may/may not have been downloaded.|  
|4|Application last failed to enforce (install/uninstall).|  
|5|Application is currently waiting for content download to complete.|  
|6|Application is currently waiting for content download to complete.|  
|7|Application is currently waiting for its dependencies to download.|  
|8|Application is currently waiting for a service (maintenance) window.|  
|9|Application is currently waiting for a previously pending reboot.|  
|10|Application is currently waiting for serialized enforcement.|  
|11|Application is currently enforcing dependencies.|  
|12|Application is currently enforcing.|  
|13|Application install/uninstall enforced and soft reboot is pending.|  
|14|Application installed/uninstalled and hard reboot is pending.|  
|15|Update is available but pending installation.|  
|16|Application failed to evaluate.|  
|17|Application is currently waiting for an active user session to enforce.|  
|18|Application is currently waiting for all users to logoff.|  
|19|Application is currently waiting for a user logon.|  
|20|Application in progress, waiting for retry.|  
|21|Application is waiting for presentation mode to be switched off.|  
|22|Application is pre-downloading content (downloading outside of install job).|  
|23|Application is pre-downloading dependent content (downloading outside of install job).|  
|24|Application download failed (downloading during install job).|  
|25|Application pre-downloading failed (downloading outside of install job).|  
|26|Download success (downloading during install job).|  
|27|Post-enforce evaluation.|  
|28|Waiting for network connectivity.|  

 `PercentComplete`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Percent complete.    

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
