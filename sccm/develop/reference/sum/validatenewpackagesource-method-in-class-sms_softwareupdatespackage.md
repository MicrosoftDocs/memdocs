---
title: "ValidateNewPackageSource Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 10479561-8533-4c16-9ddb-ef1e2509e352
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# ValidateNewPackageSource Method in Class SMS_SoftwareUpdatesPackage
The `ValidateNewPackageSource` Windows Management Instrumentation (WMI) class method, in Configuration Manager, validates a new package source location for a software update.  

> [!NOTE]
>  All of the updates available in the old package source must be available in the new package source for validation to succeed.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 ValidateNewPackageSource(  
     String PackageSource  
);  
```  

#### Parameters  
 `PackageSource`  
 Data type: `String`  

 Qualifiers: [in]  

 The location of the package content to verify.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  
 This method might be used when changing the package source location of a software update package due to infrastructure changes or a server failure.  

 This method is new in the latest version of Configuration Manager. Note that it is the only way to change the package source for an [SMS_SoftwareUpdate Server WMI Class](../../../develop/reference/sum/sms_softwareupdate-server-wmi-class.md) object. Most other types of packages can be changed in the console, but not the software update package. The access to this package from the console is restricted.  

 To use this method:  

1.  Manually copy the package files from the old source location to the new location.  

2.  In your application, obtain the [SMS_SoftwareUpdatesPackage Server WMI Class](../../../develop/reference/sum/sms_softwareupdatespackage-server-wmi-class.md) object for the software update.  

3.  Include a call to `ValidateNewPackageSource` on the package.  

4.  On successful return from the method, have the application change the `StoredPkgPath` property in the package to indicate the new source location.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_SoftwareUpdatesPackage Server WMI Class](../../../develop/reference/sum/sms_softwareupdatespackage-server-wmi-class.md)   
 [RefreshPkgSource Method in Class SMS_SoftwareUpdatesPackage](../../../develop/reference/sum/refreshpkgsource-method-in-class-sms_softwareupdatespackage.md)   
 [SetSourceSite Method in Class SMS_SoftwareUpdatesPackage](../../../develop/reference/sum/setsourcesite-method-in-class-sms_softwareupdatespackage.md)   
 [Unlock Method in Class SMS_SoftwareUpdatesPackage](../../../develop/reference/sum/unlock-method-in-class-sms_softwareupdatespackage.md)
