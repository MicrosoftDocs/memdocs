---
title: "SMS_SoftwareProductCompliance Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: d4d6cae0-271e-4878-82ab-00b6734147e8
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_SoftwareProductCompliance Server WMI Class
The `SMS_SoftwareProductCompliance` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that contains compliance information about a software product.  

 The following syntax is not defined in Managed Object Format (MOF) code.  

## Syntax  

```  
Class SMS_SoftwareProductCompliance : SMS_BaseClass  
{  
   String  Category;  
   String  Comment;  
   String  FileName;  
   UInt32 FileSize;  
   String  ProdCompany;  
   String  ProdLang;  
   String  ProdName;  
   String  ProdPlatform;  
   String  ProdRev;  
   String  ProdVer;  
   UInt32 RecordID;  
   UInt32 ResProdLangID;  
   String  ResProdName;  
   String  ResProdVer;  
   String  Source;  
   String  Type;  
   String  URL;  
};  
```  

## Methods  
 The following table lists the methods in `SMS_SoftwareProductCompliance`.  

|Method|Description|  
|------------|-----------------|  
|[DeleteByQuery Method in Class SMS_SoftwareProductCompliance](../../../develop/reference/misc/deletebyquery-method-in-class-sms_softwareproductcompliance.md)|Deletes a group of records specified by a WQLSELECT statement. It returns the number of rows deleted.|  
|[Export Method in Class SMS_SoftwareProductCompliance](../../../develop/reference/misc/export-method-in-class-sms_softwareproductcompliance.md)|Exports program compliance information from the database in tab-delimited format. It returns the number of records exported.|  
|[Import Method in Class SMS_SoftwareProductCompliance](../../../develop/reference/misc/import-method-in-class-sms_softwareproductcompliance.md)|Overwrites any matching record of program compliance data in the database. The data is in tab-delimited format. It returns the number of valid records imported.|  
|[ProcessInBox Method in Class SMS_SoftwareProductCompliance](../../../develop/reference/misc/processinbox-method-in-class-sms_softwareproductcompliance.md)|Imports all files found in the software product compliance inbox. It returns the number of records imported.|  

## Properties  
 `Category`  
 Data type: **String**  

 Access type: Read/Write  

 Qualifiers: None  

 Product compliance category. This property cannot be left blank. For the "Year 2000" value of `Type`, the possible values for `Category` are:  

- Compliant  

- Compliant with minor issues  

- Compliant with prerequisites  

- Compliant with minor issues with prerequisites  

- Not compliant  

- Testing yet to be completed  

- Will not test  

  `Comment`  
  Data type: **String**  

  Access type: Read/Write  

  Qualifiers: None  

  Additional information about product compliance. When an update for the product is available, but not necessary to reach compliance, this property contains the string "Fixes available".  

  `FileName`  
  Data type: **String**  

  Access type: Read/Write  

  Qualifiers: None  

  Executable file name, not including the path.  

  `FileSize`  
  Data type: **UInt32**  

  Access type: Read/Write  

  Qualifiers: None  

  Size, in bytes, of the file specified in `FileName`.  

  `ProdCompany`  
  Data type: **String**  

  Access type: Read/Write  

  Qualifiers: None  

  The name of the company that produced the product.  

  `ProdLang`  
  Data type: **String**  

  Access type: Read/Write  

  Qualifiers: None  

  Product language. If this property is blank, the [Import Method in Class SMS_SoftwareProductCompliance](../../../develop/reference/misc/import-method-in-class-sms_softwareproductcompliance.md) tries to create the language String by converting the `ResProdLangID` value to a text string .  

  `ProdName`  
  Data type: **String**  

  Access type: Read/Write  

  Qualifiers: None  

  Product name. If this property is blank, the `Import` method creates the name by using `ResProdName` or by using `FileName` and `FileSize`.  

  `ProdPlatform`  
  Data type: **String**  

  Access type: Read/Write  

  Qualifiers: None  

  Platform for which the product was written.  

  `ProdRev`  
  Data type: **String**  

  Access type: Read/Write  

  Qualifiers: None  

  Specific revision within the product version.  

  `ProdVer`  
  Data type: **String**  

  Access type: Read/Write  

  Qualifiers: None  

  Version level of the product. If this property is blank, the `Import` method creates the version by using the `ResProdVer` property.  

  `RecordID`  
  Data type: **UInt32**  

  Access type: Read-only  

  Qualifiers: None  

  Unique ID for the instance.  

  `ResProdLangID`  
  Data type: **UInt32**  

  Access type: Read/Write  

  Qualifiers: None  

  Product language ID, taken from the executable file resource or the DLL resource. A locale ID of 65535 (xFFFF) is a special value used by the predefined Configuration Manager software inventory queries. This value has the effect of matching any language ID found in software discovery.  

  `ResProdName`  
  Data type: **String**  

  Access type: Read/Write  

  Qualifiers: None  

  Product name from the executable file resource or the DLL resource. The name is often different from the name specified in `ProdName`.  

  `ResProdVer`  
  Data type: **String**  

  Access type: Read/Write  

  Qualifiers: None  

  Version from the executable file resource or the DLL resource. The version is often different from the version specified in `ProdVer`.  

  `Source`  
  Data type: **String**  

  Access type: Read/Write  

  Qualifiers: None  

  Source of the compliance information. Multiple sources can supply compliance information about the same `ProdName` property. If this property is blank, the `Import` method creates the data source by using the domain\user name of the user.  

  `Type`  
  Data type: **String**  

  Access type: Read/Write  

  Qualifiers: None  

  Type of compliance. This property cannot be left blank.  

  Example: "Year 2000"  

  `URL`  
  Data type: **String**  

  Access type: Read/Write  

  Qualifiers: None  

  URL (Web site address) where additional information about the product, its compliance, and any updates might be found.  

## Remarks  
 Use this class to track whether your software meets company or industry standards or supports known date and currency issues.  

 [Import Method in Class SMS_SoftwareProductCompliance](../../../develop/reference/misc/import-method-in-class-sms_softwareproductcompliance.md) and [ProcessInBox Method in Class SMS_SoftwareProductCompliance](../../../develop/reference/misc/processinbox-method-in-class-sms_softwareproductcompliance.md) are used to load compliance data into the Configuration Manager database. These methods import software product compliance data from a tab-delimited text file supplied by the product vendor or built by the system administrator. The file can contain information from one or more sources.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Resource Management Server WMI Classes](../../../develop/reference/core/clients/manage/configuration-manager-resource-management-server-wmi-classes.md)
