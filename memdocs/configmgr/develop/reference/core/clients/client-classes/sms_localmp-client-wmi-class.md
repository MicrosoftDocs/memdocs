---
title: SMS_LocalMP Class
titleSuffix: Configuration Manager
description: The SMS_LocalMP class is a client Windows Management Instrumentation class, in Configuration Manager, that represents the local management point.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 88444515-6694-45a4-b5af-87dfaad22b80
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_LocalMP Client WMI Class
The `SMS_LocalMP` class is a client Windows Management Instrumentation (WMI) class, in Configuration Manager, that represents the local management point.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_LocalMP  
{  
      String Capabilities;  
      UInt32 Index;  
      String MasterSiteCode;  
      String Name;  
      String Protocol;  
      String SiteCode;  
      UInt32 Version;  
};  
```  

## Methods  
 The `SMS_LocalMP` class does not define any methods.  

## Properties  
 `Capabilities`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Capabilities of the local management point.  

 `Index`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 For local Management Point rotation.  

 `MasterSiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The master site code for the local management point.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The name of the local management point.  

 `Protocol`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The network protocol used for the local management point.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The site code for the site supporting the local management point.  

 `Version`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The version of the local management point.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Client Framework and Data Transfer Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/client-framework-and-data-transfer-client-wmi-classes.md)
