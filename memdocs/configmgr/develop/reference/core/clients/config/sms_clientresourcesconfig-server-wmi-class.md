---
description: Learn how to represent the settings and properties used by the client agent using SMS_ClientResourcesConfig.
title: SMS_ClientResourcesConfig Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 1500ceed-5edb-46fd-9722-ded6d9d38685
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_ClientResourcesConfig Server WMI Class
The `SMS_ClientResourcesConfig` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the settings and properties used by the client agent.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ClientResourcesConfig : SMS_ClientAgentConfig_BaseClass  
{  
    UInt32 AgentID;  
    Boolean DisableGlobalRandomization;  
};  
```  

## Methods  
 The `SMS_ClientResourcesConfig` class does not define any methods.  

## Properties  
 `AgentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Identifies the client agent component. The SMS_ClientResourcesConfig Agent ID is 25.  

 `DisableGlobalRandomization`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` disables global randomization.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
