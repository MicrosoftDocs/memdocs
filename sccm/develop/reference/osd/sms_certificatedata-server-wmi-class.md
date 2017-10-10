---
title: "SMS_CertificateData Class"
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
ms.assetid: f562bbf6-0c47-4dba-abfa-6f684075578dsearchScope: - ConfigMgr SDK
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_CertificateData Server WMI Class
The `SMS_CertificateData` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents certificate data managed by Configuration Manager.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_CertificateData : SMS_BaseClass  
{  
    String CertID;  
    UInt32 CertType;  
    String Description;  
    String Name;  
};  
```  

## Methods  
 The following table lists the methods in the `SMS_CertificateData` class.  

|Method|Description|  
|------------|-----------------|  
|[SubmitCertificate Method in Class SMS_CertificateData](../../../develop/reference/osd/submitcertificate-method-in-class-sms_certificatedata.md)|Submit certificate.|  
|[DeleteCertificate Method in Class SMS_CertificateData](../../../develop/reference/osd/deletecertificate-method-in-class-sms_certificatedata.md)|Deletes the certificate from the database.|  

## Properties  
 `CertID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Certificate unique identifier.  

 `CertType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, read]  

 Certificate type. Possible values are:  

|||  
|-|-|  
|1|Windows Intune Subscription|  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Certificate description.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Certificate name.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
