---
title: SetIsExpired method in class SMS_ApplicationLatest
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: e9e410e4-78cb-490c-9a22-e12ddf2f2728
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SetIsExpired Method in Class SMS_ApplicationLatest
The `SetIsExpired` Windows Management Instrumentation (WMI) class method, in Configuration Manager, sets the expired status of this application.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 SetIsExpired (  
     boolean Expired  
);  
```  

#### Parameters  
 `Expired`  
 Data type: `Boolean`  

 Qualifiers: [in]  

 `true` to set the state to expired. The default value is `true`.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_ApplicationLatest Server WMI Class](../../../develop/reference/apps/sms_applicationlatest-server-wmi-class.md)   
