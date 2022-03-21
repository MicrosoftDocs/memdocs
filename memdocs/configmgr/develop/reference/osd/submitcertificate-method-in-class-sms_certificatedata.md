---
title: "SubmitCertificate Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 20eee368-0e55-4c2d-ba2d-561eff98c048
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SubmitCertificate Method in Class SMS_CertificateData
The `SubmitCertificate` Windows Management Instrumentation (WMI) class method, in Configuration Manager, that submits the specified certificate.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 SubmitCertificate   
{  
    [IN]    UInt32 CertType  
    [IN]    UInt8 CertData[]  
    [IN]    UInt8 Password[]  
    [IN]    String Name  
    [IN]    String Description  
};  
```  

## Parameters  
 `CertType`  
 Data type: `UInt32`  

 Qualifiers: [id("0"), in]  

 Required. Certificate type. Possible values are:  

| Value | Certificate type |  
| ----- | ---------------- |  
|1|Windows Intune Subscription|  

 `CertData`  
 Data type: `UInt8 Array`  

 Qualifiers: [id("1"), in]  

 Required. Certificate PFX data.  

 `Password`  
 Data type: `UInt8 Array`  

 Qualifiers: [id("2"), in, optional]  

 Optional. Password to read the certificate PFX data.  

 `Name`  
 Data type: `String`  

 Qualifiers: [id("3"), in, optional]  

 Optional. Certificate name.  

 `Description`  
 Data type: `String`  

 Qualifiers: [id("4"), in, optional]  

 Optional. Certificate description.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_CertificateData Server WMI Class](../../../develop/reference/osd/sms_certificatedata-server-wmi-class.md)
