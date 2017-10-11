---
title: "SMS_Permission Class"
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
ms.assetid: 598f0a6c-d67a-4559-b863-616d4044b9c8searchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_Permission Server WMI Class
The `SMS_Permission` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents RBAC Security User Permissions.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_Permission : SMS_BaseClass  
{  
    UInt32 AdminID;  
    String CategoryID;  
    String CategoryName;  
    UInt32 CategoryTypeID;  
    Boolean GrantedToCurrentUser;  
    String LogonName;  
    String RoleID;  
    String RoleName;  
};  
```  

## Methods  
 The `SMS_Permission` class does not define any methods.  

## Properties  
 `AdminID`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: [key]  

 ID of the admin account.  

 `CategoryID`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key]  

 ID of the RBA security category.  

 `CategoryName`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: None  

 Name of the RBA security category.  

 `CategoryTypeID`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: [enumeration, key]  

 The type of the category. Possible values are listed below. The default value is 29.  

|||  
|-|-|  
|1|Collection|  
|29|SecuredScope|  

 `GrantedToCurrentUser`  
 Data type: `Boolean`  

 Access type: Read  

 Qualifiers: None  

 This value will be true if this permission is granted to current user directly or indirectly (through a Security Group).  

 `LogonName`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: None  

 Logon name of the user.  

 `RoleID`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key]  

 ID of the role.  

 `RoleName`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: None  

 Name of the role.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Role Based Administration Server WMI Classes](../../../../../develop/reference/core/servers/configure/role-based-administration-server-wmi-classes.md)
