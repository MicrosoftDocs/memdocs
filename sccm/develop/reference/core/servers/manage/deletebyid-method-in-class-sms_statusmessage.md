---
title: "DeleteByID Method"
titleSuffix: "Configuration Manager"
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
ms.assetid: 70a288b1-8a61-4820-935c-a9fd89370b26searchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
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
