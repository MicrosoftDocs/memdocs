---
title: "SMS_HardwareInventoryAgentConfig Class"
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
ms.assetid: df1b1aa3-66c8-45d4-bf8e-e6382ebb25b4searchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_HardwareInventoryAgentConfig Server WMI Class
The `SMS_HardwareInventoryAgentConfig` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that specifies hardware inventory settings for client computers.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_HardwareInventoryAgentConfig : SMS_ClientAgentConfig_BaseClass  
{  
    UInt32 AgentID;  
    Boolean Enabled;  
    String InventoryReportID;  
    String LastUpdateTime;  
    UInt32 Max3rdPartyMIFSize;  
    UInt32 MIFCollection;  
    UInt32 ProviderTimeout;  
    String Schedule;  
};  
```  

## Methods  
 The `SMS_HardwareInventoryAgentConfig` class does not define any methods.  

## Properties  
 `AgentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Identifies the client agent component. The Hardware Inventory Agent ID is 15.  

 `Enabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the agent is enabled.  

 `InventoryReportID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Identifies the type of inventory report.  

|||  
|-|-|  
|Hardware Inventory|{00000000-0000-0000-0000-000000000001}|  
|Software Inventory|{00000000-0000-0000-0000-000000000002}|  
|Data Discovery Record|{00000000-0000-0000-0000-000000000003}|  

 `LastUpdateTime`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Last time the client setting was updated.  

 `Max3rdPartyMIFSize`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Maximum custom MIF file size (KB).  

 `MIFCollection`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 MIF files to collect.  

|||  
|-|-|  
|0|None|  
|0x08|Collect IDMIF files|  
|0x04|Collect NOIDMIF files|  
|0x0C|Collect IDMIF and NOIDMIF files|  

 `ProviderTimeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 This property is not currently used.  

 `Schedule`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Schedule of hardware inventory.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
