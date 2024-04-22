---
description: Learn how to use the GetAvailableLanguages method on the SMS_Subscription class to obtain a list of available languages.
title: GetAvailableLanguages Method
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 7b950db4-135b-4107-b949-2d9615de4518
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# GetAvailableLanguages Method in Class SMS_Subscription
The `GetAvailableLanguages` Windows Management Instrumentation (WMI) class method, in Configuration Manager, gets the available languages.  

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

## See also

[SMS_Alert server WMI class](sms_alert-server-wmi-class.md)
