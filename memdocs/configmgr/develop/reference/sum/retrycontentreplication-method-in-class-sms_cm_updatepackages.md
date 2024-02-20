---
title: RetryContentReplication Method
titleSuffix: Configuration Manager
description: The RetryContentReplication Windows Management Instrumentation (WMI) class method triggers DistMgr to copy content from the source to the content library.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: fde34edf-3ba7-4a89-9004-05c793aaa7e2
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# RetryContentReplication Method in Class SMS_CM_UpdatePackages
The `RetryContentReplication` Windows Management Instrumentation (WMI) class method, in Configuration Manager, triggers DistMgr to copy content from the source to the content library.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 RetryContentReplication(  
     UInt32 ForceRetry  
);  

```  

#### Parameters  
 `ForceRetry`  
 Data type: `UInt32`  

 Qualifiers: [in, optional]  

 Flag to force a retry. 1 to force a retry; otherwise 0 or `null`.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_CM_UpdatePackages Server WMI Class](../../../develop/reference/sum/sms_cm_updatepackages-server-wmi-class.md)   
