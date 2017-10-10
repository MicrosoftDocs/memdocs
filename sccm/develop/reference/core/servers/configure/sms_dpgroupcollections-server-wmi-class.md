---
title: "SMS_DPGroupCollections Class"
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
ms.assetid: 0ed27133-baea-4d59-a18f-1a6f503b8599searchScope: - ConfigMgr SDK
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_DPGroupCollections Server WMI Class
The `SMS_DPGroupCollections` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that describes collection association for a given distribution point group.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DPGroupCollections : SMS_BaseClass  
{  
    String CollectionDescription;  
    String CollectionID;  
    UInt32 CollectionMemberCount;  
    String CollectionName;  
    String GroupDescription;  
    String GroupID;  
    String GroupName;  
};  
```  

## Methods  
 The `SMS_DPGroupCollections` class does not define any methods.  

## Properties  
 `CollectionDescription`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Description of the collection.  

 `CollectionID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Collection associated with the distribution point group.  

 `CollectionMemberCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of the collection members.  

 `CollectionName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Name of the collection.  

 `GroupDescription`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Description of the distribution point group.  

 `GroupID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Identifier for the distribution point group.  

 `GroupName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Name of the distribution point group.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Content Server WMI Classes](../../../../../develop/reference/core/servers/configure/content-server-wmi-classes.md)
