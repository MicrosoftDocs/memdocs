---
title: "SMS_WinPEOptionalComponentInBootImage Class"
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
ms.assetid: d05848fb-79ea-463d-a7d7-d9d531b0d7a2searchScope: - ConfigMgr SDK
caps.latest.revision: 4
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_WinPEOptionalComponentInBootImage Server WMI Class
The `SMS_WinPEOptionalComponentInBootImage` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the association between a boot image package and a WinPE optional component.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_WinPEOptionalComponentInBootImage : SMS_BaseClass  
{  
    String Architecture;  
    UInt32 ComponentID;  
    String DependentComponentNames[];  
    UInt32 DependentIds[];  
    Boolean IsRequired;  
    String Name;  
    String PackageID;  
    UInt64 Size;  
};  
```  

## Methods  
 The `SMS_WinPEOptionalComponentInBootImage` class does not define any methods.  

## Properties  
 `Architecture`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key]  

 The architecture of WinPE optional component associated with the SMS_WinPEOptionalComponentInfo object.  

 `ComponentID`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: [key]  

 The unique identifier of the WinPE optional component associated with the SMS_WinPEOptionalComponentInfo object.  

 `DependentComponentNames`  
 Data type: `String` Array  

 Access type: Read  

 Qualifiers: none  

 The name of dependent WinPE optional components associated with the SMS_WinPEOptionalComponentInfo object.  

 `DependentIds`  
 Data type: `UInt32` Array  

 Access type: Read  

 Qualifiers: none  

 The unique identifier of dependent WinPE optional component associated with the SMS_WinPEOptionalComponentInfo object.  

 `IsRequired`  
 Data type: `Boolean`  

 Access type: Read  

 Qualifiers: none  

 The required flag of WinPE optional component associated with the SMS_WinPEOptionalComponentInfo object.  

 `Name`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The name of WinPE optional component associated with the SMS_WinPEOptionalComponentInfo object.  

 `PackageID`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key]  

 The unique identifier of the boot image associated with the SMS_BootImagePackage object.  

 `Size`  
 Data type: `UInt64`  

 Access type: Read  

 Qualifiers: none  

 The size of WinPE optional component associated with the SMS_WinPEOptionalComponentInfo object.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
