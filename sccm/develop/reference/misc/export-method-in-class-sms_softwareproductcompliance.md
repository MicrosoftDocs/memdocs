---
title: "Export Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: d8eda89a-7ec0-4612-aa77-7db2c7c48140
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Export Method in Class SMS_SoftwareProductCompliance
The `Export` Windows Management Instrumentation (WMI) class method, in Configuration Manager, exports program compliance information from the database in tab-delimited format. It also returns the number of valid records that were exported.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
UInt32 Export(  
     String ComplianceData,  
     String SourceFilter,  
     String TypeFilter  
);  
```  

#### Parameters  
 `ComplianceData`  
 Data type: **String**  

 Qualifiers: [out]  

 Tab-delimited compliance data. The data is a null-terminated string and each record terminates with a carriage return and line feed character.  

 `SourceFilter`  
 Data type: **String**  

 Qualifiers: [in, optional]  

 Source filter causing the method to export only those records that match the `Source` property.  

 `TypeFilter`  
 Data type: **String**  

 Qualifiers: [in, optional]  

 Type filter causing the method to export only those records that match the compliance `Type` property.  

## Remarks  

> [!NOTE]
>  The filter process is case-insensitive. Do not include either filter (`SourceFilter` or `TypeFilter`) if you want to import all the compliance data.  

## Return Values  
 A `UInt32` data type that indicates the number of valid records exported.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_SoftwareProductCompliance Server WMI Class](../../../develop/reference/misc/sms_softwareproductcompliance-server-wmi-class.md)
