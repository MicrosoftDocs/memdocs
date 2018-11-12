---
title: "SMS_AMTCertificate Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: fc88625c-f02c-4711-a9de-4a5d76fc9371
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_AMTCertificate Server WMI Class
The `SMS_AMTCertificate` Windows Management Instrumentation (WMI) class, in System Center Configuration Manager, contains the Intel Active Management technology (Intel AMT) certificates, which are registered to the server. This is a read-only class.  

> [!IMPORTANT]
>  This class is deprecated.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_AMTCertificate : SMS_BaseClass   
{   
    String CAFqdn;  
    String CAName;  
    String CARequestID;  
    UInt32 CAType;  
    UInt32 CertID;  
    SInt32 CertificateStatus;  
    String CertTemplate;  
    UInt32 CertType;  
    UInt32 ChainLength;  
    String ClientIdentity;  
    String SiteCode;  
    String Thumbprint;  
    DateTime ValidFrom;  
    DateTime ValidUntil;  
};  
```  

## Methods  
 The `SMS_AMTCertificate` class does not define any methods.  

## Properties  
 `CAFqdn`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Certification authority (CA) fully qualified domain name (FQDN) for request client certificate.  

 `CAName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 CA Name for request client certificate.  

 `CARequestID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 CA Request ID for request client certificate.  

 `CAType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 CA Type for request client certificate.  

 `CertID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: key  

 ID of certificate  

 `CertificateStatus`  
 Data type: `SInt32`  

 Access type: Read-only  

 Qualifiers: enumeration("RequestPending(1), RequestSuccess(2),IssuedToAMT(3),Revoked(4),Active(5)")  

 Certificate status. Possible values are:  

|Value|Description|  
|-----------|-----------------|  
|1|Request is pending.|  
|2|Request was successful.|  
|3|Has been issued to AMT.|  
|4|Has been revoked.|  
|5|Is currently active.|  

 `CertTemplate`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Certificate Template for request client certificate.  

 `CertType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: enumeration("AMTDevice(1),Provision(2),TrustRoot(3),Console(4)")  

 Type of certificate. Possible values are:  

|Value|Description|  
|-----------|-----------------|  
|1|AMT device|  
|2|Provision|  
|3|Trusted root|  
|4|Console|  

 `ChainLength`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 Certificate chain length.  

 `ClientIdentity`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Client identity.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: none  

 Site code for the site of this certificate.  

 `Thumbprint`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Thumbprint of certificate.  

 `ValidFrom`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: None  

 Date-time stamp of when the certificate validity started.  

 `ValidUntil`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: None  

 Date-time stamp of when the certificate expires.  

## Remarks  
 This class is used to create or update the trust root certificate for a wireless or wired profile. For more information, see [SubmitAMTCert Method in Class SMS_Site](../../../develop/reference/core/servers/configure/submitamtcert-method-in-class-sms_site.md).  

 Class qualifiers for this class include:  

-   DisplayName("AMT Certificates")  

-   Dynamic  

-   Provider("ExtnProv")  

-   Read  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Collections](../../../develop/core/clients/collections/collections.md)   
 [Configuration Manager Supporting Classes](../../../develop/reference/misc/supporting-server-wmi-classes.md)   
 [AMTOperateForCollection Method in Class SMS_Collection](../../../develop/reference/core/clients/collections/amtoperateforcollection-method-in-class-sms_collection.md)   
 [AMTOperateForMachines Method in Class SMS_Collection](../../../develop/reference/core/clients/collections/amtoperateformachines-method-in-class-sms_collection.md)
