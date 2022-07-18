---
description: Learn how to represent a computer or domain account used to access files on a Configuration Manager site system.
title: "SMS_NetworkAccessAccountConfig Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 51f0329c-e8ed-4a24-8439-de6597d5f7da
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_NetworkAccessAccountConfig Server WMI Class
The `SMS_NetworkAccessAccountConfig` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a computer or domain account used to access files on a Configuration Manager site system.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_NetworkAccessAccountConfig : SMS_ClientAgentConfig_BaseClass  
{  
    UInt32 AgentID;  
    Boolean SendToAllClients;  
    String Username;  
};  
```  

## Methods  
 The `SMS_NetworkAccessAccountConfig` class does not define any methods.  

## Properties  
 `AgentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Identifies the client agent component. The Network Access Account Configuration Agent ID is 7.  

 `SendToAllClients`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 This property is no longer used in Configuration Manager.  

 `Username`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Name of the user, including the domain name (domain\username).  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
