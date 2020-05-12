---
title: "CreateFromINFs Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 5377ef9c-ab77-4ffd-bca8-d62d13d24384
author: aczechowski
ms.author: aaroncz
manager: dougeby


---
# CreateFromINFs Method in Class SMS_Driver
The `CreateFromINFs` Windows Management Instrumentation (WMI) class method, in Configuration Manager, creates [SMS_Driver Server WMI Class](../../../develop/reference/osd/sms_driver-server-wmi-class.md) objects based on information from the specified source path and one or more Microsoft Windows .inf files.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 CreateFromINFs (  
    String DriverPath,   
    String INFFiles[],   
    SMS_Driver Drivers[]  
);  

```  

#### Parameters  
 `DriverPath`  
 Data type: `String`  

 Qualifiers: [in]  

 Valid Universal Naming Convention (UNC) network path to the folder that contains the driver contents. For example, \\\Servers\Driver\VideoDriver.  

 `INFFiles`  
 Data type: `String Array`  

 Qualifiers: [in]  

 The names of the INF files.  

 `Drivers`  
 Data type: `SMS_Driver Array`  

 Qualifiers: [out]  

 An array of [SMS_Driver Server WMI Class](../../../develop/reference/osd/sms_driver-server-wmi-class.md) objects with a complete driver catalog.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure. The error values are available in the [SMS_ExtendedStatus Server WMI Class](../../../develop/reference/misc/sms_extendedstatus-server-wmi-class.md) error object. For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

 Possible error values include, but are not limited to, the following:  

 0  
 Success  

 13  
 The driver is invalid  

 1633  
 The driver is valid but does not support any platforms supported by Configuration Manager.  

 2  
 The SMS Provider cannot access the network share.  

 183  
 The driver has already been imported.  

 To find out specifics of an error, see the OSDDriverCatalog.log file.  

## Remarks  
 A driver is represented by an information file (INF). The INF file is a text file that specifies the files that need to be present or downloaded for the operating system to run. The information in this type of file provides installation instructions that the Internet Component Download service provided in Microsoft Internet Explorer 3.0 or later uses to install and register software components that are downloaded from the Internet, in addition to any files required by the components.  

> [!NOTE]
>  Your application should create a driver only by calling this method or the [CreateFromOEM Method in Class SMS_Driver](../../../develop/reference/osd/createfromoem-method-in-class-sms_driver.md). It should never create a driver directly.  

 This method creates a new [SMS_Driver Server WMI Class](../../../develop/reference/osd/sms_driver-server-wmi-class.md) object.  

 Once created, the [SMS_Driver Server WMI Class](../../../develop/reference/osd/sms_driver-server-wmi-class.md)`SDMPackageXML` contains the driver definition XML. To set the display information used by the Configuration Manager console for the driver, you need to set the localization information in the [SMS_Driver Server WMI Class](../../../develop/reference/osd/sms_driver-server-wmi-class.md)`LocalizedInformation` property. The driver name used by the display from is available in [SMS_Driver Server WMI Class](../../../develop/reference/osd/sms_driver-server-wmi-class.md)`SDMPackageXML` property XML. For more information, see How to Import a Windows Driver Described by an INF File into Configuration Manager.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Driver Server WMI Class](../../../develop/reference/osd/sms_driver-server-wmi-class.md)
