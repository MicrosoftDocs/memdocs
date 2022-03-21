---
title: RebuildPackage method in class SMS_SoftwareUpdatesPackage
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 0cc4b1e3-7e96-45fe-a1c5-e012aa1af8b3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# RebuildPackage Method in Class SMS_SoftwareUpdatesPackage
The `RebuildPackage` Windows Management Instrumentation (WMI) class method, in Configuration Manager, brings the software updates package to its expected state if files are found to be corrupt or have been deleted.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 RebuildPackage(  
     String ContentSourcePath  
);  
```  

#### Parameters  
 `ContentSourcePath`  
 Data type: `String`  

 Qualifiers: [in, optional]  

 Source path where the content files are located.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_SoftwareUpdatesPackage Server WMI Class](../../../develop/reference/sum/sms_softwareupdatespackage-server-wmi-class.md)   
 [AddUpdateContent Method in Class SMS_SoftwareUpdatesPackage](../../../develop/reference/sum/addupdatecontent-method-in-class-sms_softwareupdatespackage.md)   
 [RemoveContent Method in Class SMS_SoftwareUpdatesPackage](../../../develop/reference/sum/removecontent-method-in-class-sms_softwareupdatespackage.md)
