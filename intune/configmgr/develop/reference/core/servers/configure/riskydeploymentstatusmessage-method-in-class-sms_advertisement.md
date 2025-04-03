---
description: Learn how to use the RiskyDeploymentStatusMessage method to send a warning status message about a user deployment to a risky collection.
title: RiskyDeploymentStatusMessage Method
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: cf2b7ba4-e61c-4c13-ac69-376f94a7e698
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# RiskyDeploymentStatusMessage Method in Class SMS_Advertisement
The `RiskyDeploymentStatusMessage` Windows Management Instrumentation (WMI) class method, in Configuration Manager, sends a warning status message about a user deployment to a risky collection.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 RiskyDeploymentStatusMessage (  
    String DeploymentID,  
    String DeploymentName,  
    String PackageID,  
    String CollectionID  
);  

```  

#### Parameters  
 `DeploymentID`  
 Data type: `String`  

 Qualifiers: [in]  

 Deployment ID.  

 `DeploymentName`  
 Data type: `String`  

 Qualifiers: [in]  

 Name of the deployment.  

 `PackageID`  
 Data type: `String`  

 Qualifiers: [in]  

 Package ID of the deployment.  

 `CollectionID`  
 Data type: `String`  

 Qualifiers: [in]  

 Collection ID of the deployment.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Advertisement Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_advertisement-server-wmi-class.md)   
