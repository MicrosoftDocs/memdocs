---
title: SMS_CloudAgentConfig Class
titleSuffix: Configuration Manager
description: The SMS_CloudAgentConfig WMI class is an SMS Provider server class in Configuration Manager.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 969c2e06-c475-409b-903b-71be831fa754
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# SMS_CloudAgentConfig Server WMI Class

The `SMS_CloudAgentConfig` Windows Management Instrumentation (WMI) class is an SMS Provider server class in Configuration Manager.

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_CloudAgentConfig : SMS_ClientAgentConfig_BaseClass  
{  
    UInt32 AgentID;  
    Boolean AllowCloudDP;  
};  
```  

## Methods  
 The `SMS_CloudAgentConfig` class does not define any methods.  

## Properties  
 `AgentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 AgentID    

 `AllowCloudDP`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 AllowCloudDP    

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
