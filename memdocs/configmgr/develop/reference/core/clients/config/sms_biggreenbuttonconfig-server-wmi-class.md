---
description: Learn how to stop clients from connecting to the client notification server with SMS_BigGreenButtonConfig.
title: SMS_BigGreenButtonConfig Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 3fd7c3a1-bab9-4970-93a4-0b6e978fd3eb
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_BigGreenButtonConfig Server WMI Class
The `SMS_BigGreenButtonConfig` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that can stop clients from connecting to the client notification server (a hidden role, co-located with management point).  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_BigGreenButtonConfig : SMS_ClientAgentConfig_BaseClass  
{  
    UInt32 AgentID;  
    Boolean EnableClientNotification;  
};  
```  

## Methods  
 The `SMS_BigGreenButtonConfig` class does not define any methods.  

## Properties  
 `AgentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Identifies the client agent component. The BigGreenButton Agent ID is 18.  

 `EnableClientNotification`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `false` to stop clients from connecting to the client notification server (a hidden role, co-located with management point). No active connections will be established between the clients and the client notification server. The default value is `true`.  

 This setting is part of the client infrastructure and turned on by default. This value would likely only be changed to troubleshoot a significant performance issue.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
