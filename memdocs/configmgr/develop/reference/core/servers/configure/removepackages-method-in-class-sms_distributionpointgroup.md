---
title: "RemovePackages Method"
titleSuffix: "Configuration Manager"
description: "In Configuration Manager, the RemovePackages WMI class method removes a set of packages from this distribution point group."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 03006525-fa62-4259-b9e3-0382159d61f7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# RemovePackages Method in Class SMS_DistributionPointGroup
The `RemovePackages` Windows Management Instrumentation (WMI) class method, in Configuration Manager, removes a set of packages from this distribution point group.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 RemovePackages(  
     string PackageIDs[],  
     boolean RemoveTargetedPackages  
);  
```  

#### Parameters  
 `PackageIDs`  
 Data type: `String` Array  

 Qualifiers: `[in]`  

 A unique, auto-generated key that is used to relate programs, advertisements, and distribution points to the package.  

 `RemovePackageFromDPs`  
 Data type: `Boolean`  

 Qualifiers: `[in, optional]`  

 `true`, if the packages should be removed from the distribution points.  The default value is `true`.  

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Application Server WMI Class](../../../../../develop/reference/apps/sms_application-server-wmi-class.md)   
