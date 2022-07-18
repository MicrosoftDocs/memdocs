---
title: "Commit Method"
titleSuffix: "Configuration Manager"
description: "A Windows Management Instrumentation class method, which indicates that the content package is ready for processing."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 0765d2ae-4d37-4caf-9393-f66ceb5e50d2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# Commit Method in Class SMS_ContentPackage
The `Commit` Windows Management Instrumentation (WMI) class method, in Configuration Manager, indicates that the content package is ready for processing.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 Commit();  
```  

#### Parameters  
 None.  

## Remarks  
 This method needs to be called when all the contents have been added to the content package to start package processing.  

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
