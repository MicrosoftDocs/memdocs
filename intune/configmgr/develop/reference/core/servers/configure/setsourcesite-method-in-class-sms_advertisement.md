---
title: SetSourceSite method in class SMS_Advertisement
description: Learn how the SetSourceSite Windows Management Instrumentation (WMI) class method, in Configuration Manager, sets the source site code for the advertisement.
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: cf608c26-85b1-4ea8-bd06-c066693a9a17
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SetSourceSite Method in Class SMS_Advertisement
The `SetSourceSite` Windows Management Instrumentation (WMI) class method, in Configuration Manager, sets the source site code for the advertisement.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 SetSourceSite(  
     string SourceSite,  
);  
```  

#### Parameters  
 `SourceSite`  
 Data type: `String`  

 Qualifiers: `[in]`  

 The site code of the source site for the advertisement.  

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Advertisement Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_advertisement-server-wmi-class.md)   
