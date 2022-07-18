---
title: "SMS_DeviceEnrollmentProfile Class"
titleSuffix: "Configuration Manager"
description: "The SMS_DeviceEnrollmentProfile Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a device enrollment profile in the database."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 5a836c27-75a0-4394-8632-e3c591f97326
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_DeviceEnrollmentProfile Server WMI Class
The `SMS_DeviceEnrollmentProfile` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a device enrollment profile in the database.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DeviceEnrollmentProfile : SMS_BaseClass  
{  
    String CertAuthorities[];  
    String CertCIUniqueID;  
    String Description;  
    String DevicesContainerDN;  
    String DevicesGroup;  
    String EnrollmentSiteCode;  
    String ManagementSiteCode;  
    String Name;  
    UInt32 ProfileID;  
    UInt32 ProfileType;  
    UInt32 RecordExpiryMinutes;  
};  
```  

## Methods  
 The `SMS_DeviceEnrollmentProfile` class does not define any methods.  

## Properties  
 `CertAuthorities`  
 Data type: `String` Array  

 Access type: Read/Write  

 Qualifiers: none  

 Each CA must have a properly configured template of CertTemplateName, and must chain to the root certificate trusted by the server hosting the ManagementUri.  

 `CertCIUniqueID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Unique identifier for a certificate configuration item.  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Text describing the profile.  

 `DevicesContainerDN`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The location where device accounts are created.  

 `DevicesGroup`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The Security Group with enroll rights on the CA template.  

 `EnrollmentSiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The site code where devices should enroll.  

 `ManagementSiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The site code from where device should be managed.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The name of the profile. This name must be unique.  

 `ProfileID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Unique identifier to differentiate the profile.  

 `ProfileType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The type of the profile.  

| Value | Profile type |
| ----- | ------------ |
|1|DM|  
|2|AMT|  

 `RecordExpiryMinutes`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Number of minutes for which the record is valid.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Device Management Server WMI Classes](../../../develop/reference/mdm/device-management-server-wmi-classes.md)
