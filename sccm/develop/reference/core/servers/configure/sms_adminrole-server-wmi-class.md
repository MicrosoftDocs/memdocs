---
title: "SMS_AdminRole Class"
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
ms.assetid: d08cc68b-533b-4679-ac06-e14686ecd234searchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_AdminRole Server WMI Class
The `SMS_AdminRole` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the association between the admin account and the security role.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_AdminRole : SMS_BaseClass  
{  
    UInt32 AdminID;  
    String RoleID;  
};  
```  

## Methods  
 The `SMS_AdminRole` class does not define any methods.  

## Properties  
 `AdminID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 ID of the admin account.  

 `RoleID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 ID of the security role.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Role Based Administration Server WMI Classes](../../../../../develop/reference/core/servers/configure/role-based-administration-server-wmi-classes.md)
