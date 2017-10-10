---
title: "SMS_DmInvVersion Class"
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
ms.assetid: 08db3d36-8ac8-4904-9466-eb2933023269searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_DmInvVersion Client WMI Class
The `SMS_DmInvVersion` class is a client Windows Management Instrumentation (WMI) class, in Configuration Manager, that represents the device management inventory version.  

## Syntax  

```  
Class SMS_DmInvVersion  
{  
   UInt32 Version  
};  
```  

## Methods  
 The `SMS_ActiveSyncConnectedDevice` class does not define any methods.  

## Properties  
 `Version`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The inventory version.  

## See Also  
 [Device Management Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/device-management-client-wmi-classes.md)
