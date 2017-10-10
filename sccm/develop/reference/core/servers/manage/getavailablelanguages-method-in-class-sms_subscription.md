---
title: "GetAvailableLanguages Method"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: 7b950db4-135b-4107-b949-2d9615de4518searchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# GetAvailableLanguages Method in Class SMS_Subscription
The `GetAvailableLanguages` Windows Management Instrumentation (WMI) class method, in System Center Configuration Manager, gets the available languages.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 GetAvailableLanguages(  
     UInt32 LocaleIDs[]  
);  
```  

#### Parameters  
 `LocaleIDs`  
 Data type: `UInt32`  array  

 Qualifiers: `[out]`  

 The identifiers of the locales associated with the localized information.  

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Subscription Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_subscription-server-wmi-class.md)   
 [Alert System WMI Server Classes](../../../../../develop/reference/core/servers/manage/alert-system-server-wmi-classes.md)
