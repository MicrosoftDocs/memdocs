---
title: "RequestRefresh Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: fd7b5351-a3ed-40c2-a629-156f22507f88
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# RequestRefresh Method in Class SMS_Collection
The `RequestRefresh` Windows Management Instrumentation (WMI) class method, in System Center Configuration Manager, triggers a re-evaluation of collection membership by the System Center Configuration Manager collection evaluator component.  

 The following syntax is simplified from Managed Object Format (MOF) code and is intended to show the definition of the method.  

## Syntax  

```  
SInt32 RequestRefresh();  
```  

#### Parameters  

> [!NOTE]
>  The previously available parameter `includesubcollections` has been deprecated in System Center Configuration Manager.  

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Collection Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md)   
 [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md)
