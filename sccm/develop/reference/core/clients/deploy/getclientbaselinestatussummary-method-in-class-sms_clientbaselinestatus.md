---
title: "GetClientBaselineStatusSummary Method"
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
ms.assetid: ff58c3a0-203e-476b-b803-e449444f4fb1searchScope: - ConfigMgr SDK
caps.latest.revision: 4
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# GetClientBaselineStatusSummary Method in Class SMS_ClientBaselineStatus
The `GetClientBaselineStatusSummary` Windows Management Instrumentation (WMI) class method, in Configuration Manager, gets baseline status summary information by `BaselineType` and `CollectionID`.  

## Syntax  

```  
sint32 GetClientBaselineStatusSummary(  
     UInt32 BaselineType,                  
     String CollectionID,                     
     UInt32 Total,                        
     UInt32 Compliant,                       
     UInt32 InProgress,                        
     UInt32 NotCompliant,                       
     UInt32 CriticalError  
);  

```  

#### Parameters  
 `BaselineType`  
 Data type: `uint32`  

 Qualifiers: [in]  

 The client baseline type. Possible values are:  

|||  
|-|-|  
|1|Production|  
|2|Staging|  

 `CollectionID`  
 Data type: `String`  

 Qualifiers: [in]  

 The collection for which you want to get the baseline status summary.  

 `Total`  
 Data type: `uint32`  

 Qualifiers: [out]  

 The total number of clients in the specified collection.  

 `Compliant`  
 Data type: `uint32`  

 Qualifiers: [out]  

 The number of clients in the specified collection that are compliant with the baseline.  

 `InProgress`  
 Data type: `uint32`  

 Qualifiers: [out]  

 The number of clients in the specified collection for which setup is in progress.  

 `NotCompliant`  
 Data type: `uint32`  

 Qualifiers: [out]  

 The number of clients in the specified collection that are not compliant.  

 `CriticalError`  
 Data type: `uint32`  

 Qualifiers: [out]  

 The number of clients in the specified collection that have a critical error.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_ClientBaselineStatus Server WMI Class](../../../../../develop/reference/core/clients/deploy/sms_clientbaselinestatus-server-wmi-class.md)   
 [Configuration Manager Client Deployment Server WMI Classes](../../../../../develop/reference/core/clients/deploy/client-deployment-server-wmi-classes.md)
