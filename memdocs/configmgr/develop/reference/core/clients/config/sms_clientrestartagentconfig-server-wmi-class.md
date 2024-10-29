---
title: SMS_ClientRestartAgentConfig Class
titleSuffix: Configuration Manager
description: An SMS Provider server class that represents the settings and properties used by the client restart agent.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: aef07b1f-8fde-4c19-9fbc-b121a2df68e0
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_ClientRestartAgentConfig Server WMI Class
The `SMS_ClientRestartAgentConfig` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the settings and properties used by the client restart agent.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ClientRestartAgentConfig : SMS_ClientAgentConfig_BaseClass  
{  
    UInt32 AgentID;  
    UInt32 RebootLogoffNotificationCountdownDuration;  
    UInt32 RebootLogoffNotificationFinalWindow;  
};  
```  

## Methods  
 The `SMS_ClientRestartAgentConfig` class does not define any methods.  

## Properties  
 `AgentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Identifies the client agent component. The SMS_ClientRestartAgentConfig Agent ID is 21.  

 `RebootLogoffNotificationCountdownDuration`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Display a temporary notification to the user that indicates the interval before the user is logged off or the computer restarts (minutes).  

 `RebootLogoffNotificationFinalWindow`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Display a dialog box that the user cannot close, which displays the countdown interval before the user is logged off or the computer restarts (minutes).  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
