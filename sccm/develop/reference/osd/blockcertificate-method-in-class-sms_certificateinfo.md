---
title: "BlockCertificate Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: f477e086-3a1b-46fb-b957-1e63e9d6602b
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# BlockCertificate Method in Class SMS_CertificateInfo
The `BlockCertificate` Windows Management Instrumentation (WMI) class method, in Configuration Manager, blocks or unblocks the specified certificate.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 BlockCertificate(  
      String SMSID,  
      Boolean Blocked  
);  
```  

#### Parameters  
 `SMSID`  
 Data type: `String`  

 Qualifiers: [in]  

 The GUID used to identify the certificate. This identifier is defined by the `SMSID` property of [SMS_CertificateInfo Server WMI Class](../../../develop/reference/osd/sms_certificateinfo-server-wmi-class.md).  

 `Blocked`  
 Data type: `Boolean`  

 Qualifiers: [in]  

 `true`, by default, to block the certificate. A blocked certificate is rejected by the site database. See the Remarks section later in this topic.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  
 The value furnished for the `Blocked` parameter directly affects the setting of the `IsBlocked` property of [SMS_CertificateInfo Server WMI Class](../../../develop/reference/osd/sms_certificateinfo-server-wmi-class.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_CertificateInfo Server WMI Class](../../../develop/reference/osd/sms_certificateinfo-server-wmi-class.md)
