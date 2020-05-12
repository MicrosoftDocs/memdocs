---
title: "Stop Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 24a6f364-95bd-4f92-9c68-9edf45f97bc7
author: aczechowski
ms.author: aaroncz
manager: dougeby


---
# Stop Method in Class SMS_MigrationJob
The `Stop` Windows Management Instrumentation (WMI) class method, in Configuration Manager, stops the migration job.  

> [!IMPORTANT]
>  This requires the Manage Migration Job right.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 Stop();  
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
 [SMS_MigrationJob Server WMI Class](../../../../develop/reference/core/migration/sms_migrationjob-server-wmi-class.md)
