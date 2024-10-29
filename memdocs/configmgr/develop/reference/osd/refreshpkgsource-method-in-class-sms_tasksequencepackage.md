---
title: RefreshPkgSource Method in SMS_TaskSequencePackage
titleSuffix: Configuration Manager
description: The RefreshPkgSource class method refreshes the package source at all distribution points when the package properties haven't changed.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 24d3514f-b1b7-4ac3-b1ac-17548aa3f273
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# RefreshPkgSource Method in Class SMS_TaskSequencePackage
The `RefreshPkgSource` class method, in Configuration Manager, refreshes the package source at all distribution points when the package properties haven't changed.  

> [!CAUTION]
>  This method supports the Configuration Manager infrastructure and renders your task sequence inoperable if it is called.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 RefreshPkgSource();  
```  

#### Parameters  
 None.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or nonzero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  
 Using this method is the only way to force an update of the source files, other than by creating a `RefreshSchedule` value for the package. For information about the `RefreshSchedule` property, see [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_TaskSequencePackage Server WMI Class](../../../develop/reference/osd/sms_tasksequencepackage-server-wmi-class.md)   
 [SetSourceSite Method in Class SMS_TaskSequencePackage](../../../develop/reference/osd/setsourcesite-method-in-class-sms_tasksequencepackage.md)
