---
description: Article outlining the use of SMS_PDFPkgToPDFProgram class in Configuration Manager.
title: "SMS_PDFPkgToPDFProgram_a Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: d60b8239-d255-4f93-a856-bb327067fb4f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_PDFPkgToPDFProgram_a Server WMI Class
The `SMS_PDFPkgToPDFProgram_a` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that uses the `PDFID` property to relate a [SMS_PDF_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_pdf_package-server-wmi-class.md) object to an [SMS_PDF_Program Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_pdf_program-server-wmi-class.md) object that is part of the package.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_PDFPkgToPDFProgram_a : SMS_BaseAssociation  
{  
      ref:SMS_PDF_Package PDF_Package;  
      ref:SMS_PDF_Program PDF_Program;  
};  
```  

## Methods  
 The `SMS_PDFPkgToPDFProgram_a` class does not define any methods.  

## Properties  
 `PDF_Package`  
 Data type: `ref:SMS_PDF_Package`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Reference to an [SMS_PDF_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_pdf_package-server-wmi-class.md) object path.  

 `PDF_Program`  
 Data type: `ref:SMS_PDF_Program`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Reference to an [SMS_PDF_Program Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_pdf_program-server-wmi-class.md) object path.  

## Remarks  
 Class qualifiers for this class include:  

- Association: ToInstance  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_PDF_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_pdf_package-server-wmi-class.md)   
 [SMS_PDF_Program Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_pdf_program-server-wmi-class.md)
