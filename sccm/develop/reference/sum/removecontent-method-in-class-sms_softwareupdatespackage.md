---
title: "RemoveContent Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 36e102e8-7a1f-49c1-9ea8-89e5fc81ef97
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# RemoveContent Method in Class SMS_SoftwareUpdatesPackage
The `RemoveContent` Windows Management Instrumentation (WMI) class method, in Configuration Manager, removes old or unnecessary content from the software updates package.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 RemoveContent(  
     UInt32 ContentIDs[],  
     Boolean bRefreshDPs  
);  
```  

#### Parameters  
 `ContentIDs`  
 Data type: `UInt32` Array  

 Qualifiers: [in]  

 IDs of content to remove from the software updates package.  

 `bRefreshDPs`  
 Data type: `Boolean`  

 Qualifiers: [in, optional]  

 `true`, by default, to replicate package content to the distribution points.  

## Return Values  
 The method returns an exception on failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  
 To determine the content to remove using this method, your application should use [SMS_CIToContent Server WMI Class](../../../develop/reference/sum/sms_citocontent-server-wmi-class.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_SoftwareUpdatesPackage Server WMI Class](../../../develop/reference/sum/sms_softwareupdatespackage-server-wmi-class.md)   
 [AddUpdateContent Method in Class SMS_SoftwareUpdatesPackage](../../../develop/reference/sum/addupdatecontent-method-in-class-sms_softwareupdatespackage.md)   
 [RebuildPackage Method in Class SMS_SoftwareUpdatesPackage](../../../develop/reference/sum/rebuildpackage-method-in-class-sms_softwareupdatespackage.md)
