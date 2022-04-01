---
title: "Unlock Method in SMS_DriverPackage"
titleSuffix: "Configuration Manager"
description: "Set the source site to the current site, unlocking the driver package."  
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 082d6a5f-f16f-47e7-b314-d65962d13250
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# Unlock Method in Class SMS_DriverPackage
The `Unlock` Windows Management Instrumentation (WMI) class method, in Configuration Manager, sets the source site to the current site, unlocking the driver package.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 Unlock();  
```  

#### Parameters  
 None.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_DriverPackage Server WMI Class](../../../develop/reference/osd/sms_driverpackage-server-wmi-class.md)
