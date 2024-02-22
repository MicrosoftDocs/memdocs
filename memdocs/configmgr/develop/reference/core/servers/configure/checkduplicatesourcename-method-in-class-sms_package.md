---
title: CheckDuplicateSourceName Method
titleSuffix: Configuration Manager
description: The CheckDuplicateSourceName Windows Management Instrumentation (WMI) class method determines if the specified source name is used by another package.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 214c1768-0200-4ecf-b871-cbdc61f8348c
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# CheckDuplicateSourceName Method in Class SMS_Package
The `CheckDuplicateSourceName` Windows Management Instrumentation (WMI) class method, in Configuration Manager, determines if the specified source name is used by another package.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 CheckDuplicateSourceName(  
     String SourceName,  
     String SourceSite,  
     Boolean IsDuplicated,  
     String DupPkgName,  
     String DupPkgID,  
     SInt32 DupPkgType  
);  
```  

#### Parameters  
 `SourceName`  
 Data type: `String`  

 Qualifiers: [in]  

 Source name defined for the package.  

 `SourceSite`  
 Data type: `String`  

 Qualifiers: [in]  

 ID of the package to which to add the source specified by `SourceName`.  

 `IsDuplicated`  
 Data type: `Boolean`  

 Qualifiers: [out]  

 `true` if the source specified by `SourceName` has been used by another package.  

 `DupPkgName`  
 Data type: `String`  

 Qualifiers: [out]  

 Name of the package using the source specified by `SourceName`.  

 `DupPkgID`  
 Data type: `String`  

 Qualifiers: [out]  

 ID of the other package using the source specified by `SourceName`.  

 `DupPkgType`  
 Data type: `SInt32`  

 Qualifiers: [out]  

 Type of package for which the source specified by `SourceName` is duplicated. Possible values are defined for the `PackageType` property of [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md). The default value is 1.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md)   
 [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md)
