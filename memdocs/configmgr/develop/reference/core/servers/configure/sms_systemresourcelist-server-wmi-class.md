---
description: Learn how to map network abstraction layer (NAL) paths, resource types, site codes, and role names for system resources located on site servers.
title: SMS_SystemResourceList Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: f43f66b7-5ec4-4a47-91f2-cdbd61654147
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_SystemResourceList Server WMI Class
The `SMS_SystemResourceList` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that maps network abstraction layer (NAL) paths, resource types, site codes, and role names for system resources located on site servers.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SystemResourceList : SMS_BaseClass   
{  
     Boolean InternetEnabled;  
     Boolean InternetShared;  
     String NALPath;  
     String ResourceType;  
     String RoleName;  
     String ServerName,  
     String ServerRemoteName,  
     String SiteCode,  
     UInt32 SslState  
};  
```  

## Methods  
 The `SMS_SystemResourceList` class does not define any methods.  

## Properties  
 `InternetEnabled`  
 Data type: `Boolean`  

 Access type: Read Only  

 Qualifiers: None  

 `true` if this role system resource is Internet enabled. The default value is `false`.  

 `InternetShared`  
 Data type: `Boolean`  

 Access type: Read Only  

 Qualifiers: None  

 `true` if the site system resource instance can serve both internet clients as well as intranet clients. It has meaning only if the `InternetEnabled` property is also set to `true`.  

 `NALPath`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: [key]  

 NAL path of the system resource. The default value is "".  

 `ResourceType`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: [key]  

 Type of the system resource, such as a Windows NT Server. The default value is "".  

 `RoleName`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: [key]  

 Role of the server. The default value is "".  

 `ServerName`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 Name of the server. The default value is "".  

 `ServerRemoteName`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 Fully qualified domain name (FQDN) for the site system on the intranet. The default value is "".  

 `SiteCode`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: [key, SizeLimit("3")]  

 Site that owns the system resource. The default value is "".  

 `SslState`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 SSL state description. Possible values are:  

|Value|SSL state|  
|-|-|  
|0|HTTP|  
|1|HTTPS|  
|2|Not applicable. The property is only applicable for a site system role that is client facing.|  
|3|Always HTTPS|  
|4|Always HTTP|  

## Remarks  
 Class qualifiers for this class include:  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)
