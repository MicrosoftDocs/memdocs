---
title: "SyncToken Method"
titleSuffix: "Configuration Manager"
description: "Initiate a synchronization of the Apple Volume Purchase Program (VPP) token."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: da8257d2-4e32-4af9-9313-239127d0aab5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SyncToken Method in Class SMS_MDMAppleVppToken
The `SyncToken` Windows Management Instrumentation (WMI) class method, in Configuration Manager, initiates a synchronization of the Apple Volume Purchase Program (VPP) token.  

## Syntax  

```  
sint32 SyncToken(  
     String TokenID  
);  

```  

#### Parameters  
 `TokenID`  
 Data type: `String`  

 Qualifiers: [in]  

 The ID of the Apple VPP token.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_MDMAppleVppToken Server WMI Class](../../../develop/reference/mdm/sms_mdmapplevpptoken-server-wmi-class.md)   
