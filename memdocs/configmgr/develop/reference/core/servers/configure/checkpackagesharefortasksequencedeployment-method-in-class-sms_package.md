---
description: Learn how to use the Configuration Manager with the CheckPackageShareForTaskSequenceDeployment Windows Management Instrumentation (WMI) class method to verify that the package share type meets the requirements of a task sequence deployment.
title: CheckPackageShareForTaskSequenceDeployment Method
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 94d247a9-c862-433d-84b5-d19d7ca39a0e
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# CheckPackageShareForTaskSequenceDeployment Method in Class SMS_Package
The `CheckPackageShareForTaskSequenceDeployment` Windows Management Instrumentation (WMI) class method in Configuration Manager that checks whether the package share type meets the requirements of a task sequence deployment.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
uint32 CheckPackageShareForTaskSequenceDeployment   
{  
    [IN]    String PackageID  
    [OUT]   Boolean IsValid  
    [OUT]   String InvalidTaskSequenceDeploymentIDs[]  
    [OUT]   String InvalidTaskSequenceDeploymentNames[]  
};  
```  

## Parameters  
 `PackageID`  
 Data type: `String`  

 Qualifiers: [id("0"), in]  

 Package identifier.  

 `IsValid`  
 Data type: `Boolean`  

 Qualifiers: [id("1"), out]  

 `true` if the package is valid for task sequence use. `false` if the package is invalid for task sequence use. If the package is referred to by a run-from-net deployment, the package must be available as a share on a distribution point.  

 `InvalidTaskSequenceDeploymentIDs`  
 Data type: `String` Array  

 Qualifiers: [id("2"), out]  

 Identifiers of task sequence deployments that are invalid because this package isn't valid for task sequence use.  

 `InvalidTaskSequenceDeploymentNames`  
 Data type: `String Array`  

 Qualifiers: [id("3"), out]  

 Names of task sequence deployments that are invalid because this package isn't valid for task sequence use.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
