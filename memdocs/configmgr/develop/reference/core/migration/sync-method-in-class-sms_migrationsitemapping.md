---
description: Article detailing the use of the Sync class method in Configuration Manager to synchronize the entities on the source site.
title: Sync Method
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 372a0ba8-4a3c-4dbc-ac41-9c87ce96c0ba
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Sync Method in Class SMS_MigrationSiteMapping
The `Sync` Windows Management Instrumentation (WMI) class method, in Configuration Manager, synchronizes the entities on the source site.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 Sync();  
```  

#### Parameters  
 None.  

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_MigrationSiteMapping Server WMI Class](../../../../develop/reference/core/migration/sms_migrationsitemapping-server-wmi-class.md)
