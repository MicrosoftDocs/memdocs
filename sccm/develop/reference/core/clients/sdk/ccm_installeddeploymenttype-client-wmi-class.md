---
title: "CCM_InstalledDeploymentType Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: cae7f7bf-0160-400d-86d8-d3a32933ebbb
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# CCM_InstalledDeploymentType Client WMI Class
The `CCM_InstalledDeploymentType` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents an installed deployment type.   

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class CCM_InstalledDeploymentType :    
{  
    String Id;  
    String Revision;  
};  
```  

## Methods  
 The `CCM_InstalledDeploymentType` class does not define any methods.  

## Properties  
 `Id`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Identifier.    

 `Revision`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Revision.    

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
