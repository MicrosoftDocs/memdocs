---
title: SMS_SecuredCategory Class
titleSuffix: Configuration Manager
description: The SMS_SecuredCategory Windows Management Instrumentation class is an SMS Provider server class, in Configuration Manager, that represents the RBA security category.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 25ae1991-bb85-400b-be7e-7efed4575a57
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_SecuredCategory Server WMI Class
The `SMS_SecuredCategory` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the RBA security category. An RBA security category defines a set of objects associated with it.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SecuredCategory : SMS_BaseClass  
{  
    String CategoryDescription;  
    String CategoryID;  
    String CategoryName;  
    String CreatedBy;  
    DateTime CreatedDate;  
    Boolean IsBuiltIn;  
    String LastModifiedBy;  
    DateTime LastModifiedDate;  
    UInt32 NumberOfAdmins;  
    UInt32 NumberOfObjects;  
    String SourceSite;  
};  
```  

## Methods  
 The `SMS_SecuredCategory` class does not define any methods.  

## Properties  
 `CategoryDescription`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [sizelimit("512")]  

 Description of the RBA security category.  

 `CategoryID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 The ID of the RBA security category. Auto generated when the RBA security category is created.  

 `CategoryName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null, sizelimit("256"]  

 Name of the RBA security category.  

 `CreatedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read, SizeLimit("512")]  

 The logon name of the user that created the RBA security category.  

 `CreatedDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 The date when the RBA security category was created.  

 `IsBuiltIn`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true`, if RBA security category is built-in.  

 `LastModifiedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read, SizeLimit("512")]  

 User that last modified the RBA security category.  

 `LastModifiedDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Time when the RBA security category was last modified.  

 `NumberOfAdmins`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Number of admin accounts associated with the RBA security category.  

 `NumberOfObjects`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The number of objects associated with the RBA security category.  

 `SourceSite`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read, SizeLimit("3")]  

 The site where the RBA security category was created.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
