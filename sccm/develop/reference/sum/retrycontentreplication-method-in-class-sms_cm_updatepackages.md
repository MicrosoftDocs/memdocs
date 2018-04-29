---
title: "RetryContentReplication Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: fde34edf-3ba7-4a89-9004-05c793aaa7e2
author: aczechowski
ms.author: aaroncz
manager: dougeby
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

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_CM_UpdatePackages Server WMI Class](../../../develop/reference/sum/sms_cm_updatepackages-server-wmi-class.md)   
 [Configuration Manager Software Updates Server WMI Classes](../../../develop/reference/sum/software-updates-server-wmi-classes.md)
