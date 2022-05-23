---
description: Learn how to use the Configuration Manager with the CreateIdentity method to create a PXE certificate identity that is used in the client configuration file.
title: "IPxeAuthClass::ReadIdentity"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 35cbac5e-9acf-45fb-a4a4-392196df8776
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# IPxeAuthClass::ReadIdentity Method
In Configuration Manager, the `ReadIdentity` method reads a PXE certificate identity from the client configuration (PFX) file. The method is used in serializing a certificate from the file.  

## Syntax  

```  
HRESULT ReadIdentity(  
   BSTR FileName,  
   BSTR FilePassword,  
   BSTR SMSID,  
   VARIANT* Identity  
);  
```  

#### Parameters  
 `FileName`  
 Data type: `BSTR`  

 Qualifiers: [in]  

 Name of the client configuration (PFX) file.  

 `FilePassword`  
 Data type: `BSTR`  

 Qualifiers: [in]  

 Password to use for access to the client configuration file.  

 `SMSID`  
 Data type: `BSTR`  

 Qualifiers: [in]  

 The GUID used to identify the certificate. This is the value of the SMSID property in [SMS_CertificateInfo Server WMI Class](../../../../../develop/reference/osd/sms_certificateinfo-server-wmi-class.md).  

 `Identity`  
 Data type: `VARIANT`  

 Qualifiers: [out, retval]  

 PXE certificate identity. The return value can be used with [SubmitRegistrationRecord Method in Class SMS_Site](../../../../../develop/reference/core/servers/configure/submitregistrationrecord-method-in-class-sms_site.md).  

## Return Values  
 An `HRESULT` code. Possible values include, but are not limited to, the following value.  

 S_OK  
 The method succeeded.  

## Remarks  

## See Also  
 [IPxeAuthClass Interface](../../../../../develop/reference/core/clients/client-classes/ipxeauthclass-interface.md)   
 [About Operating System Deployment Site Role Configuration](../../../../../develop/osd/about-operating-system-deployment-site-role-configuration.md)
