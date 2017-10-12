---
title: "SMS_PowerAgentConfig Class"
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
ms.assetid: 2b1e09df-f8f1-4384-acd6-2108ad9a1f6csearchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_PowerAgentConfig Server WMI Class
The `SMS_PowerAgentConfig` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that specifies power management settings on client computers.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_PowerAgentConfig : SMS_ClientAgentConfig_BaseClass  
{  
    UInt32 AgentID;  
    Boolean AllowUserToOptOutFromPowerPlan;  
    Boolean Enabled;  
    Boolean EnableP2PWakeupSolution; (obsolete in SP1)  
    Boolean EnableWakeupProxy;  
    Boolean EnableUserIdleMonitoring;  
    UInt32 MaxCPU;  
    UInt32 MaxMachinesPerManager;  
    UInt32 MinimumServersNeeded;  
    UInt32 NumOfDaysToKeep;  
    UInt32 NumOfMonthsToKeep;  
    UInt32 Port;  
    UInt32 WakeupProxyDirectAccessPrefixList;  
    UInt32 WakeupProxyFirewallFlags;  
    UInt32 WolPort;  
};  
```  

## Methods  
 The `SMS_PowerAgentConfig` class does not define any methods.  

## Properties  
 `AgentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Identifies the client agent component. The Power Management Agent ID is 18.  

 `AllowUserToOptOutFromPowerPlan`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` to allow users to exclude their device from power management.  

 `Enabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the agent is enabled.  

 `EnableP2PWakeupSolution`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 This method/property has been removed or deprecated in System Center Configuration Manager SP1.  

 `EnableWakeupProxy`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 EnableWakeupProxy.   

 This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.  

 `EnableUserIdleMonitoring`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if user idle status needs to be monitored. The default value is `true`.  

 `MaxCPU`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Reserved for future use.  

 `MaxMachinesPerManager`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Reserved for future use.  

 `MinimumServersNeeded`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Reserved for future use.  

 `NumOfDaysToKeep`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Maximum number of days that power data will be kept on the client computer. The default value is 31.  

 `NumOfMonthsToKeep`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Maximum number of months that power data will be kept on the client computer. The default value is 13.  

 `Port`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Reserved for future use.  

 `WakeupProxyDirectAccessPrefixList`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 WakeupProxyDirectAccessPrefixList.   

 This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.  

 `WakeupProxyFirewallFlags`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 WakeupProxyFirewallFlags.   

 This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.  

 `WolPort`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Reserved for future use.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
