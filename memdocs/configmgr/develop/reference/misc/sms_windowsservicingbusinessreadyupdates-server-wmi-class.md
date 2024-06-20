---
title: SMS_WindowsServicingBusinessReadyUpdates Class
titleSuffix: Configuration Manager
description: An internal-only Windows Management Instrumentation class method.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 94ec78e1-bef9-4a49-b6e8-0b615589de5b
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# SMS_WindowsServicingBusinessReadyUpdates Server WMI Class
For internal use only.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_WindowsServicingBusinessReadyUpdates : SMS_BaseClass  
{  
     String UpdateID;  
};  

```  

## Methods  
 The  `SMS_WindowsServicingBusinessReadyUpdates` class does not define any methods.  

## Properties  
 `UpdateID`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key, not_null]  

 Reserved for internal use.  

## Remarks  
 Class qualifiers for this class include:  

- Dynamic  

- Read (read-only)  

- Secured  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
