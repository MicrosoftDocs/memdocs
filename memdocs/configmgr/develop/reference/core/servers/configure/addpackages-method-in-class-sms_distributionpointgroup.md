---
title: "AddPackages Method"
titleSuffix: "Configuration Manager"
description: "A Windows Management Instrumentation class method that assigns a set of packages to the distribution point group."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: d9ef0822-0931-4459-b121-49d953b0a233
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# AddPackages Method in Class SMS_DistributionPointGroup
The `AddPackages` Windows Management Instrumentation (WMI) class method, in Configuration Manager, assigns a set of packages to the distribution point group.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 AddPackages(  
     string PackageIDs[]  
);  
```  

#### Parameters  
 `PackageIDs`  
 Data type: `String` Array  

 Qualifiers: `[in]`  

 A unique, auto-generated key that is used to relate programs, advertisements, and distribution points to the package.  

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
