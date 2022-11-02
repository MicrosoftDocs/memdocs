---
description: The ImportForUser Windows Management Instrumentation class method, in Configuration Manager, imports a certificate for a user, encrypted by using a password.
title: ImportForUser Method
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 6521620d-03b4-4a3b-9579-4fe211b3b718
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# ImportForUser Method in Class SMS_ClientPfxCertificate
The `ImportForUser` Windows Management Instrumentation (WMI) class method, in Configuration Manager, imports a certificate for a user, encrypted by using a password.  

## Syntax  

```  
sint32 ImportForUser(  
     String ProfileName,  
     String UserName,  
     String EncryptedPfxBlob,  
     String Password  
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

 `EncryptedPfxBlob`  
 Data type: `String`  

 Qualifiers: [in]  

 The encrypted blob.  

 `Password`  
 Data type: `String`  

 Qualifiers: [in]  

 The password used to encrypt the certificate.  

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
