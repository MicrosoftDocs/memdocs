---
title: Deny Method
titleSuffix: Configuration Manager
description: The Deny Windows Management Instrumentation (WMI) class method, in Configuration Manager, denies user application requests.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: e1204ee0-7193-41ff-9061-4bd8ca07a76b
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Deny Method in Class SMS_UserApplicationRequest
The `Deny` Windows Management Instrumentation (WMI) class method, in Configuration Manager, denies user application requests.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 Deny(  
     string Comments  
);  
```  

#### Parameters  
 `Comments`  
 Data type: `String` Array  

 Qualifiers: [in, SizeLimit("2000")]  

 Comments regarding the denial of the application request.  

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_UserApplicationRequest Server WMI Class](../../../develop/reference/apps/sms_userapplicationrequest-server-wmi-class.md)
