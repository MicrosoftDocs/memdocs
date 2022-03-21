---
title: "SMS_TaskSequenceAppReferencesInfo Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 932e81bd-0533-46ee-9794-8a33ebdfb08d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_TaskSequenceAppReferencesInfo Server WMI Class
The `SMS_TaskSequenceAppReferencesInfo` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a Configuration Manager application in the task sequence.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequenceAppReferencesInfo : SMS_BaseClass  
{  
    String PackageID;  
    SInt32 RefAppCI_ID;  
    String RefAppModelName;  
    String RefAppPackageID;  
};  
```  

## Methods  
 The `SMS_TaskSequenceAppReferencesInfo` class does not define any methods.  

## Properties  
 `PackageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Package ID of the task sequence.  

 `RefAppCI_ID`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 CI_ID of the referenced by task sequence application.  

 `RefAppModelName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The model name of the referenced by task sequence application.  

 `RefAppPackageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Package ID of the referenced by task sequence application.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
