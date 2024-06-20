---
description: Learn how to define a media certificate that is registered by Configuration Manager and used by PXE clients to communicate with a management point.
title: SMS_PXECertificateInfo Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 8a647b49-306e-427e-93e8-1c0f479246da
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_PXECertificateInfo Server WMI Class
The `SMS_PXECertificateInfo` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that defines a media certificate that is registered by Configuration Manager and used by PXE clients to communicate with a management point.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_PXECertificateInfo : SMS_CertificateInfo  
{  
      String Certificate;  
      Boolean IsApproved;  
      Boolean IsBlocked;  
      String IssuedTo;  
      SInt32 KeyType;  
      String PublicKey;  
      String PXEServerName;  
      String SMSID;  
      String Thumbprint;  
      UInt32 Type;  
      DateTime ValidFrom;  
      DateTime ValidUntil;  
};  
```  

## Methods  
 The `SMS_PXECertificateInfo` class does not define any methods.  

## Properties  
 `Certificate`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [large, lazy]  

 See [SMS_CertificateInfo Server WMI Class](../../../develop/reference/osd/sms_certificateinfo-server-wmi-class.md).  

 `IsApproved`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_CertificateInfo Server WMI Class](../../../develop/reference/osd/sms_certificateinfo-server-wmi-class.md).  

 `IsBlocked`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_CertificateInfo Server WMI Class](../../../develop/reference/osd/sms_certificateinfo-server-wmi-class.md).  

 `IssuedTo`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_CertificateInfo Server WMI Class](../../../develop/reference/osd/sms_certificateinfo-server-wmi-class.md).  

 `KeyType`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_CertificateInfo Server WMI Class](../../../develop/reference/osd/sms_certificateinfo-server-wmi-class.md).  

 `PublicKey`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 See [SMS_CertificateInfo Server WMI Class](../../../develop/reference/osd/sms_certificateinfo-server-wmi-class.md).  

 `PXEServerName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The name of the PXE server to which the PXE certificate belongs.  

 `SMSID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 See [SMS_CertificateInfo Server WMI Class](../../../develop/reference/osd/sms_certificateinfo-server-wmi-class.md).  

 `Thumbprint`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Lazy]  

 See [SMS_CertificateInfo Server WMI Class](../../../develop/reference/osd/sms_certificateinfo-server-wmi-class.md).  

 `Type`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_CertificateInfo Server WMI Class](../../../develop/reference/osd/sms_certificateinfo-server-wmi-class.md).  

 `ValidFrom`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_CertificateInfo Server WMI Class](../../../develop/reference/osd/sms_certificateinfo-server-wmi-class.md).  

 `ValidUntil`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_CertificateInfo Server WMI Class](../../../develop/reference/osd/sms_certificateinfo-server-wmi-class.md).  

## Remarks  
 Class qualifiers for this class include:  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See also

[SMS_CertificateInfo server WMI class](sms_certificateinfo-server-wmi-class.md)
