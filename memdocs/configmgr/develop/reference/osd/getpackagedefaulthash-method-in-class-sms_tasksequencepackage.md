---
title: GetPackageDefaultHash Method
titleSuffix: Configuration Manager
description: The `GetPackageDefaultHash` Windows Management Instrumentation (WMI) class method, in Configuration Manager, gets the hash of a Configuration Manager package.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 157c52c0-4c83-415a-9f21-91807b5fd0cc
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# GetPackageDefaultHash Method in Class SMS_TaskSequencePackage
The `GetPackageDefaultHash` Windows Management Instrumentation (WMI) class method, in Configuration Manager, gets the hash of a Configuration Manager package.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 GetPackageDefaultHash(  
      String PackageID,  
      UInt32 SourceVersion,  
      String Hash,  
);  
```  

#### Parameters  
 `PackageID`  
 Data type: `String`  

 Qualifiers: [in]  

 ID of the task sequence package.  

 `SourceVersion`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 The version of the package available at the site. This version is indicated by the `SourceVersion` property of [SMS_TaskSequencePackage Server WMI Class](../../../develop/reference/osd/sms_tasksequencepackage-server-wmi-class.md).  

 `Hash`  
 Data type: `String`  

 Qualifiers: [out]  

 The hash for the package content.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_TaskSequencePackage Server WMI Class](../../../develop/reference/osd/sms_tasksequencepackage-server-wmi-class.md)
