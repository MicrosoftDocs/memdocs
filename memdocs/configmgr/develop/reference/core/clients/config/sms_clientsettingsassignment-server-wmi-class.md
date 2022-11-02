---
title: SMS_ClientSettingsAssignment Class
titleSuffix: Configuration Manager
description: The SMS_ClientSettingsAssignment WMI class is an SMS Provider server class, in Configuration Manager, that represents the collection assignments of specified SMS_ClientSettings.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: df1f7e55-033c-4644-b1cb-dc395d859345
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_ClientSettingsAssignment Server WMI Class
The `SMS_ClientSettingsAssignment` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the collection assignments of specified SMS_ClientSettings.   

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ClientSettingsAssignment : SMS_BaseClass  
{  
    UInt32 ClientSettingsID;  
    String CollectionID;  
    String CollectionName;  
    DateTime CreationTime;  
    String UniqueID;  
};  
```  

## Methods  
 The `SMS_ClientSettingsAssignment` class does not define any methods.  

## Properties  
 `ClientSettingsID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Identifies the client agent component. The Client Settings Agent ID is 1.  

 `CollectionID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The ID for the collection associated with the client settings assignment.  

 `CollectionName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [notnull, read]  

 The name of the collection associated with the client settings assignment.  

 `CreationTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [notnull, read]  

 The date and time when the client settings assignment is created.  

 `UniqueID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [notnull, read]  

 The GUID of the client settings assignment.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
