---
title: "DeleteForUser Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: af6c7a1c-824e-4ccd-ac51-c3b20df3d543
author: aczechowski
ms.author: aaroncz
manager: dougeby


---
# DeleteForUser Method in Class SMS_ClientPfxCertificate
The `DeleteForUse` Windows Management Instrumentation (WMI) class method, in Configuration Manager, deletes a certificate for a user.  

## Syntax  

```  
 sint32 DeleteForUser(  
     String ProfileName,  
     String UserName,  
     String Thumbprint  
);  

```  

#### Parameters  
 `ProfileName`  
 Data type: `String`  

 Qualifiers: [in]  

 The profile name.  

 `UserName`  
 Data type: `String`  

 Qualifiers: [in]  

 The user name.  

 `Thumbprint`  
 Data type: `String`  

 Qualifiers: [in]  

 The thumbprint for the certificate.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_ClientPfxCertificate Server WMI Class](../../../../../develop/reference/core/clients/deploy/sms_clientpfxcertificate-server-wmi-class.md)   
