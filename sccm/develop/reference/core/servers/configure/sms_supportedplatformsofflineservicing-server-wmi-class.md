---
title: "SMS_SupportedPlatformsOfflineServicing Class"
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
ms.assetid: 0d06ee26-6406-4acd-b1bc-3fa925066c3csearchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_SupportedPlatformsOfflineServicing Server WMI Class
The `SMS_SupportedPlatformsOfflineServicing` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that used to determine which operating system images can be serviced offline.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SupportedPlatformsOfflineServicing : SMS_BaseClass  
{  
    String Name;  
    String OsVersionBuild;  
    String ProductType;  
};  
```  

## Methods  
 The `SMS_SupportedPlatformsOfflineServicing` class does not define any methods.  

## Properties  
 `Name`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key, not_null]  

 The name of the operating system that supports offline servicing, such as "Windows 8" or "Windows 8 Server".  

 `OsVersionBuild`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key, not_null]  

 The version and build number of Windows that supports offline servicing, such as 6.0.6001.  

 `ProductType`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key, not_null]  

 Product type. Two string values are used: "WinNT" - to indicate a client operating system type, "ServerNT" - to indicate server operating system type. Possible values are:  

|String Value|Operating System Type|  
|------------------|---------------------------|  
|ServerNT|Server|  
|WinNT|Client|  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Software Distribution Server WMI Classes](../../../../../develop/reference/core/servers/configure/software-distribution-server-wmi-classes.md)
