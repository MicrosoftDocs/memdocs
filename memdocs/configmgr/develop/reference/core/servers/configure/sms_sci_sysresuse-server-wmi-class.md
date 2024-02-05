---
title: SMS_SCI_SysResUse Class
titleSuffix: Configuration Manager
description: An SMS Provider server class that represents a specific usage of a server or other network resource.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: f2a6e60e-a0df-4c13-9c46-485bd6061da1
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_SCI_SysResUse Server WMI Class
The `SMS_SCI_SysResUse` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a specific usage of a server or other network resource.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SCI_SysResUse : SMS_SiteControlItem  
{  
    UInt32 FileType;  
    String ItemName;  
    String ItemType;  
    String NALPath;  
    String NALType;  
    String NetworkOSPath;  
    SMS_EmbeddedPropertyList PropLists[];  
    SMS_EmbeddedProperty Props[];  
    UInt32 RoleCount;  
    String RoleName;  
    SMS_ServiceWindow ServiceWindows[];  
    String SiteCode;  
    UInt32 SslState;  
    UInt32 Type;  
};  
```  

## Methods  
 The `SMS_SCI_SysResUse` class doesn't define any methods.  

## Properties  
 `FileType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [enumeration, key, enumeration, key]  

 See [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

 `ItemName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, key, read]  

 See [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

 `ItemType`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, key, read]  

 See [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

 `NALPath`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Path to the NAL resource. The default value is "".  

 `NALType`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Friendly name for the `NetworkOSPath` value. For example, "Windows NT Server". The default value is "".  

 `NetworkOSPath`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The network operating system path. The default value is "".  

 `PropLists`  
 Data type: `SMS_EmbeddedPropertyList` Array  

 Access type: Read/Write  

 Qualifiers: none  

 [SMS_EmbeddedPropertyList Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_embeddedpropertylist-server-wmi-class.md) objects for the network resource.  

 `Props`  
 Data type: `SMS_EmbeddedProperty` Array  

 Access type: Read/Write  

 Qualifiers: none  

 [SMS_EmbeddedProperty Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_embeddedproperty-server-wmi-class.md) objects for the network resource.  

 `RoleCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The number of roles.  

 `RoleName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [sizelimit("64"), stringenumeration]  

 Role of the server. The default value is "".  

 `ServiceWindows`  
 Data type: `SMS_ServiceWindow` Array  

 Access type: Read-only  

 Qualifiers: [read, lazy]  

 List of service windows.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key, key, sizelimit]  

 See [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md).  

 `SslState`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, valuemap, values]  

 SSL state description. Possible values are:  

|Value|SSL state|  
|-|-|  
|0|HTTP|  
|1|HTTPS|  
|2|Not applicable. The property is only applicable for a site system role that is client facing.|  
|3|Always HTTPS|  
|4|Always HTTP|  

 `Type`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [enumeration]  

 Returns the site server type if the site system role is colocated on the site server.  Possible values are:  

|Value|Site server type|  
|-|-|  
|1|The site system role is colocated on the secondary site server.|  
|2|The site system role is colocated on the primary site server.|  
|4|The site system role is colocated on the CAS site server.|  
|8|The site system role isn't colocated with any site server.|  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)
