---
title: SMS_ClientBaseline Class
titleSuffix: Configuration Manager
description: In Configuration Manager, the SMS_ClientBaseline WMI class is an SMS Provider server class that represents a client deployment baseline.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 524d8fd8-d226-4cb3-85d5-91ecfc45eef7
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_ClientBaseline Server WMI Class
The `SMS_ClientBaseline` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a client deployment baseline.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ClientBaseline: SMS_BaseClass  
{  
    UInt32 BaselineID;  
    String BaselineName;  
    UInt32 BaselineType;  
    String ClientVersion;      
    DateTime LastUpdatedTime;  
    String SourceHash;      
};  

```  

## Methods  
 The `SMS_ClientBaseline` class does not define any methods.  

## Properties  
 `BaselineID`  
 Data type: `uint32`  

 Access type: Read  

 Qualifiers: [key]  

 The client baseline ID.  

 `BaselineName`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The friendly name of the client baseline.  

 `BaselineType`  
 Data type: `uint32`  

 Access type: Read  

 Qualifiers: none  

 The client baseline type. Possible values are:  

|Value|Client baseline type|  
|-|-|  
|1|Production|  
|2|Staging|  

 `ClientVersion`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The client baseline version.  

 `LastUpdatedTime`  
 Data type: `DateTime`  

 Access type: Read  

 Qualifiers: none  

 The last time the client baseline was modified.  

 `SourceHash`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The client baseline source hash.  

## Remarks  
 Class qualifiers for this class include:  

- Dynamic  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
