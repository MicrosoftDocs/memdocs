---
title: "SMS_Role Class"
titleSuffix: "Configuration Manager"
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
ms.assetid: 4dd6209a-9074-4b70-8f19-7814cfef2c62searchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_Role Server WMI Class
The `SMS_Role` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents an RBA role.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_Role : SMS_BaseClass  
{  
    String CopiedFromID;  
    String CreatedBy;  
    DateTime CreatedDate;  
    Boolean IsBuiltIn;  
    Boolean IsSecAdminRole;  
    String LastModifiedBy;  
    DateTime LastModifiedDate;  
    UInt32 NumberOfAdmins;  
    SMS_ARoleOperation Operations[];  
    String RoleDescription;  
    String RoleID;  
    String RoleName;  
    String SourceSite;  
};  
```  

## Methods  
 The following table lists the methods in the `SMS_Role` class.  

|Method|Description|  
|------------|-----------------|  
|[ExportRole Method in Class SMS_Role](../../../../../develop/reference/core/servers/configure/exportrole-method-in-class-sms_role.md)|Exports roles to an XML string.|  
|[ImportRole Method in Class SMS_Role](../../../../../develop/reference/core/servers/configure/importrole-method-in-class-sms_role.md)|Imports a role defined by an XML string to the database.|  

## Properties  
 `CopiedFromID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [sizelimit(“8��?)]  

 Role ID from which this role was copied.  

 `CreatedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read, SizeLimit(“512��?)]  

 Name of the user that created this role.  

 `CreatedDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Date that the role was created.  

 `IsBuiltIn`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true`, if this is a built-in role.  

 `IsSecAdminRole`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read, lazy]  

 `true`, if this role as a secured admin role. The role is security admin role if the role has can create or modify admin permission.  

 `LastModifiedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read, SizeLimit(“512��?)]  

 The name of the user that last modified the role.  

 `LastModifiedDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 The time when the role was last modified.  

 `NumberOfAdmins`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The number of admin accounts associated with this role.  

 `Operations`  
 Data type: `SMS_ARoleOperation` Array  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 The operations granted to this role.  

 `RoleDescription`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [sizelimit(“512��?)]  

 Description of the role.  

 `RoleID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 The ID of the role. Auto generated when the role was created. This ID will not change during the lifetime of the role and will be unique across sites.  

 `RoleName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null, sizelimit(“256��?)]  

 Name of the role.  

 `SourceSite`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read, SizeLimit(“3��?)]  

 The site code of the site where the role was created.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Role Based Administration Server WMI Classes](../../../../../develop/reference/core/servers/configure/role-based-administration-server-wmi-classes.md)
