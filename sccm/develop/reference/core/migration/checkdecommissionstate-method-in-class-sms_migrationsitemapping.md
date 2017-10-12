---
title: "CheckDecommissionState Method"
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
ms.assetid: a85dc34d-ddf7-4ac2-bbf5-0529406b568dsearchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# CheckDecommissionState Method in Class SMS_MigrationSiteMapping
The `CheckDecommissionState` Windows Management Instrumentation (WMI) class method, in System Center Configuration Manager, checks to see if site mapping can be decommissioned.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 CheckDecommissionState();  
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
