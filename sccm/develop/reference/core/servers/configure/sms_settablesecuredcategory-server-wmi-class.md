---
title: "SMS_SettableSecuredCategory Class"
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
ms.assetid: 77b0c79e-0291-4988-8be5-01113494460csearchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_SettableSecuredCategory Server WMI Class
The `SMS_SettableSecuredCategory` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the list of secured categories which the current user can assign to certain types of objects.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SettableSecuredCategory : SMS_BaseClass  
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
 The `SMS_SettableSecuredCategory` class does not define any methods.  

## Properties  
 `CategoryDescription`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read, sizelimit(“512��?)]  

 Description of the security category.  

 `CategoryID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 ID of the security category.  

 `CategoryName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read, sizelimit(“256��?)]  

 Name of the security category.  

 `CreatedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read, SizeLimit(“512��?)]  

 The name of the user who created the security category.  

 `CreatedDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 The date when the security category was created.  

 `IsBuiltIn`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true`, if this is a built-in security category (All or Default).  

 `LastModifiedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read, SizeLimit(“512��?)]  

 The name of the user who last modified the security category.  

 `LastModifiedDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 The date when the security category was last modified.  

 `NumberOfAdmins`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Number of admin accounts associated with this security category.  

 `NumberOfObjects`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Number of objects associated with this security category.  

 `ObjectTypeID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 The object type which the current user has permission to assign to this security category.  

 `SourceSite`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read, SizeLimit(“3��?)]  

 Site where this was security category was created.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_SettableSecuredCategory Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_settablesecuredcategory-server-wmi-class.md)
