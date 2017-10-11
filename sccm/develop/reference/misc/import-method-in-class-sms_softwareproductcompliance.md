---
title: "Import Method"
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
ms.assetid: 7fe387a8-9ab5-43aa-b50e-d8ca5fb5825csearchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# Import Method in Class SMS_SoftwareProductCompliance
The `Import` Windows Management Instrumentation (WMI) class method, in Configuration Manager, overwrites any matching records of program-compliance data in the database. It also returns the number of records that were imported.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
UInt32 Import(  
     String ComplianceData,   
     String SourceFilter,   
     String TypeFilter,  
     Boolean ReportErrors,  
     UInt32 TotalRecordsProcessed  
);  
```  

#### Parameters  
 `ComplianceData`  
 Data type: **String**  

 Qualifiers: [in]  

 Tab-delimited compliance data. The data is passed as a null-terminated string. Each record terminates with a carriage return and line feed character.  

 `SourceFilter`  
 Data type: **String**  

 Qualifiers: [in, optional]  

 Source filter used by the method to import only those records that match the source value, limiting them to a single data source.  

 `TypeFilter`  
 Data type: **String**  

 Qualifiers: [in, optional]  

 If a compliance type, such as "Year 2000", is set in `TypeFilter`,the method imports only those records matching the compliance `Type` property.  

 `ReportErrors`  
 Data type: **Boolean**  

 Qualifiers: [in, optional]  

 `true`, by default, if the import process stops on the first error and performs a rollback on the database, that is, removes all inserted and updated compliance data. If this parameter is set to `false`, the import process continues when errors occur.  

 `TotalRecordsProcessed`  
 Data type: **UInt32**  

 Qualifiers: [out]  

 Total number of records imported, valid or invalid.  

## Remarks  

> [!NOTE]
>  The filter process is case-insensitive. Do not include either filter (`SourceFilter` or `TypeFilter`) if you want to import all the compliance data.  

## Return Values  
 A `UInt32` data type that indicates the number of valid records imported.  

 The method sets the `ErrorCode` property of [SMS_ExtendedStatus Class](../../../develop/reference/misc/sms_extendedstatus-server-wmi-class.md) to 0x40441218 (E_INT_READ_LINE &#124; R_FIELDNO) when the method is unable to process a record in the file. The `ObjectInfo` property identifies the record number (excluding blank lines) that is in error. The `CauseInfo` property contains a number representing the field in the record that caused the error. The field numbers start from zero.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_SoftwareProductCompliance Server WMI Class](../../../develop/reference/misc/sms_softwareproductcompliance-server-wmi-class.md)
