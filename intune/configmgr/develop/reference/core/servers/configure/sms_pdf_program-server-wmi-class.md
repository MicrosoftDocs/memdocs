---
title: SMS_PDF_Program Class
titleSuffix: Configuration Manager
description: The SMS_PDF_Program WMI class is an SMS Provider server class that represents a package definition file (PDF) template from which to create an initialized program.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 5acde161-499a-43f3-9470-a83cebb7a3cd
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_PDF_Program Server WMI Class
The `SMS_PDF_Program` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a package definition file (PDF) template from which to create an initialized program.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_PDF_Program : SMS_BaseClass  
{  
      String CommandLine;  
      String Comment;  
      String DependentProgram;  
      String Description;  
      String DiskSpaceReq;  
      String DriveLetter;  
      UInt32 Duration;  
      UInt8 Icon[];  
      UInt32 IconSize;  
      UInt32 PDFID;  
      UInt32 ProgramFlags;  
      String ProgramName;  
      String Publisher;  
      String Requirements;  
      String WorkingDirectory;  
};  
```  

## Methods  
 The `SMS_PDF_Program` class doesn't define any methods.  

## Properties  
 `CommandLine`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Command that executes when the program is launched.  

 `Comment`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Description of the program displayed in the Configuration Manager console.  

 `DependentProgram`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 A formatted text string defining any program that should be run prior to executing the current program. The format is defined as: \<PackageID>;; \<ProgramName>. The default value is "".  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Description of the program (not displayed in the Configuration Manager console).  

 `DiskSpaceReq`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Approximate disk space that the program requires.  

 `DriveLetter`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [SizeLimit("1"), Range("a-z")]  

 Drive letter (one character in the range from a to z) that the program maps to and runs from. The default value is "".  

 `Duration`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Approximate duration, in minutes, that the program takes to execute.  

 `Icon`  
 Data type: `UInt8` Array  

 Access type: Read/Write  

 Qualifiers: [lazy, large]  

 Icon to associate with the program in the Configuration Manager console.  

 `IconSize`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 Size, in bytes, of the icon. The default value is 0.  

 `PDFID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 ID of the [SMS_PDF_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_pdf_package-server-wmi-class.md) object to which the program belongs.  

 `ProgramFlags`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Flags defining the installation characteristics of the program. See the `ProgramFlags` property of [SMS_Program Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_program-server-wmi-class.md).  

 `ProgramName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Name that uniquely identifies the program.  

 `Publisher`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Manufacturer of the program.  

 `Requirements`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Description of any extra requirements of the program. The default value is "".  

 `WorkingDirectory`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The location from which the program executes. This can be an absolute path on the client or a path relative to the distribution point folder that contains the package. The default value is "".  

## Remarks  
 Class qualifiers for this class include:  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

  Your application can't delete individual programs from the package definition file store. To delete a program, the application must delete the package template and then reload the package template without the program.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
