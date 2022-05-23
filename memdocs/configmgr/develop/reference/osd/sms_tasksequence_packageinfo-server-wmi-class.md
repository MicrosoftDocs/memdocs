---
title: "SMS_TaskSequence_PackageInfo Class"
titleSuffix: "Configuration Manager"
description: "SMS_TaskSequence_PackageInfo WMI is an SMS provider server class that represents information about an operating system deployment task sequence."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 32df68b1-836a-4e85-a52c-c2a7574113c0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_TaskSequence_PackageInfo Server WMI Class
The `SMS_TaskSequence_PackageInfo` Windows Management Instrumentation (WMI) class is an SMS provider server class, in Configuration Manager, that represents information about an operating system deployment task sequence.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_PackageInfo   
{  
    String Name;  
    String PackageId;  
    UInt32 PkgType;  
    UInt32 Size;  
};  

```  

## Methods  
 The `SMS_TaskSequence_PackageInfo` class does not define any methods.  

## Properties  
 `Name`  
 Data type:  `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The name of the package.  

 `PackageId`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The ID of the package.  

 `PkgType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The package type.  

 `Size`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The size of the package, in kilobytes.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
