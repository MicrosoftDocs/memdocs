---
title: "SMS_Permission Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 598f0a6c-d67a-4559-b863-616d4044b9c8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


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

|Value|Category type|  
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

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
