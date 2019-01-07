---
title: "ImportInventoryReport Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 79ae21e0-8d58-4ec0-8cc1-9322031cb582
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# ImportInventoryReport Method in Class SMS_InventoryReport
The `ImportInventoryReport` Windows Management Instrumentation (WMI) class method, in System Center Configuration Manager, imports an inventory class from the MOF file content.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 ImportInventoryReport(     
     string InventoryReportID,  
     uint32 ImportType,  
     string MofBuffer  
);  
```  

#### Parameters  
 `InventoryReportID`  
 Data type: `String`  

 Qualifiers: [in]  

 Inventory report ID.  

 `ImportType`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 Import type. Possible values are:  

|Value|Description|  
|-----------|-----------------|  
|1|ClassOnly: Imports only the inventory class. This option is only available at the central site or a standalone primary site.|  
|2|ReportOnly: Imports only the inventory report.|  
|3|BothClassAndReport: Imports both inventory class definition and inventory report information.|  

 `MofBuffer`  
 Data type: `String`  

 Qualifiers: [in]  

 The MOF content that contains the inventory class or report to import. This is the same format as the Configuration Manager 2007 sms_def.mof file, or the file format that you export from inventory client settings.  

## Return Values  
 An `SInt32`data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md)
