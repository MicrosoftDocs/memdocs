---
title: "CleanupHierarchyData Method"
description: "The CleanupHierarchyData Windows Management Instrumentation (WMI) class method cleans up hierarchy data." 

ms.date: "09/20/2016"
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3


---
# CleanupHierarchyData Method in Class SMS_MigrationSiteMapping
The `CleanupHierarchyData` Windows Management Instrumentation (WMI) class method, in Configuration Manager, cleans up hierarchy data.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 CleanupHierarchyData(  
     UInt32 siteID   
);  
```  

#### Parameters  
 `siteID`  
 Data type: `UInt32` Array  

 Qualifiers: [in]  

 Site ID of the Configuration Manager site.  

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../develop/core/reqs/server-development-requirements.md).  

## See also

[SMS_MigrationSiteMapping Server WMI Class](../../../../develop/reference/core/migration/sms_migrationsitemapping-server-wmi-class.md)
