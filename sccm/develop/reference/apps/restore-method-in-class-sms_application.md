---
title: "Restore Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: c25cbbc4-8dd7-46a5-bf53-61ffc53a23cb
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Restore Method in Class SMS_Application
The `Restore` Windows Management Instrumentation (WMI) class method, in Configuration Manager, restores this application and related deployment type as a current active application.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 Restore();  
```  

#### Parameters  
 None.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Application Server WMI Class](../../../develop/reference/apps/sms_application-server-wmi-class.md)   
 [Configuration Manager Application Management Server WMI Classes](../../../develop/reference/apps/application-management-server-wmi-classes.md)
