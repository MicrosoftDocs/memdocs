---
title: Refresh method in class SMS_ResourceMap
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: a2d1fee0-c1fc-49a2-8c01-73d31732e1d7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# Refresh Method in Class SMS_ResourceMap
The `Refresh` Windows Management Instrumentation (WMI) class method, in Configuration Manager, updates resource (classes derived from [SMS_R_System Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_r_system-server-wmi-class.md)) and inventory (classes derived from [SMS_G_System_Current Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system_current-server-wmi-class.md)) class definitions.  

 The following syntax is simplified from Manage Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 Refresh();  
```  

#### Parameters  
 None.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_ResourceMap Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_resourcemap-server-wmi-class.md)
