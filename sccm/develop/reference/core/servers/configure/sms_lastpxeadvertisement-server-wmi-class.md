---
title: "SMS_LastPXEAdvertisement Class"
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
ms.assetid: 9522d5d9-b5f4-443d-a51a-518793d4c62bsearchScope: - ConfigMgr SDK
caps.latest.revision: 4
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_LastPXEAdvertisement Server WMI Class
The `SMS_LastPXEAdvertisement` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the last PXE advertisement.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_LastPXEAdvertisement : SMS_BaseClass  
{  
    String AdvertisementID;  
    DateTime LastPXEAdvertisementTime;  
    String NetbiosName;  
    UInt32 ResourceId;  
    String SMBIOSGUID;  
};  
```  

## Methods  
 The `SMS_LastPXEAdvertisement` class does not define any methods.  

## Properties  
 `AdvertisementID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The advertisement ID.  

 `LastPXEAdvertisementTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 The time of last PXE advertisement for this equipment.  

 `NetbiosName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 NetbiosName description … The netbios name.. The default value is …  

 `ResourceId`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Key of the item.  

 `SMBIOSGUID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The GUID of the BIOS.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
