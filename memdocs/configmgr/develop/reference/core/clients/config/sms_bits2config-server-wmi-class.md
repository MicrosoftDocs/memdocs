---
description: Learn how to specify Background Intelligent Transfer settings for client computers using SMS_BITS2Config class.
title: SMS_BITS2Config Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 0369ae43-38f0-4dc2-b65f-34fe0f5b93c5
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
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
