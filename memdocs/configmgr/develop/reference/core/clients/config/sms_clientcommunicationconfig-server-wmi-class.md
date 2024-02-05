---
description: Learn how to control how Windows 8 client computers communicate with Configuration Manager sites when they use metered Internet connections.
title: SMS_ClientCommunicationConfig Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: a9007fe8-9150-40cc-9f37-6430e49718f4
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_ClientCommunicationConfig Server WMI Class
The `SMS_ClientCommunicationConfig` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that controls how Windows 8 client computers communicate with Configuration Manager sites when they use metered Internet connections.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ClientCommunicationConfig : SMS_ClientAgentConfig_BaseClass  
{  
    UInt32 AgentID;  
    UInt32 MeteredNetworkUsage;  
};  
```  

## Methods  
 The `SMS_ClientCommunicationConfig` class doesn't define any methods.  

## Properties  
 `MeteredNetworkUsage`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Set metered network usage behavior. Possible values are:  

|Value|Metered network usage policy|  
|-|-|  
|1|Allow metered network use.|  
|2|Only use the metered network for deployments that are marked to allow use of the metered network. This means meta-data such as policy will always use the metered network. And based on the policy, the client decides whether or not to use the metered network for the deployment.|  
|4|Block metered network usage.|  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
