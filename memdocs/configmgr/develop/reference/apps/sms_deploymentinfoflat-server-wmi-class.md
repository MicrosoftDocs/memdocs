---
title: "SMS_DeploymentInfoFlat Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 5bcdc5a5-1989-4c84-9df3-bdeb0c275eee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_DeploymentInfoFlat Server WMI Class
The `SMS_DeploymentInfoFlat` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents all kinds of flattened deployment relations (includes dependence and supersedence).  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DeploymentInfoFlat : SMS_BaseClass  
{  
    String CollectionID;  
    String CollectionName;  
    String DeploymentID;  
    String DeploymentName;  
    UInt32 DeploymentTypeID;  
    String TargetName;  
    UInt32 TargetSecurityTypeID;  
    String TargetSubName;  
};  
```  

## Methods  
 The `SMS_DeploymentInfoFlat` class does not define any methods.  

## Properties  
 `CollectionID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Existing collection to which the advertisement is targeted.  

 `CollectionName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Name of the collection to which the advertisement is advertising.  

 `DeploymentID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Unique auto-generated key.  

 `DeploymentName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Plain text name of the deployment (advertisement/assignment).  

 `DeploymentTypeID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [enumeration, key]  

 Deployment type identifier.  

 `TargetName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Package name, if the target is a package. Application name, if it is application. Update name, if it is update.  

 `TargetSecurityTypeID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Security type identifier of the object type. For example, if the object is a package, it is `2`.  

 `TargetSubName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Program name if it is package, otherwise leave this value empty.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
