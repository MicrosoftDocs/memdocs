---
description: The SMS_AssociatedSecuredCategory WMI class is an SMS Provider server class, in Configuration Manager, that represents the list of RBA security categories associated with the current admin user.
title: "SMS_AssociatedSecuredCategory Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 8e8b2e66-0bf2-4029-a5dd-7bf0b7d3dc44
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_AssociatedSecuredCategory Server WMI Class
The `SMS_AssociatedSecuredCategory` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the list of RBA security categories associated with the current admin user.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_AssociatedSecuredCategory : SMS_BaseClass  
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
    UInt32 ObjectTypeID;  
    String SourceSite;  
};  
```  

## Methods  
 The `SMS_AssociatedSecuredCategory` class does not define any methods.  

## Properties  
 `CategoryDescription`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read, sizelimit("512")]  

 Description of the RBA security category.  

 `CategoryID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 ID of the RBA security category.  

 `CategoryName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read, sizelimit("256")]  

 Name of the RBA security category.  

 `CreatedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read, SizeLimit("512")]  

 The user who created the RBA security category.  

 `CreatedDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 The date when the RBA security category was created.  

 `IsBuiltIn`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true`, if this is a built-in RBA security category (All or Default).  

 `LastModifiedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read, SizeLimit("512")]  

 The user who last modified this RBA security category.  

 `LastModifiedDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 The date when this RBA security category was last modified.  

 `NumberOfAdmins`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Number of RBA admins associated with this RBA security category.  

 `NumberOfObjects`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Number of objects associated with this RBA security category.  

 `ObjectTypeID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 The object type of the object which the current user can assign to this RBA security category.  

 `SourceSite`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read, SizeLimit("3")]  

 The source site of the RBA security category.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
