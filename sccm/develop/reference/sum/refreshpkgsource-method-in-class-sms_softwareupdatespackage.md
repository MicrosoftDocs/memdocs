---
title: "RefreshPkgSource Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 136541e4-0d5a-458d-89a3-f3dea24d6e5f
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# RefreshPkgSource Method in Class SMS_SoftwareUpdatesPackage
The `RefreshPkgSource` Windows Management Instrumentation (WMI) class method, in Configuration Manager, refreshes the package source at all distribution points. The latest version of the package is copied to all the distribution points of the package. The source version of the package is incremented, and the package content is replicated to child sites.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 RefreshPkgSource();  
```  

#### Parameters  
 None.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  
 Using this method is the only way to force an update of the source files, other than by creating a `RefreshSchedule` value for the package. For information about the `RefreshSchedule` property, see [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_SoftwareUpdatesPackage Server WMI Class](../../../develop/reference/sum/sms_softwareupdatespackage-server-wmi-class.md)   
 [SetSourceSite Method in Class SMS_SoftwareUpdatesPackage](../../../develop/reference/sum/setsourcesite-method-in-class-sms_softwareupdatespackage.md)   
 [ValidateNewPackageSource Method in Class SMS_SoftwareUpdatesPackage](../../../develop/reference/sum/validatenewpackagesource-method-in-class-sms_softwareupdatespackage.md)   
 [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md)
