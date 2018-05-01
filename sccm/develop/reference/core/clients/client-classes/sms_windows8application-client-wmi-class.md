---
title: "SMS_Windows8Application Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: a8d947db-3396-42df-a01a-cfb9665ebf81
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_Windows8Application Client WMI Class
In Configuration Manager, the `SMS_Windows8Application` class is a client Windows Management Instrumentation (WMI) class that defines a Windows 8 style application or a Windows Store application.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_Windows8Application  
{  
      String ApplicationName;  
      String Architecture;  
      String DependencyApplicationNames;  
      String FamilyName;  
      String FullName;  
      String InstalledLocation;  
      Boolean IsFramework;  
      Boolean ConfigMgrManaged;  
      String Publisher;  
      String PublisherId;  
      String Version;  
};  
```  

## Methods  
 The `SMS_Windows8Application` class does not define any methods.  

## Properties  
 `ApplicationName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Name of the application.  

 `Architecture`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Specifies the processor architecture supported by an application. Possible values are:  

|Value|Description|  
|-----------|-----------------|  
|X86 or x86|The x86 processor architecture.|  
|Arm or arm|The ARM processor architecture.|  
|X64 or x64|The x64 processor architecture.|  
|Neutral or neutral|A neutral processor architecture.|  
|Unknown or unknown|An unknown processor architecture.|  

 `DependencyApplicationNames`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Dependency application names.  

 `FamilyName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Family name.  

 `FullName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Full name.  

 `InstalledLocation`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Installation location.  

 `IsFramework`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if another application can declare a dependency on this application.  

 `ConfigMgrManaged`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if the application is managed by Configuration Manager.  

 `Publisher`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Application publisher.  

 `PublisherId`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Application publisher identifier.  

 `Version`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Application version.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Inventory Agent Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/inventory-agent-client-wmi-classes.md)
