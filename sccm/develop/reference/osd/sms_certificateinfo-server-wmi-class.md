---
title: "SMS_CertificateInfo Class"
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
ms.assetid: 85ab0d42-8469-4085-a346-ae7ce6e3c14bsearchScope: - ConfigMgr SDK
caps.latest.revision: 12
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_CertificateInfo Server WMI Class
The `SMS_CertificateInfo` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that defines a media certificate registered by Configuration Manager and used by client computers to communicate with a management point.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_CertificateInfo : SMS_BaseClass  
{  
      String Certificate;  
      Boolean IsApproved;  
      Boolean IsBlocked;  
      String IssuedTo;  
      SInt32 KeyType;  
      String PublicKey;  
      String SMSID;  
      String Thumbprint;  
      UInt32 Type;  
      DateTime ValidFrom;  
      DateTime ValidUntil;  
};  
```  

## Methods  
 The following table shows the methods in `SMS_CertificateInfo`.  

|Name|Description|  
|----------|-----------------|  
|[BlockCertificate Method in Class SMS_CertificateInfo](../../../develop/reference/osd/blockcertificate-method-in-class-sms_certificateinfo.md)|Blocks or unblocks the specified certificate.|  

## Properties  
 `Certificate`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [large, lazy]  

 The certification content.  

 `IsApproved`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if the certificate is approved.  

 `IsBlocked`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if the certificate is blocked. A blocked certificate is rejected by the site database. See the [BlockCertificate Method in Class SMS_CertificateInfo](../../../develop/reference/osd/blockcertificate-method-in-class-sms_certificateinfo.md).  

 `IssuedTo`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The identity of the client.  

 `KeyType`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The public key type for the certificate. Possible values are:  

|||  
|-|-|  
|1|self-sign|  
|2|issued|  

 `PublicKey`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 Public key of the certificate, which reflects the globally unique SHA-1 hash thumbprint indicated by the `Thumbprint` property.  

 `SMSID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The GUID used to identify the certificate.  

 `Thumbprint`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Lazy]  

 Hash value of the certificate.  

 `Type`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The type of certificate. Possible values are:  

|||  
|-|-|  
|1|Boot Media|  
|2|PXE|  
|3|ISVProxy|  

 `ValidFrom`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 Date and time when the certificate becomes effective.  

 `ValidUntil`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 Date and time when the certificate expires.  

## Remarks  
 Class qualifiers for this class include:  

-   Read (read-only)  

 For more information about both the class qualifiers and the property qualifiers that are included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Operating System Deployment Server WMI Classes](../../../develop/reference/osd/operating-system-deployment-server-wmi-classes.md)   
 [BlockCertificate Method in Class SMS_CertificateInfo](../../../develop/reference/osd/blockcertificate-method-in-class-sms_certificateinfo.md)   
 [SMS_PXECertificateInfo Server WMI Class](../../../develop/reference/osd/sms_pxecertificateinfo-server-wmi-class.md)
