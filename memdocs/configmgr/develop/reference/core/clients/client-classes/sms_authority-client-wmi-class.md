---
title: "SMS_Authority Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: c51f2209-2382-4005-a960-c87fea65d04c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_Authority Client WMI Class
The `SMS_Authority` class is a client Windows Management Instrumentation (WMI) class, in Configuration Manager, that represents the Configuration Manager site that manages the client.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_Authority : CCM_Authority  
{  
      String Capabilities;  
      String CurrentManagementPoint;  
      UInt32 Index;  
      String Name;  
      UInt32 PolicyOrder;  
      String PolicyRequestTarget;  
      String Protocol;  
      String SigningCertificate;  
      UInt32 Version;  
};  
```  

## Methods  
 The `SMS_Authority` class does not define any methods.  

## Properties  
 `Capabilities`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Reserved.  

 `CurrentManagementPoint`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The current management point for the site.  

 `Index`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 For assigned Management Point rotation.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Name of the authority.  

 `PolicyOrder`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Determines the priority of the authority when resolving policy conflicts. The lower the order, the higher the priority of the authority's policy.  

 `PolicyRequestTarget`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Specifies the target for requesting policy assignments. If this value is NULL, no policy is requested for this authority.  

 `Protocol`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Reserved.  

 `SigningCertificate`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The site signing certificate. This is only relevant in native mode.  

 `Version`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The version of the authority.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Client Framework and Data Transfer Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/client-framework-and-data-transfer-client-wmi-classes.md)
