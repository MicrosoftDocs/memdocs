---
title: "ProcessInBox Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: f47e1a8e-387d-44be-b45f-8e75c19485a9
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# ProcessInBox Method in Class SMS_SoftwareProductCompliance
The `ProcessInBox` Windows Management Instrumentation (WMI) class method, in Configuration Manager, imports all records, valid or invalid, found in the Software Product Compliance inbox, which is located in the \\*Smsinstalldir*\Y2k directory.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
UInt32 ProcessInBox(  
     UInt32 TotalRecordsProcessed  
);  
```  

#### Parameters  
 `TotalRecordsProcessed`  
 Data type: **UInt32**  

 Qualifiers: [out]  

 Number of records, valid or invalid, that were found in the Software Product Compliance inbox.  

## Remarks  
 Configuration Manager uses this method at startup to load the compliance data when the table is empty. Processed files are moved to the \\*Smsinstalldir*\Y2k\Loaded directory. The method does not stop when errors are encountered. The only way it can determine if an error occurred is to compare the number of records processed to the number of records successfully imported. It returns the number of valid records imported.  

## Return Values  
 A `UInt32` data type that indicates the number of valid records imported.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_SoftwareProductCompliance Server WMI Class](../../../develop/reference/misc/sms_softwareproductcompliance-server-wmi-class.md)
