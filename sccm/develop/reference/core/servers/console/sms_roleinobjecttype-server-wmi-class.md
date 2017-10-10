---
title: "SMS_RoleInObjectType Class"
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
ms.assetid: 849fb64d-23d4-4642-b5bc-92168a35b2c1searchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_RoleInObjectType Server WMI Class
The `SMS_RoleInObjectType` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that maps a role and its associated object types.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_RoleInObjectType : SMS_BaseClass  
{  
    UInt32 ObjectTypeID;  
    String RoleID;  
};  
```  

## Methods  
 The `SMS_RoleInObjectType` class does not define any methods.  

## Properties  
 `ObjectTypeID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Secured object class ID. Possible values are listed below.  

|||  
|-|-|  
|2|SMS_Package|  
|14|SMS_OperatingSystemInstallPackage|  
|18|SMS_ImagePackage|  
|19|SMS_BootImagePackage|  
|21|SMS_DeviceSettingPackage|  
|23|SMS_DriverPackage|  
|24|SMS_SoftwareUpdatesPackage|  
|31|SMS_Application|  

 `RoleID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The ID of the role.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
