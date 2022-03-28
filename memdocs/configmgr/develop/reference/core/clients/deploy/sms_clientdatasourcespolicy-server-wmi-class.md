---
description: Learn how to represent client policy data sources in Configuration Manager using SMS_ClientDataSourcesPolicy class.
title: "SMS_ClientDataSourcesPolicy Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 55bd888c-93b7-49b8-98af-273953a5fa37
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_ClientDataSourcesPolicy Server WMI Class
The  `SMS_ClientDataSourcesPolicy` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents client policy data sources.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ClientDataSourcesPolicy : SMS_BaseClass  
{  
    UInt64 BranchCacheBytes;  
    UInt64 ManagementPointBytes;  
};  

```  

## Methods  
 The  `SMS_ClientDataSourcesPolicy`  class does not define any methods.  

## Properties  
 `BranchCacheBytes`  
 Data type: `UInt64`  

 Access type: Read  

 Qualifiers: none  

 The number of bytes from the branch cache.  

 `ManagementPointBytes`  
 Data type: `UInt64`  

 Access type: Read  

 Qualifiers: none  

 The number of bytes from management points.  

## Remarks  
 Class qualifiers for this class include:  

- Dynamic  

- Read (read-only)  

- Singleton  

- Secured  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
