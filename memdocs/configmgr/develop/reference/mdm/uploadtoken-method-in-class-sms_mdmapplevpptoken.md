---
title: "UploadToken Method"
titleSuffix: "Configuration Manager"
description: "The UploadToken WMI class method uploads an Apple Volume Purchase Program (VPP) token to Microsoft Intune."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: ec148faa-654f-46ce-ba73-5910ad45bada
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


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
