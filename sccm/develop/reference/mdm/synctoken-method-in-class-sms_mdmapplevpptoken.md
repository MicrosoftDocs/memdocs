---
title: "SyncToken Method"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: da8257d2-4e32-4af9-9313-239127d0aab5searchScope: - ConfigMgr SDK
caps.latest.revision: 3
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
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
 [Mobile Device Management Server WMI Classes](../../../develop/reference/mdm/mobile-device-management-server-wmi-classes.md)
