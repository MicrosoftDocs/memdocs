---
title: "SMS_PDF_Package Class"
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
ms.assetid: fa8d0144-76bb-47de-916f-ea6e7f39b8d0searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_PDF_Package Server WMI Class
The `SMS_PDF_Package` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a package definition file (PDF) template from which to create an initialized package.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_PDF_Package : SMS_BaseClass  
{  
      UInt8 Icon[];  
      UInt32 IconSize;  
      String Language;  
      String Name;  
      String PDFFileName;  
      UInt32 PDFID;  
      String Publisher;  
    String RequiredIconNames[];  
      UInt32 Status;  
      String Version;  
};  
```  

## Methods  
 The following table lists the methods in the `SMS_PDF_Package` class.  

|Method|Description|  
|------------|-----------------|  
|[GetPDFData Method in Class SMS_PDF_Package](../../../../../develop/reference/core/servers/configure/getpdfdata-method-in-class-sms_pdf_package.md)|Gets `SMS_Package` and `SMS_Program` objects for a loaded package definition file.|  
|[LoadIconForPDF Method in Class SMS_PDF_Package](../../../../../develop/reference/core/servers/configure/loadiconforpdf-method-in-class-sms_pdf_package.md)|Imports a required icon for a package definition file.|  
|[LoadPDF Method in Class SMS_PDF_Package](../../../../../develop/reference/core/servers/configure/loadpdf-method-in-class-sms_pdf_package.md)|Imports a package definition file into the package definition file store.|  
|[ProcessInBox Method in Class SMS_PDF_Package](../../../../../develop/reference/core/servers/configure/processinbox-method-in-class-sms_pdf_package.md)|Imports package definition files from the package definition file inbox.|  

## Properties  
 `Icon`  
 Data type: `UInt8` Array  

 Access type: Read/Write  

 Qualifiers: [lazy, large]  

 Icon to associate with the package in the Configuration Manager console.  

 `IconSize`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 Size, in bytes, of the icon. The default value is 0.  

 `Language`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Language for the package, for example, English.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the package.  

 `PDFFileName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [SizeLimit("100")]  

 File name of the package definition file. The file name does not include the .sms file name extension.  

 `PDFID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Unique auto-generated ID for the package definition file.  

 `Publisher`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Manufacturer of the package.  

 `RequiredIconNames`  
 Data type: `String` Array  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 Icons still required to be loaded.  

 `Status`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [lazy, Enumeration]  

 Load status of the package definition file. Possible values are:  

|||  
|-|-|  
|0|Loaded|  
|1|RequiresIcon|  

 `Version`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Version number of the package.  

## Remarks  
 Class qualifiers for this class include:  

-   Read (read-only)  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

 This class contains methods that store the package definition file template in the package definition file store and that produce [SMS_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md) objects and [SMS_Program Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_program-server-wmi-class.md) objects from the template.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Software Distribution Server WMI Classes](../../../../../develop/reference/core/servers/configure/software-distribution-server-wmi-classes.md)   
 [SMS_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md)   
 [SMS_Program Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_program-server-wmi-class.md)
