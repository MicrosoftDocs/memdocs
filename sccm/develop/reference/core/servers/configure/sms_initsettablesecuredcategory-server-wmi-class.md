---
title: "SMS_InitSettableSecuredCategory Class"
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
ms.assetid: ec147358-e38e-4d43-ac89-d0fffb4511a3searchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_InitSettableSecuredCategory Server WMI Class
The `SMS_InitSettableSecuredCategory` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the list of RBA security categories.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_InitSettableSecuredCategory : SMS_BaseClass  
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
 The `SMS_InitSettableSecuredCategory` class does not define any methods.  

## Properties  
 `CategoryDescription`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read, sizelimit(“512��?)]  

 Description of the RBA security category.  

 `CategoryID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 ID of the RBA security category.  

 `CategoryName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read, sizelimit(“256��?)]  

 Name of the RBA security category.  

 `CreatedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read, SizeLimit(“512��?)]  

 Name of the user who created the RBA security category.  

 `CreatedDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Date the RBA security category was created.  

 `IsBuiltIn`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true`, if this RBA security category is built-in (All or Default).  

 `LastModifiedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read, SizeLimit(“512��?)]  

 User who last modified this RBA security category.  

 `LastModifiedDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Time this RBA security category was last modified.  

 `NumberOfAdmins`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The number of admin accounts associated with this RBA security category.  

 `NumberOfObjects`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The number of objects associated with this RBA security category.  

 `ObjectTypeID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Object type which the current user has permissions to assign to this RBA security category.  

 `SourceSite`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read, SizeLimit(“3��?)]  

 Site where the RBA security category was created.  

## Remarks  
 Current user can assign objects to the RBA security categories specified by this class.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Role Based Administration Server WMI Classes](../../../../../develop/reference/core/servers/configure/role-based-administration-server-wmi-classes.md)
