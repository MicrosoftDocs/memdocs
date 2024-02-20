---
title: SMS_DPGroupPackages Class
titleSuffix: Configuration Manager
description: The SMS_DPGroupPackages WMI class is an SMS Provider server class that represents distribution point packages.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 3c646042-3102-4444-8672-ab8c9a095882
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_DPGroupPackages Server WMI Class
The `SMS_DPGroupPackages` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents distribution point packages.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DPGroupPackages : SMS_BaseClass  
{  
    String GroupID;  
    String PkgID;  
};  
```  

## Methods  
 The `SMS_DPGroupPackages` class does not define any methods.  

## Properties  
 `GroupID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Unique identifier for the distribution point group.  

 `PkgID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Package associated with the distribution point group.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
