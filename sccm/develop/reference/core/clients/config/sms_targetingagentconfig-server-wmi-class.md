---
title: "SMS_TargetingAgentConfig Class"
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
ms.assetid: 9d7e244d-549e-4a3e-9a04-2033b960e29fsearchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_TargetingAgentConfig Server WMI Class
The `SMS_TargetingAgentConfig` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents how the client is configured for user and device affinity.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TargetingAgentConfig : SMS_ClientAgentConfig_BaseClass  
{  
    UInt32 AgentID;  
    UInt32 AllowUserAffinity;  
    UInt32 AllowUserAffinityAfterMinutes;  
    UInt32 AutoApproveAffinity;  
    UInt32 ConsoleMinutes;  
    UInt32 IntervalDays;  
};  
```  

## Methods  
 The `SMS_TargetingAgentConfig` class does not define any methods.  

## Properties  
 `AgentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Identifies the client agent component. The Targeting Agent Config ID is 10.  

 `AllowUserAffinity`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Allows users to define their primary devices.  

 `AllowUserAffinityAfterMinutes`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 This property is obsolete.  

 `AutoApproveAffinity`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Automatically configures user device affinity from usage data.  

 `ConsoleMinutes`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 User device affinity usage threshold in minutes.  

 `IntervalDays`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 User device affinity usage threshold in days.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
