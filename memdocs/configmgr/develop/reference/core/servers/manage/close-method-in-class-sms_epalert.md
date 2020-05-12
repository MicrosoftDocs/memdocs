---
title: "Close Method in Class SMS_EPAlert"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 2637f1c4-037b-4f91-b0d3-ce61e9eeb63b
author: aczechowski
ms.author: aaroncz
manager: dougeby


---
# Close Method in Class SMS_EPAlert
The `Close` Windows Management Instrumentation (WMI) class method, in Configuration Manager, postpones the alert.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 Close(  
     string Comments,  
     datetime SkipUntil  
);  
```  

#### Parameters  
 `Comments`  
 Data type: `String`  

 Qualifiers: `[in, optional]`  

 Administrator-supplied comments for the postpone action.  

 `SkipUntil`  
 Data type: `DateTime`  

 Qualifiers: `[out, optional]`  

 Do not start the evaluation until the specified time.  

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
