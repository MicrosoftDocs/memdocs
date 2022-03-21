---
title: "SMS_AdminRole Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: d08cc68b-533b-4679-ac06-e14686ecd234
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


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

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
