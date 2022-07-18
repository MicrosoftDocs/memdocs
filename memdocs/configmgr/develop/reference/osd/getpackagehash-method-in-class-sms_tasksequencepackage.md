---
description: Learn how to get the hash of a Configuration Manager package using GetPackageHash class method in Configuration Manager.
title: "GetPackageHash Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 12f67c04-b89e-4f12-b560-f08908a8d68c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# GetPackageHash Method in Class SMS_TaskSequencePackage
The `GetPackageHash` Windows Management Instrumentation (WMI) class method, in Configuration Manager, gets the hash of a Configuration Manager package.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 GetPackageHash(  
      String PackageID,  
      UInt32 SourceVersion,  
      String Hash,  
      UInt32 HashVersion  
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

 `HashVersion`  
 Data type: `UInt32`  

 Qualifiers: [out]  

 The type of the requested hash which can be one of the following values.  

 1 - MD5 hash  

 2 - SHA-1 hash  

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
