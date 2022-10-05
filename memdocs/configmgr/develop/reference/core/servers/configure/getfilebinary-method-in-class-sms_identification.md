---
description: Learn how to use the GetFileBinary Method to get the binary user interface for a feature.
title: GetFileBinary Method
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 0d7b1097-d386-48aa-8fc4-ff0e4c5d7dc3
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# GetFileBinary Method in Class SMS_Identification
The `GetFileBinary` Windows Management Instrumentation (WMI) class method, in Configuration Manager, gets the binary user interface for a feature. The binary can be separated into multiple blocks starting with number 1. If `isTheLastBlock` equals `False`, then you need call the method again with blockNumber+1 to get the next block.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 GetFileBinary (  
    String FileName,   
    UInt32 blockNumber,   
    String binary64Encoded,   
    Boolean isTheLastBlock  
);  

```  

#### Parameters  
 `FileName`  
 Data type: `String`  

 Qualifiers: [in]  

 The name of the file.  

 `blockNumber`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 The block number. To get the next block, call the method again with blockNumber+1, as long as isTheLastBlock equals `False`.  

 `binary64Encoded`  
 Data type: `String`  

 Qualifiers: [out]  

 The binary 64-encoded file.  

 `isTheLastBlock`  
 Data type: `Boolean`  

 Qualifiers: [out]  

 `True` if the current block is the last block; otherwise, `False`. While `False`, you can get the next block by calling the method again with blockNumber+1.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Identification Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_identification-server-wmi-class.md)
