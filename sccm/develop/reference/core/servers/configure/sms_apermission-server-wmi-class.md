---
title: "SMS_APermission Class"
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
ms.assetid: a1491aa9-1def-4e35-923a-84bb1e1a1bf0searchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_APermission Server WMI Class
The `SMS_APermission` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that is embedded by `SMS_Admin` and describes the permission granted to a specific admin.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_APermission :    
{  
    String CategoryID;  
    String CategoryName;  
    UInt32 CategoryTypeID;  
    String RoleID;  
    String RoleName;  
};  
```  

## Methods  
 The `SMS_APermission` class does not define any methods.  

## Properties  
 `CategoryID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 ID of the associated RBA security category or collection.  

 `CategoryName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Name of the RBA security category or collection.  

 `CategoryTypeID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [enumeration]  

 The type of category. The default value is 29.  

|||  
|-|-|  
|1|Collection|  
|29|SecuredScope|  

 `RoleID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 ID of the security role.  

 `RoleName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Name of the role.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Role Based Administration Server WMI Classes](../../../../../develop/reference/core/servers/configure/role-based-administration-server-wmi-classes.md)
