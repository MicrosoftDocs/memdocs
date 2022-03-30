---
description: Learn how to change the source site code using SetSourceSite Windows Management Instrumentation (WMI) class method.
title: SetSourceSite method in class SMS_ContentPackage
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 6057c670-f3c8-4632-9a06-777f68a41dba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SetSourceSite Method in Class SMS_ContentPackage
The `SetSourceSite` Windows Management Instrumentation (WMI) class method, in Configuration Manager, changes the source site code.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 SetSourceSite(  
     string SourceSite  
);  
```  

#### Parameters  
 `SourceSite`  
 Data type: `String` Array  

 Qualifiers: `[in]`  

 The site code of the source site for the package.  

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
