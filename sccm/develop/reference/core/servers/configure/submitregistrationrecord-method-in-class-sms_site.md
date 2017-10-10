---
title: "SubmitRegistrationRecord Method"
titleSuffix: "Configuration Manager"
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
ms.assetid: ca40b886-729f-4390-aacf-64878811a96asearchScope: - ConfigMgr SDK
caps.latest.revision: 16
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SubmitRegistrationRecord Method in Class SMS_Site
The `SubmitRegistrationRecord` Windows Management Instrumentation (WMI) class method, in Configuration Manager, submits a registration record.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 SubmitRegistrationRecord(  
     String SMSID,  
     String Certificate,  
     String CertificatePFX,  
     SInt32 Type,  
     String ServerName,  
     SInt32 UdaSetting,  
     SInt32 IssuedCert  
);  
```  

#### Parameters  
 `SMSID`  
 Data type: `String`  

 Qualifiers: [in]  

 The GUID used to identify the certificate. This is the value of the `SMSID` property in [SMS_CertificateInfo Server WMI Class](../../../../../develop/reference/osd/sms_certificateinfo-server-wmi-class.md).  

 `Certificate`  
 Data type: `String`  

 Qualifiers: [in]  

 Hexadecimal-encoded certificate.  

 `CertificatePFX`  
 Data type: `String`  

 Qualifiers: [in, optional]  

 Hexadecimal-encoded private key for PFX file containing the certificate. The default value is "".  

 `Type`  
 Data type: `SInt32`  

 Qualifiers: [in, optional]  

 The type of certificate. Possible values are defined for the `Type` property of [SMS_CertificateInfo Server WMI Class](../../../../../develop/reference/osd/sms_certificateinfo-server-wmi-class.md). The default value for this parameter is BootMedia (1).  

 `ServerNam`  
 Data type: `String`  

 Qualifiers: [in, optional]  

 Name used to identify the server.  

 `UdaSetting`  
 Data type: `SInt32`  

 Qualifiers: [in, optional]  

 UdaSetting. . The default value for this parameter is Disabled (0).  

|||  
|-|-|  
|0|Disabled|  
|1|Pending|  
|2|Auto|  

 `IssuedCert`  
 Data type: `SInt32`  

 Qualifiers: [in, optional]  

 IssuedCert. . The default value for this parameter is 1.  

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
 [ImportMachineEntry Method in Class SMS_Site](../../../../../develop/reference/core/servers/configure/importmachineentry-method-in-class-sms_site.md)   
 [IsUsedCert Method in Class SMS_Site](../../../../../develop/reference/core/servers/configure/isusedcert-method-in-class-sms_site.md)   
 [SMS_CertificateInfo Server WMI Class](../../../../../develop/reference/osd/sms_certificateinfo-server-wmi-class.md)
