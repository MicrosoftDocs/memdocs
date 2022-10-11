---
title: DeleteCertificate Method
titleSuffix: Configuration Manager
description: In Configuration Manager, the DeleteCertificate WMI class method that deletes the certificate from the database.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 246d0ad5-582b-4c6d-9611-0e200c47f354
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# DeleteCertificate Method in Class SMS_CertificateData
The `DeleteCertificate` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that deletes the certificate from the database.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 DeleteCertificate(  
    [IN] UInt32 CertType  
);  

```  

## Parameters  
 `CertType`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 Certificate type.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
