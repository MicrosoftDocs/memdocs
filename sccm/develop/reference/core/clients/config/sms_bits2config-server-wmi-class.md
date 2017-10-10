---
title: "SMS_BITS2Config Class"
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
ms.assetid: 0369ae43-38f0-4dc2-b65f-34fe0f5b93c5searchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_BITS2Config Server WMI Class
The `SMS_BITS2Config` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that specifies Background Intelligent Transfer settings for client computers.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_BITS2Config : SMS_ClientAgentConfig_BaseClass  
{  
    UInt32 AgentID;  
    Boolean ApplyToAllClients;  
    Boolean EnableBitsMaxBandwidth;  
    Boolean EnableDownloadOffSchedule;  
    UInt32 MaxBandwidthValidFrom;  
    UInt32 MaxBandwidthValidTo;  
    UInt32 MaxTransferRateOffSchedule;  
    UInt32 MaxTransferRateOnSchedule;  
};  
```  

## Methods  
 The `SMS_BITS2Config` class does not define any methods.  

## Properties  
 `AgentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Identifies the client agent component. The BITS2Config Agent ID is 11.  

 `ApplyToAllClients`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` to apply Background Intelligent Transfer settings to all computers.  

 `EnableBitsMaxBandwidth`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` to enable maximum network bandwidth for BITS background transfers.  

 `EnableDownloadOffSchedule`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` to allow BITS downloads outside of the throttling window.  

 `MaxBandwidthValidFrom`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Throttling window end time. Valid values are from 0-23.  

 `MaxBandwidthValidTo`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Throttling window start time. Valid values are from 0-23.  

 `MaxTransferRateOffSchedule`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Maximum transfer rate outside of the throttling window (Kbps).  

 `MaxTransferRateOnSchedule`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Maximum transfer rate during the throttling window (Kbps).  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
