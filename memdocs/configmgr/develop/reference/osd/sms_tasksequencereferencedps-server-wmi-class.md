---
title: SMS_TaskSequenceReferenceDps Class
titleSuffix: Configuration Manager
description: Learn about the simplified syntax, methods, properties, and requirements of the SMS_TaskSequenceReferenceDps server class.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: de43cd2c-26e6-426a-8dd9-4977fcdea31c
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_TaskSequenceReferenceDps Server WMI Class
The `SMS_TaskSequenceReferenceDps` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the package that is available for the task sequence at a specified distribution point.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequenceReferenceDps  
{  
      String Hash;  
      String PackageID;  
      String ServerNALPath;  
      String SiteCode;  
      UInt32 SourceVersion;  
      String TaskSequenceID;  
};  
```  

## Methods  
 The `SMS_TaskSequenceReferenceDps` class does not define any methods.  

## Properties  
 `Hash`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 A hash of package content.  

 `PackageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The ID of the package associated with the task sequence.  

 `ServerNALPath`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The server network abstraction layer (NAL) path to the package at a particular distribution point.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The site code for the distribution point.  

 `SourceVersion`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The version of the package source.  

 `TaskSequenceID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The ID for the task sequence.  

## Remarks  
 Class qualifiers for this class include:  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
