---
title: "IPxeAuthClass::CreateIdentity"
description: Learn how to use the CreateIdentity method to create a new self-signed certificate.
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 8966724d-f663-42a9-98a5-d10cfa9a6a5c
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# IPxeAuthClass::CreateIdentity Method
In Configuration Manager, the `CreateIdentity` method creates a PXE certificate identity that is used in the client configuration file. This method is used to create a new self-signed certificate.  

## Syntax  

```  
HRESULT CreateIdentity(  
      BSTR FriendlyName,  
      BSTR SubjectName,  
      BSTR SMSID,  
      VARIANT* StartTime,  
      VARIANT* EndTime,  
      VARIANT* Identity  
);  
```  

#### Parameters  
 `FriendlyName`  
 Data type: `BSTR`  

 Qualifiers: [in]  

 Friendly name of the certificate identity.  

 `SubjectName`  
 Data type: `BSTR`  

 Qualifiers: [in]  

 Name of the certificate subject.  

 `SMSID`  
 Data type: `BSTR`  

 Qualifiers: [in]  

 The GUID used to identify the certificate. This is the value of the SMSID property in [SMS_CertificateInfo Server WMI Class](../../../../../develop/reference/osd/sms_certificateinfo-server-wmi-class.md).  

 `StartTime`  
 Data type: `VARIANT`  

 Qualifiers: [in]  

 Time when the certificate becomes valid.  

 `EndTime`  
 Data type: `VARIANT`  

 Qualifiers: [in]  

 Time when the validity of the certificate ends.  

 `Identity`  
 Data type: `VARIANT`  

 Qualifiers: [out, retval]  

 PXE certificate identity. Can be used with [SubmitRegistrationRecord Method in Class SMS_Site](../../../../../develop/reference/core/servers/configure/submitregistrationrecord-method-in-class-sms_site.md).  

## Return Values  
 An `HRESULT` code. Possible values include, but are not limited to, the following value.  

 S_OK  
 The method succeeded.  

## Remarks  

## See Also  
 [IPxeAuthClass Interface](../../../../../develop/reference/core/clients/client-classes/ipxeauthclass-interface.md)   
 [About Operating System Deployment Site Role Configuration](../../../../../develop/osd/about-operating-system-deployment-site-role-configuration.md)
