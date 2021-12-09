---
title: "SMS_BulkEnrollmentProfiles Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: b958ac99-cf9a-4dd3-aa52-0235cf6033b0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_BulkEnrollmentProfiles Server WMI Class
The  `SMS_BulkEnrollmentProfiles` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents bulk enrollment profiles for Windows Embedded handheld devices.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_BulkEnrollmentProfiles : SMS_BaseClass  
{  
    String Certificate_CI_UniqueID[];  
    UInt32 EnrollmentProxyPointType;  
    String EnrollProxyPointServerNames[];  
    DateTime ExpirationDate;  
    String FriendlyNamePrefix;  
    UInt32 ID;  
    Boolean IsEnabled;  
    String ProfileDescription;  
    UInt32 ProfileID;  
    String ProfileName;  
    UInt32 ProxyPort;  
    String ProxyServer;  
    String Thumbprint;  
    String UserName;  
    String Wifi_CI_UniqueID;  
};  

```  

## Methods  
 The following table lists the methods in the `SMS_BulkEnrollmentProfiles` class.  

|Method|Description|  
|------------|-----------------|  
|[GenerateProvisioningXML Method in Class SMS_BulkEnrollmentProfiles](../../../develop/reference/mdm/generateprovisioningxml-method-in-class-sms_bulkenrollmentprofiles.md)|Generates provisioning data in XML format.|  

## Properties  
 `Certificate_CI_UniqueID`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: none  

 The unique ID for a certificate configuration item.  

 `EnrollmentProxyPointType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [enumeration]  

 Specifies the type of URL for all enrollment proxy points. Possible values are:  

| Value | Enrollment Proxy Point type |
| ----- | --------------------------- |
|0|NONE|  
|1|INTERNET|  
|2|INTRANET|  

 `EnrollProxyPointServerNames`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: none  

 The name of the enrollment proxy point server.  

 `ExpirationDate`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 The expiration date of the certificate.  

 `FriendlyNamePrefix`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The friendly name prefix for the device.  

 `ID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 A unique profile ID.  

 `IsEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 Indicates whether the profile is enabled.  

 `ProfileDescription`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 A description of the profile.  

 `ProfileID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The ID of the device enrollment profile.  

 `ProfileName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The name of the device enrollment profile.  

 `ProxyPort`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The proxy port number.  

 `ProxyServer`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The proxy server.  

 `Thumbprint`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The thumbprint of the certificate.  

 `UserName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The user name.  

 `Wifi_CI_UniqueID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The unique ID for a Wi-Fi configuration item.  

## Remarks  
 Class qualifiers for this class include:  

- Dynamic  

- Secured  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
