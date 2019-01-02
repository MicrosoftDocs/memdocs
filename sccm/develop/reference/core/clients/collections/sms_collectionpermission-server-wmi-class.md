---
title: "SMS_CollectionPermission Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: f2c7789c-c55e-492f-88c7-0e6d8861938b
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_CollectionPermission Server WMI Class
The `SMS_CollectionPermission` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in System Center Configuration Manager, is used to query and define which collection scopes are associated to an RBAC role.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_CollectionPermission : SMS_BaseClass  
{  
      UInt32 AdminID;  
      String CollectionID;  
      String CollectionName;  
      Boolean GrantedToCurrentUser;  
      String LogonName;  
      String RoleID;  
      String RoleName;  
};  
```  

## Methods  
 The `SMS_ CollectionPermission` class does not define any methods.  

## Properties  
 `AdminID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The administrator id from RBAC, which is used to associate the collection between each instance of this class.  

 `CollectionID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The ID that refers to the collection.  

 `CollectionName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The name of the collection.  

 `GrantedToCurrentUser`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 This value will be true if this permission is granted to the current user directly or indirectly (through a Security Group).  

 `LogonName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the resource.  

 `RoleID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The role id from RBAC, which is used to associate the collection between each instance of this class.  

 `RoleName`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The name of the RBAC.   

## Remarks  
 Class qualifiers for this class include:  

- Abstract  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Collections Server WMI Classes](../../../../../develop/reference/core/clients/collections/collections-server-wmi-classes.md)
