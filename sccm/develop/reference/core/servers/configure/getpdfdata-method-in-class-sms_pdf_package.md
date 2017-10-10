---
title: "GetPDFData Method"
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
ms.assetid: 1c071dbe-d601-4448-8e8f-3bb29398cd8csearchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# GetPDFData Method in Class SMS_PDF_Package
The `GetPDFData` Windows Management Instrumentation (WMI) class method, in Configuration Manager, produces [SMS_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md) and [SMS_Program Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_program-server-wmi-class.md) objects from a loaded package definition file.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 GetPDFData(  
     UInt32 PDFID,  
     SMS_Package PackageData,  
      SMS_Program ProgramData[]  
);  
```  

#### Parameters  
 `PDFID`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 ID of the package definition file to be retrieved. Get this value from the [SMS_PDF_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_pdf_package-server-wmi-class.md) class.  

 `PackageData`  
 Data type: `SMS_Package`  

 Qualifiers: [out]  

 An [SMS_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md) object produced from the package definition file.  

 `ProgramData`  
 Data type: `SMS_Program` Array  

 Qualifiers: [out]  

 [SMS_Program Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_program-server-wmi-class.md) objects produced from the package definition file.  

## Return Values  
 An `SInt32` data type that is one of the following bit-field warning flags.  

|Flag|Description|  
|----------|-----------------|  
|WARN_BAD_RUN (0)|Invalid run information specified.|  
|WARN_BAD_RESTART (1)|Invalid restart information specified.|  
|WARN_BAD_CANRUNWHEN (2)|Invalid CanRunWhen information specified.|  
|WARN_BAD_ASSIGNMENT (3)|Invalid assignment information specified.|  
|WARN_BAD_DEPENDPROG (4)|Invalid DependentProgram information specified.|  
|WARN_BAD_SPECIFYDRIVE (5)|Invalid SpecifyDrive information specified.|  
|WARN_BAD_ESTDISKSPACE (6)|Invalid EstimatedDiskSpace information specified.|  
|WARN_NO_SUPPCLINFO (7)|No SupportedClients information specified.|  
|WARN_BAD_SUPPCLINFO (8)|Invalid SupportedClients information specified.|  
|WARN_VER1PDF (9)|Version 1.0 file used.|  
|WARN_REMPRONOUKEY(10)|The remove program is set, but no uninstall Key is given.|  

## Example Code  
 For an example that uses this method, see [How to Create a Package Using a PDF Template](../../../../../develop/core/servers/configure/how-to-create-a-package-by-using-a-package-definition-file-template.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_PDF_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_pdf_package-server-wmi-class.md)
