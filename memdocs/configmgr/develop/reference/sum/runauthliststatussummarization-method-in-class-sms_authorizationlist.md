---
description: Learn how to use Configuration Manager RunAuthListStatusSummarization Windows Management Instrumentation (WMI) class method to update summarized results for a particular update group.
title: RunAuthListStatusSummarization Method
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 7b74264f-bdf5-4cd0-8ebd-a60e5c25ea0e
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# RunAuthListStatusSummarization Method in Class SMS_AuthorizationList
The `RunAuthListStatusSummarization` Windows Management Instrumentation (WMI) class method, in Configuration Manager, updates summarized results for a particular update group.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 RunAuthListStatusSummarization(  
     UInt32 CI_ID  
);  
```  

#### Parameters  
 `CI_ID`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  
 Your application should call this method only if the `EulaExists` property is set to `true` in the configuration item for the software update. This property is defined in the [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_SoftwareUpdate Server WMI Class](../../../develop/reference/sum/sms_softwareupdate-server-wmi-class.md)
