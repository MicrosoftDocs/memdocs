---
title: CCM_NetworkSettings Class
titleSuffix: Configuration Manager
description: Details of the CCM_NetworkSettings Client WMI Class
ms.date: 08/02/2021
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# CCM_NetworkSettings Client WMI Class
The `CCM_NetworkSettings` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents how clients behave on metered Internet connections.   

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class CCM_NetworkSettings :    
{  
    UInt32 MeteredNetworkUsage;  
};  
```  

## Methods  
 The `CCM_NetworkSettings` class does not define any methods.  

## Properties  
 `MeteredNetworkUsage`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Client communications on metered connections. Default is **Block**. Possible values are:   

|Value|Metered network usage policy|
|-|-|
|0|Unknown|
|1|Allow|
|2|Limit|
|4|Block|

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
