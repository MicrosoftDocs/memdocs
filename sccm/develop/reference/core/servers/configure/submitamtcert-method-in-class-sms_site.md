---
title: "SubmitAMTCert Method"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: f7aa0ba7-ba01-4c7d-81e1-fa2dfca93f8bsearchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SubmitAMTCert Method in Class SMS_Site
The `SubmitAMTCert` Windows Management Instrumentation (WMI) class method, in Configuration Manager, submits a certificate for a computer that implements Intel Active Management Technology (Intel AMT).  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 SubmitAMTCert(    
     String Certificate,    
     String Password,    
     SInt32 Type  
);  
```  

#### Parameters  
 `Certificate`  
 Data type: `String`  

 Qualifiers: [in, optional]  

 Hexadecimal-encoded certificate.  

 `Password`  
 Data type: `String`  

 Qualifiers: [in, optional]  

 The password for Personal Information Exchange (PFX) Certificate, if needed.  

 `Type`  
 Data type: `SInt32`  

 Qualifiers: [in, optional]  

 The type of certificate. If omitted, the default value is `4`. Possible values are:  

|Value|Description|  
|-----------|-----------------|  
|4|Root certificate. Currently unimplemented.|  
|5|Provisioning certificate. Indicates that this certificate will be used by an Out of Band service point provisioning server to authenticate Intel AMT firmware during Transport Layer Security (TLS) handshaking|  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md)
