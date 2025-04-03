---
title: UpdateClassicDeployment Method
titleSuffix: Configuration Manager
description: The UpdateClassicDeployment Windows Management Instrumentation (WMI) class method, in Configuration Manager, updates the summarized results for a specific Classic Deployment.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: f3c70bc6-229c-4c03-b1a1-ad11ee8e5d62
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# UpdateClassicDeployment Method in Class SMS_DeploymentSummary
The `UpdateClassicDeployment` Windows Management Instrumentation (WMI) class method, in Configuration Manager, updates the summarized results for a specific Classic Deployment.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 UpdateClassicDeployment (  
     string OfferID   
);  
```  

#### Parameters  
 `OfferID`  
 Data type: `String`  

 Qualifiers: [in]  

 Advertisement identifier.  

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_DeploymentSummary Server WMI Class](../../../develop/reference/apps/sms_deploymentsummary-server-wmi-class.md)   
