---
title: "RefreshPkgSource Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 26332303-5803-4daf-80e0-891458cd64de
author: aczechowski
ms.author: aaroncz
manager: dougeby


---
# RefreshPkgSource Method in Class SMS_ContentPackage
The `RefreshPkgSource` Windows Management Instrumentation (WMI) class method, in Configuration Manager, causes a refresh of the package source.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 RefreshPkgSource();  
```  

#### Parameters  
 None.  

## Remarks  
 This method is used when the package properties have not changed.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Application Server WMI Class](../../../../../develop/reference/apps/sms_application-server-wmi-class.md)   
