---
title: DeleteByID Method
description: Learn how the DeleteByID Windows Management Instrumentation (WMI) class method deletes a group of up to 256 status messages.
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 70a288b1-8a61-4820-935c-a9fd89370b26
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# DeleteByID Method in Class SMS_StatusMessage
The `DeleteByID` Windows Management Instrumentation (WMI) class method, in Configuration Manager, deletes a group of up to 256 status messages.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
UInt32 DeleteByID(  
   SInt64 RecordIDs[]  
);  
```  

#### Parameters  
 `RecordIDs`  
 Data type: `SInt64` Array  

 Qualifiers: [in, Max(256)]  

 IDs for the records of the status messages to delete.  

## Return Values  
 A `UInt32` data type that indicates the number of rows deleted.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_StatusMessage Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statusmessage-server-wmi-class.md)
