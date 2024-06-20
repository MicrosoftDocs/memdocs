---
title: AddDriverContent Method
titleSuffix: Configuration Manager
description: In Configuration Manager, the AddDriverContent Windows Management Instrumentation class method adds a driver to the driver package and replicates the driver content to distribution points.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: f30ff615-6e14-41aa-940d-eb3cd8d51b08
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# AddDriverContent Method in Class SMS_DriverPackage
The `AddDriverContent` Windows Management Instrumentation (WMI) class method, in Configuration Manager, adds a driver to the driver package and replicates the driver content to distribution points.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 AddDriverContent(  
     UInt32 ContentIDs[],  
     String ContentSourcePath[],  
     Boolean bRefreshDPs  
);  
```  

#### Parameters  
 `ContentIDs`  
 Data type: `UInt32` Array  

 Qualifiers: [in]  

 The IDs for content to add to the driver package.  

 `ContentSourcePath`  
 Data type: `String` Array  

 Qualifiers: [in]  

 The source paths where the content files are located. In most cases, these paths should be the same as the settings for the `ContentSourcePath` properties of the [SMS_Driver Server WMI Class](../../../develop/reference/osd/sms_driver-server-wmi-class.md) objects represented by the driver package. The paths can be overridden with local paths if the SMS Provider does not have access to the central site for Configuration Manager.  

 `bRefreshDPs`  
 Data type: `Boolean`  

 Qualifiers: [in, optional]  

 `true`, by default, if driver package content is to be replicated to the distribution points.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  
 An example of the use of this method is provided in [How to Create a Driver Package for a Windows Driver in Configuration Manager](../../../develop/osd/how-to-create-a-driver-package-for-a-windows-driver.md).  

 If the call to this method fails, check the Smsprov.log file on the provider computer for more information.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_DriverPackage Server WMI Class](../../../develop/reference/osd/sms_driverpackage-server-wmi-class.md)   
 [RemoveDriverContent Method in Class SMS_DriverPackage](../../../develop/reference/osd/removedrivercontent-method-in-class-sms_driverpackage.md)   
 [ValidateNewPackageSource Method in Class SMS_DriverPackage](../../../develop/reference/osd/validatenewpackagesource-method-in-class-sms_driverpackage.md)   
 [How to Create a Driver Package for a Windows Driver in Configuration Manager](../../../develop/osd/how-to-create-a-driver-package-for-a-windows-driver.md)
