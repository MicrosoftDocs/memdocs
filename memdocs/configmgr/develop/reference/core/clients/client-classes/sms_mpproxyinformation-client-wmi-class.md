---
title: SMS_MPProxyInformation Class
titleSuffix: Configuration Manager
description: A client Windows Management Instrumentation class that represents information about a proxy management point.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: e327907b-13c8-4025-b066-e10dbf299f78
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_MPProxyInformation Client WMI Class
The `SMS_MPProxyInformation` class is a client Windows Management Instrumentation (WMI) class, in Configuration Manager, that represents information about a proxy management point.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_MPProxyInformation  
{  
      String Capabilities;  
      UInt32 Index;  
      String Name;  
      String Protocol;  
      String SiteCode;  
      String State;  
      UInt32 Version;  
};  
```  

## Methods  
 The `SMS_MPProxyInformation` class does not define any methods.  

## Properties  
 `Capabilities`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Capabilities of the proxy management point.  

 `Index`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 For proxy Management Point rotation.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The name of the proxy management point.  

 `Protocol`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The network protocol used by the proxy management point.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The site code of the site for the proxy management point.  

 `State`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The state of the proxy management point.  

 `Version`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The version of the proxy management point.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Client Framework and Data Transfer Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/client-framework-and-data-transfer-client-wmi-classes.md)
