---
title: "UploadToken Method"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ec148faa-654f-46ce-ba73-5910ad45badasearchScope: - ConfigMgr SDK
caps.latest.revision: 4
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# UploadToken Method in Class SMS_MDMAppleVppToken
The `UploadToken` Windows Management Instrumentation (WMI) class method, in Configuration Manager, uploads an Apple Volume Purchase Program (VPP) token to Microsoft Intune.  

## Syntax  

```  
sint32 UploadToken(  
     String TokenID,   
     String VppToken,  
     String OrganizationName,   
     String ExpirationDate  
);  

```  

#### Parameters  
 `TokenID`  
 Data type: `String`  

 Qualifiers: [in]  

 The ID of the Apple VPP token.  

 `VppToken`  
 Data type: `String`  

 Qualifiers: [in]  

 Name of the token.  

 `OrganizationName`  
 Data type: `String`  

 Qualifiers: [in]  

 Organization name for the token.  

 `ExpirationDate`  
 Data type: `String`  

 Qualifiers: [in]  

 Expiration date of the token.  

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
