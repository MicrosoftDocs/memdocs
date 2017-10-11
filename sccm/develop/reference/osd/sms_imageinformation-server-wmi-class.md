---
title: "SMS_ImageInformation Class"
titleSuffix: "Configuration Manager"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: 90235fe7-fbcd-4fd0-a76c-fa7b389bd5b8searchScope: - ConfigMgr SDK
caps.latest.revision: 15
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_ImageInformation Server WMI Class
The `SMS_ImageInformation` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents all image information in boot image, operating system image, and operating system installer.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ImageInformation : SMS_BaseClass  
{  
    String Architecture;  
    String CreatedBy;  
    String CreationDate;  
    String Description;  
    Boolean EnableLabShell;  
    String HALType;  
    String ImagePath;  
    String ImageOSVersion;  
    UInt32 Index;  
    String Language;  
    String Name;  
    UInt32 ObjectType;  
    String OSVersion;  
    String PackageID;  
    UInt32 PackageType;  
    String ProductType;  
    SInt64 Size;  
    String Version;  
};  
```  

## Methods  
 The `SMS_ImageInformation` class does not define any methods.  

## Properties  
 `Architecture`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Architecture of the boot image.  

 `CreatedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Name of the user who created the image.  

 `CreationDate`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Date and time when the image was created.  

 `Description`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Description of the image.  

 `EnableLabShell`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [lazy]  

 `true` if command-line support is enabled. The default value is `false`.  

 `HALType`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Image HAL type.  

 `ImagePath`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 For internal use only.  

 `ImageOSVersion`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 The operating system version for the default image in the boot WIM file.  

 `Index`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [lazy, read]  

 A one-based number indicating which image in the source WIM file is the boot image.  

 The default value is 1.  

 `Language`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Language of the image.  

 `Name`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Name of the image.  

 `ObjectType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, read]  

 Secured object type.  

|||  
|-|-|  
|14|SMS_OperatingSystemInstallPackage|  
|18|SMS_ImagePackage|  
|19|SMS_BootImagePackage|  

 `OSVersion`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Image operating system version.  

 `PackageID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 A unique, auto-generated key that is used to relate programs, advertisements, and distribution points to the package.  

 `PackageType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, read]  

 Image package type.  

|||  
|-|-|  
|257|PKG_TYPE_IMAGE|  
|258|PKG_TYPE_BOOTIMAGE|  
|259|PKG_TYPE_OSINSTALLIMAGE|  

 `ProductType`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Image product type.  

 `Size`  
 Data type: `SInt64`  

 Access type: Read-only  

 Qualifiers: [read]  

 Image size.  

 `Version`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
