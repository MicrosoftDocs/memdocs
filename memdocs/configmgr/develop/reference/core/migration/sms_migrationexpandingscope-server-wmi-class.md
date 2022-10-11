---
title: SMS_MigrationExpandingScope Class
titleSuffix: Configuration Manager
description: The SMS_MigrationExpandingScope class represents collections that have the expanding scope problem when migrated to System Center 2012 Configuration Manager.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: f80595c2-73e9-4869-8e13-ab711783f9d9
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_MigrationExpandingScope Server WMI Class
The `SMS_MigrationExpandingScope` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the collections that have the problem of expanding scope when migrated to System Center 2012 Configuration Manager.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_MigrationExpandingScope : SMS_BaseClass  
{  
    UInt32 CollectionEntityID;  
    String CollectionEntityName;  
    String CollectionWMIObjectPath;  
    UInt32 TargetingEntityID;  
    String TargetingEntityName;  
    String TargetingWMIObjectPath;  
};  
```  

## Methods  
 The `SMS_MigrationExpandingScope` class does not define any methods.  

## Properties  
 `CollectionEntityID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key]  

 Unique identifier for the collection.  

 `CollectionEntityName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: none  

 The collection entity display name.  

 `CollectionWMIObjectPath`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: none  

 The collection entity WMI path.  

 `TargetingEntityID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key]  

 Unique identifier for the targeting entity.  

 `TargetingEntityName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: none  

 The targeting entity display name.  

 `TargetingWMIObjectPath`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: none  

 The targeting entity WMI path.  

## Remarks  
 When you create a migration job, consider whether to specify a new limit to the collection to restrict the scope for each of such collections.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../develop/core/reqs/server-development-requirements.md).
