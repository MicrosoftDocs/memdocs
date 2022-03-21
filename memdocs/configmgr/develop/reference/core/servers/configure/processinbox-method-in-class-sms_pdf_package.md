---
title: "ProcessInBox Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: ab2245c3-f676-47cc-82ea-f1787abf9b79
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# ProcessInBox Method in Class SMS_PDF_Package
The `ProcessInBox` Windows Management Instrumentation (WMI) class method, in Configuration Manager, imports package definition files from the package definition file inbox.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 ProcessInBox();  
```  

#### Parameters  
 None.  

## Return Values  
 An `SInt32` data type that is the number of package definition files successfully loaded.  

## Remarks  
 This method processes all .pdf and .sms files found in the \\*Smsinstalldir*\Scripts\\<*localeid*>\Pdfstore\Load inbox. Successfully processed files are then removed and placed in the package definition file store. Files that fail to load, however, remain in the load directory.  

 Configuration Manager uses this method at startup to load package definition file templates if the Configuration Manager tables are empty. Icons defined in the package definition file for the package or programs must exist in the load directory at the time the method is called.  

 When your application imports a package definition file that has the same `Name`, `Publisher`, `Version`, and `Language` properties as an existing package definition file, the existing package definition file is overwritten, including file icons and programs. The value specified by the `PDFID` parameter is retained.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_PDF_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_pdf_package-server-wmi-class.md)
