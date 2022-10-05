---
description: Learn how the SMS_DCMAgentConfig Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that specifies how client computers retrieve compliance settings.
title: SMS_DCMAgentConfig Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: ce4ca4df-660b-426d-a362-d9025d2b28ef
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_DCMAgentConfig Server WMI Class
The `SMS_DCMAgentConfig` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that specifies how client computers retrieve compliance settings.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DCMAgentConfig : SMS_ClientAgentConfig_BaseClass  
{  
    UInt32 AgentID;  
    Boolean Enabled;  
    Boolean EnableUserStateManagement;  
    UInt32 PerProviderTimeout;  
    UInt32 PerScanDefaultPriority;  
    UInt32 PerScanTimeout;  
    UInt32 PerScanTTL;  
};  
```  

## Methods  
 The `SMS_DCMAgentConfig` class does not define any methods.  

## Properties  
 `AgentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Identifies the client agent component. The Settings Management Agent identifier is 1.  

 `Enabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the agent is enabled.  

 `EnabledUserStateManagement`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` to enable user state management.  

 This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.  

 `PerProviderTimeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Indicated the timeout value for accessing the provider.  

 `PerScanDefaultPriority`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Priority of the Settings Management evaluation job. Possible values are:  

|Value|Settings scan priority|  
|-|-|  
|priIdle|Idle|  
|priNormal|Normal (recommended)|  
|priHigh|High|  
|priForeground|Foreground|  

 `PerScanTimeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Time after which an in-progress Settings Management evaluation will be canceled.  

 This property is deprecated.  

 `PerScanTTL`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Time to live (TTL) for the baseline evaluation result. If a baseline is evaluated and then quickly evaluated again, the second evaluation may be ignored depending TTL value.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
