---
title: "SMS_G_SYSTEM_DCMDeploymentCompliantAssetDetails Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 3007dfd9-5611-4126-9cc6-c8d11fb319e7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_G_SYSTEM_DCMDeploymentCompliantAssetDetails Server WMI Class
The `SMS_G_SYSTEM_DCMDeploymentCompliantAssetDetails` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents compliant asset details for a deployment.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_G_SYSTEM_DCMDeploymentCompliantAssetDetails : SMS_G_System  
{  
    UInt32 AssignmentID;  
    UInt32 BL_ID;  
    UInt32 CI_ID;  
    UInt32 ResourceID;  
    UInt32 Rule_ID;  
};  
```  

## Methods  
 The `SMS_G_SYSTEM_DCMDeploymentCompliantAssetDetails` class does not define any methods.  

## Properties  
 `AssignmentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 ID of the configuration item assignment. This ID is unique only for the site.  

 `BL_ID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Baseline ID.  

 `CI_ID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Unique ID of the configuration item. This ID is unique only for the site.  

 `ResourceID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Unique ID, supplied by Configuration Manager, that identifies a client resource. This ID is not unique across sites.  

 `Rule_ID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Description of the rule ID.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
