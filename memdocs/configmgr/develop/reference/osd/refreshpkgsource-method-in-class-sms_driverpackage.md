---
title: "RefreshPkgSource Method in SMS_DriverPackage"
description: The RefreshPkgSource Windows Management Instrumentation (WMI) class method, in Configuration Manager, refreshes the package source at all distribution points.
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 96826b76-5ac5-45c8-9328-f04536667bb6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# RefreshPkgSource Method in Class SMS_DriverPackage
The `RefreshPkgSource` Windows Management Instrumentation (WMI) class method, in Configuration Manager, refreshes the package source at all distribution points.  

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
 This method copies the latest version of the package to all the distribution points of the package. The source version of the package is incremented, and the package content is replicated to child sites.  

 Using this method is the only way to force an update of the source files, other than by creating a RefreshSchedule value for the package. For information about the RefreshSchedule property, see [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 For more information about using this method, see [How to Create a Driver Package for a Windows Driver in Configuration Manager](../../../develop/osd/how-to-create-a-driver-package-for-a-windows-driver.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_DriverPackage Server WMI Class](../../../develop/reference/osd/sms_driverpackage-server-wmi-class.md)   
 [AddDriverContent Method in Class SMS_DriverPackage](../../../develop/reference/osd/adddrivercontent-method-in-class-sms_driverpackage.md)   
 [RemoveDriverContent Method in Class SMS_DriverPackage](../../../develop/reference/osd/removedrivercontent-method-in-class-sms_driverpackage.md)   
 [ValidateNewPackageSource Method in Class SMS_DriverPackage](../../../develop/reference/osd/validatenewpackagesource-method-in-class-sms_driverpackage.md)
