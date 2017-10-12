---
title: "CheckDuplicateShareName Method"
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
ms.assetid: 305f9dc9-acb0-415d-bc10-369a7f1c8e63searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# CheckDuplicateShareName Method in Class SMS_Package
The `CheckDuplicateShareName` Windows Management Instrumentation (WMI) class method, in System Center Configuration Manager, determines if the specified share name has been used by another package.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 CheckDuplicateShareName(  
     String ShareName,  
     String PackageID,  
     Boolean IsDuplicated,  
      String DupPkgName,  
     String DupPkgID,  
     SInt32 DupPkgType  
);  
```  

#### Parameters  
 `ShareName`  
 Data type: `String`  

 Qualifiers: [in]  

 Share name defined for the package.  

 `PackageID`  
 Data type: `String`  

 Qualifiers: [in]  

 ID of the package to which to add the share specified by `ShareName`.  

 `IsDuplicated`  
 Data type: `Boolean`  

 Qualifiers: [out]  

 `true` if the share specified by `ShareName` has been used by another package.  

 `DupPkgName`  
 Data type: `String`  

 Qualifiers: [out]  

 Name of the package using the share specified by `ShareName`.  

 `DupPkgID`  
 Data type: `String`  

 Qualifiers: [out]  

 ID of the other package using the share specified by `ShareName`.  

 `DupPkgType`  
 Data type: `SInt32`  

 Qualifiers: [out]  

 Type of package for which the share specified by `ShareName` is duplicated. Possible values are defined for the `PackageType` property of [SMS_PackageBaseclass Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md). The default value is 1.  

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
