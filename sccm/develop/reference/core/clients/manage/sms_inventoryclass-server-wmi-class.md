---
title: "SMS_InventoryClass Class"
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
ms.assetid: 404d435c-8f01-46f1-9341-e3db6f0971f0searchScope: - ConfigMgr SDK
caps.latest.revision: 4
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_InventoryClass Server WMI Class
The `SMS_InventoryClass` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents inventory classes that exist in the system.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_InventoryClass :    
{  
    String ClassName;  
    Boolean IsDeletable;  
    String Namespace;  
    InventoryClassProperty Properties[];  
    String SMSClassID;  
    String SMSContext;  
    String SMSDeviceUri;  
    String SMSGroupName;  
};  
```  

## Methods  
 The following table lists the methods in the `SMS_InventoryClass` class.  

|Method|Description|  
|------------|-----------------|  
|GetInventoryClassesFromMof Method in Class SMS_InventoryClass|For internal use only.|  

## Properties  
 `ClassName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 The WMI name of the inventory class.  

 `IsDeletable`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 For internal use only.  

 `Namespace`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 The WMI namespace.  

 `Properties`  
 Data type: `Object Array`  

 Access type: Read/Write  

 Qualifiers: none  

 The properties of this class.  

 `SMSClassID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The Class ID that will be used to generate the database table, view and the UI SDK class.  

 `SMSContext`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 SMS contexts in XML format. This can support multiple contexts.  

 `SMSDeviceUri`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 SMS device URI in XML format. This could support multiple device URIs.  

 `SMSGroupName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 The default class name displayed in the MOF editor and Resource Explorer, if no localized resources are provided.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
