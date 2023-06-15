---
title: DeleteByQuery Method
titleSuffix: Configuration Manager
description: In Configuration Manager, the DeleteByQuery WMI class method deletes status messages specified by a WQL query.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 0b96f338-dd8a-449d-a4c0-8177ebbb0bc3
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# DeleteByQuery Method in Class SMS_StatusMessage
The `DeleteByQuery` Windows Management Instrumentation (WMI) class method, in Configuration Manager, deletes status messages specified by a WQL query.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
UInt32 DeleteByQuery(  
      String WQLSelect  
);  
```  

#### Parameters  
 `WQLSelect`  
 Data type: `String`  

 Qualifiers: [in]  

 A WQL SELECT statement.  

## Return Values  
 A `UInt32` data type that indicates the number of rows deleted.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_StatusMessage Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statusmessage-server-wmi-class.md)
