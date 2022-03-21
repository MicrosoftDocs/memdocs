---
title: "LoadIconForPDF Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 9936a9b1-243b-4bc7-a48c-ee6942b795d1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# LoadIconForPDF Method in Class SMS_PDF_Package
The `LoadIconForPDF` Windows Management Instrumentation (WMI) class method, in Configuration Manager, imports a required icon for a package definition file.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 LoadIconForPDF(  
    UInt32 PDFID,  
     String IconFileName,  
     UInt8 Icon[]  
);  
```  

#### Parameters  
 `PDFID`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 ID of the package definition file to which to add icons. Get this value from the `PDFID` parameter of the [LoadPDF Method in Class SMS_PDF_Package](../../../../../develop/reference/core/servers/configure/loadpdf-method-in-class-sms_pdf_package.md) method.  

 `IconFileName`  
 Data type: `String`  

 Qualifiers: [in, SizeLimit("100")]  

 Full path and file name of a required package definition file icon. Get the icon name from the `RequriedIconNames` parameter of the `LoadPDF` method. Include the path if necessary.  

 `Icon`  
 Data type: `UInt8` Array  

 Qualifiers: [in]  

 Icon to associate with the package.  

## Return Values  
 An `SInt32` data type.  

## Remarks  
 Package definition files can reference icons to be used with the package. These icons are not part of the file and must be loaded separately.  

 Your application must call `LoadIconForPDF` for every icon that [LoadPDF Method in Class SMS_PDF_Package](../../../../../develop/reference/core/servers/configure/loadpdf-method-in-class-sms_pdf_package.md) loads.  

## Example Code  
 For an example that uses the `LoadIconForPDF` method, see [LoadPDF Method in Class SMS_PDF_Package](../../../../../develop/reference/core/servers/configure/loadpdf-method-in-class-sms_pdf_package.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_PDF_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_pdf_package-server-wmi-class.md)
