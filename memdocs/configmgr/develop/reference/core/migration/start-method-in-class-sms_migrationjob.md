---
title: "Start Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 1f6682fd-3a51-4b5b-a72b-9e5eac591f03
author: aczechowski
ms.author: aaroncz
manager: dougeby


---
# Start Method in Class SMS_MigrationJob
The `Start` Windows Management Instrumentation (WMI) class method, in Configuration Manager, starts the migration job.  

> [!IMPORTANT]
>  This requires the Manage Migration Job right.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 Start();  
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
