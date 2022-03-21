---
title: "SMS_CollectionDependencies Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 88924960-781a-4b8e-800f-6caeb75f1c80
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_CollectionDependencies Server WMI Class
The `SMS_CollectionDependencies` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, is used to query dependency relationships between collections, specifically the composable collection rules (inclusion, exclusion) and the limiting collection.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_CollectionDependencies : SMS_BaseClass  
{  
      String DependentCollectionID;  
      UInt32 RelationshipType;  
      String SourceCollectionID;  
};  
```  

## Methods  
 The `SMS_CollectionDependencies` class does not define any methods.  

## Properties  
 `DependentCollectionID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The unique id of the dependent collection.  

 `RelationshipType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key, enumeration]  

 Dependency relationship, how the dependent collection uses the source.  

| Value | Relationship type |
| ----- | ----------------- |
|1|LIMITING|  
|2|INCLUDE|  
|3|EXCLUDE|  

 `SourceCollectionID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The unique id of the source collection.  

## Remarks  
 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
