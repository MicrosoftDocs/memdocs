---
title: "Unlock Method in SMS_SoftwareUpdatesPackage"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: beace883-5c9b-46ef-bf6f-9447efeb75f9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# Unlock Method in Class SMS_SoftwareUpdatesPackage
The `Unlock` Windows Management Instrumentation (WMI) class method, in Configuration Manager, sets the source site to the current site, unlocking the software updates package.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 Unlock();  
```  

#### Parameters  
 None.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_SoftwareUpdatesPackage Server WMI Class](../../../develop/reference/sum/sms_softwareupdatespackage-server-wmi-class.md)   
 [RefreshPkgSource Method in Class SMS_SoftwareUpdatesPackage](../../../develop/reference/sum/refreshpkgsource-method-in-class-sms_softwareupdatespackage.md)   
 [SetSourceSite Method in Class SMS_SoftwareUpdatesPackage](../../../develop/reference/sum/setsourcesite-method-in-class-sms_softwareupdatespackage.md)   
 [ValidateNewPackageSource Method in Class SMS_SoftwareUpdatesPackage](../../../develop/reference/sum/validatenewpackagesource-method-in-class-sms_softwareupdatespackage.md)
