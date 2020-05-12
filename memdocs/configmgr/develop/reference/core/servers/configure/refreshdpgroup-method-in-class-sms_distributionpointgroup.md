---
title: "RefreshDPGroup Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: e5448fd5-9eff-49e3-88d0-2b3299561a37
author: aczechowski
ms.author: aaroncz
manager: dougeby


---
# RefreshDPGroup Method in Class SMS_DistributionPointGroup
The `RefreshDPGroup` Windows Management Instrumentation (WMI) class method, in Configuration Manager, refreshes all of the member distribution points with the latest version of the targeted packages.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 RefreshDPGroup();  
```  

#### Parameters  
 None.  

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Application Server WMI Class](../../../../../develop/reference/apps/sms_application-server-wmi-class.md)   
