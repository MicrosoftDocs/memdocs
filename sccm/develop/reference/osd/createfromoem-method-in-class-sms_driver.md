---
title: "CreateFromOEM Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: ff294184-6e2f-4be1-b1db-44ccd82d18db
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# CreateFromOEM Method in Class SMS_Driver
The `CreateFromOEM` Windows Management Instrumentation (WMI) class method, in Configuration Manager, creates a set of mass-storage [SMS_Driver Server WMI Class](../../../develop/reference/osd/sms_driver-server-wmi-class.md) objects referenced by the specified Txtsetup.oem file.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 CreateFromOEM(  
      String DriverPath,  
      String OEMFile,  
      SMS_Driver Drivers[]  
);  
```  

#### Parameters  
 `DriverPath`  
 Data type: `String`  

 Qualifiers: [in]  

 Universal Naming Convention (UNC) path containing the driver content.  

 `OEMFile`  
 Data type: `String`  

 Qualifiers: [in]  

 Relative path of the Txtsetup.oem file.  

 `Drivers`  
 Data type: `SMS_Driver Array`  

 Qualifiers: [out]  

 An array of drivers with a complete driver catalog.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure. The error values are available in the [SMS_ExtendedStatus Server WMI Class](../../../develop/reference/misc/sms_extendedstatus-server-wmi-class.md) error object. For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

 This method returns successfully if at least one of the files referenced by the Txtsetup.oem file is valid.  

 Possible error values include, but are not limited to, the following:  

 0  
 Success  

 13  
 The Txtsetup.oem file is invalid.  

 All drivers referenced by the Txtsetup.oem file are invalid.  

 2  
 The SMS provider cannot access the Txtsetup.oem file.  

 1633  
 All drivers referenced by the Txtsetup.oem file are valid but do not support any platforms supported by Configuration Manager.  

 183  
 All drivers referenced by the Txtsetup.oem file have already been imported.  

 All drivers referenced by the Txtsetup.oem file have another type of error. See the OSDDriverCatalog.log file on the provider computer for more information.  

## Remarks  
 To support pre-Windows Vista operating system deployments, Configuration Manager uses boot-critical mass storage device drivers. This type of driver is furnished in the form of a Txtsetup.oem file supplied on a disk. The file contains the following information:  

- Hardware components supported by the file  

- Files to copy from the distribution disk for each component  

- Registry keys and values to create for each component  

  A mass storage device driver file must be installed before setup on a pre-Windows Vista operating system deployment.  

> [!NOTE]
>  Your application should create a driver only by calling this method or the [CreateFromINF Method in Class SMS_Driver](../../../develop/reference/osd/createfrominf-method-in-class-sms_driver.md). It should never create a driver directly.  

 Your application calls this method with a driver Txtsetup.oem file and file path. The method examines the supplied information and creates an array of new [SMS_Driver Server WMI Class](../../../develop/reference/osd/sms_driver-server-wmi-class.md) objects, one for each referenced .inf file.  

 This method generates [SMS_Driver Server WMI Class](../../../develop/reference/osd/sms_driver-server-wmi-class.md) objects with System Definition Model (SDM) package XML defined, and allows your application to make property changes before they are saved.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Driver Server WMI Class](../../../develop/reference/osd/sms_driver-server-wmi-class.md)
