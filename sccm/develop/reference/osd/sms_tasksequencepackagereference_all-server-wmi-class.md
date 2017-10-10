---
title: "SMS_TaskSequencePackageReference_All Class"
titleSuffix: "Configuration Manager"
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
ms.assetid: 247f1a76-062d-42b1-aa82-bad9763a0a1bsearchScope: - ConfigMgr SDK
caps.latest.revision: 4
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_TaskSequencePackageReference_All Server WMI Class
The `SMS_TaskSequencePackageReference_All` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that allows the retrieval of all task sequence package or application references (including those that do not contain any content files).  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequencePackageReference_All : SMS_BaseClass  
{  
    String ObjectID;  
    String PackageID;  
    String RefPackageID;  
};  
```  

## Methods  
 The `SMS_TaskSequencePackageReference_All` class does not define any methods.  

## Properties  
 `ObjectID`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key]  

 If the Task Sequence reference is to a legacy package, this property is the package identifier of the legacy package. If the Task Sequence reference is to an application, this property is the package identifier of the application.  

 `PackageID`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key]  

 Package identifier of the task sequence for which the user requests package or application references.  

 `RefPackageID`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 If the Task Sequence reference is to a legacy package, this property is the package identifier of the legacy package. If the Task Sequence reference is to an application, this property is the package identifier of the application.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
