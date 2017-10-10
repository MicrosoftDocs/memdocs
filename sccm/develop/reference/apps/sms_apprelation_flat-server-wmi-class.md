---
title: "SMS_AppRelation_Flat Class"
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
ms.assetid: b6f86f0b-6593-4f58-8e6b-3934529408cdsearchScope: - ConfigMgr SDK
caps.latest.revision: 17
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_AppRelation_Flat Server WMI Class
The `SMS_AppRelation_Flat` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the flattened application relation. This includes direct and indirect relations.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_AppRelation_Flat : SMS_BaseClass  
{  
    UInt32 FromApplicationCIID;  
    UInt32 FromDeploymentTypeCIID;  
    UInt32 Level;  
    UInt32 RelationType;  
    UInt32 ToApplicationCIID;  
    UInt32 ToDeploymentTypeCIID;  
};  
```  

## Methods  
 The `SMS_AppRelation_Flat` class does not define any methods.  

## Properties  
 `FromApplicationCIID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 From-application configuration item identifier.  

 `FromDeploymentTypeCIID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 From-deployment type identifier.  

 `Level`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Level between the from-deployment type and the to-deployment type.  

 `RelationType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Type of relationship between configuration items. Possible values are:  

|||  
|-|-|  
|1|Bundled|  
|2|Required|  
|3|Prohibited|  
|4|Optional|  
|5|Derived|  
|6|Superseded|  

 `ToApplicationCIID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 To-application configuration item identifier.  

 `ToDeploymentTypeCIID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 To-deployment type configuration item identifier.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Application Management Server WMI Classes](../../../develop/reference/apps/application-management-server-wmi-classes.md)
