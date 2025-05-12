---
title: GetClientsCountByCollections Method
titleSuffix: Configuration Manager
description: A Windows Management Instrumentation class method that retrieves the number of clients in the specified collections.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 1c44e69e-4a53-4f63-bd6a-441f15a0d97b
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# GetClientsCountByCollections Method in Class SMS_MigrationCollectionInfo
The `GetClientsCountByCollections` Windows Management Instrumentation (WMI) class method, in Configuration Manager, retrieves the number of clients in the specified collections.  

> [!NOTE]
>  This method is reserved for future use.  

 The following syntax is simplified from Managed Object Format (MOF) code and is intended to show the definition of the method.  

## Syntax  

```  
SInt32 GetClientsCountByCollections(  
     String collectionIDs[],  
     UInt32 clientsCount  
);  
```  

#### Parameters  
 `collectionIDs`  
 Data type: `String` array  

 Qualifiers: [in]  

 The specified collection IDs.  

 `clientsCount`  
 Data type: `UInt32`  

 Qualifiers: `[out]`  

 The number of clients in the collections.  

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../develop/core/reqs/server-development-requirements.md).  

## See also

[SMS_MigrationCollectionInfo Server WMI Class](../../../../develop/reference/core/migration/sms_migrationcollectioninfo-server-wmi-class.md)
