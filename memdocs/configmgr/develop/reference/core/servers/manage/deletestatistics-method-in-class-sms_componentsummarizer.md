---
description: Learn how the DeleteStatistics Windows Management Instrumentation (WMI) class method, in Configuration Manager, deletes status message counts for Configuration Manager components.
title: "DeleteStatistics Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: fe50e71c-973b-4425-893e-6630b60fa388
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# DeleteStatistics Method in Class SMS_ComponentSummarizer
The `DeleteStatistics` Windows Management Instrumentation (WMI) class method, in Configuration Manager, deletes status message counts for Configuration Manager components.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 DeleteStatistics( );  
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
 [SMS_ComponentSummarizer Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_componentsummarizer-server-wmi-class.md)
