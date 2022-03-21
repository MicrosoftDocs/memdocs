---
title: "AddUpdateContent Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: e35c4bae-d916-4e11-82a2-09643dd239f3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# AddUpdateContent Method in Class SMS_SoftwareUpdatesPackage
The `AddUpdateContent` Windows Management Instrumentation (WMI) class method, in Configuration Manager, downloads content to a software update package and replicates the content to distribution points.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 AddUpdateContent(  
     UInt32 ContentIDs[],  
     String ContentSourcePath[],  
     Boolean bRefreshDPs  
);  
```  

#### Parameters  
 `ContentIDs`  
 Data type: `UInt32` Array  

 Qualifiers: [in]  

 IDs of contents to add to the software updates package.  

 `ContentSourcePath`  
 Data type: `String` Array  

 Qualifiers: [in]  

 The source path where the content files are located.  

 `bRefreshDPs`  
 Data type: `Boolean`  

 Qualifiers: [in, optional]  

 `true` (default) to replicate package content to the distribution points.  

## Return Values  
 The method returns an exception on failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  
 This method first creates the [SMS_SoftwareUpdatesPackage Server WMI Class](../../../develop/reference/sum/sms_softwareupdatespackage-server-wmi-class.md) object and then adds the indicated content. Your application can use [SMS_CIToContent Server WMI Class](../../../develop/reference/sum/sms_citocontent-server-wmi-class.md) and [SMS_CIContentFiles Server WMI Class](../../../develop/reference/sum/sms_cicontentfiles-server-wmi-class.md) to determine the content.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_SoftwareUpdatesPackage Server WMI Class](../../../develop/reference/sum/sms_softwareupdatespackage-server-wmi-class.md)   
 [SMS_CIToContent Server WMI Class](../../../develop/reference/sum/sms_citocontent-server-wmi-class.md)   
 [SMS_CIContentFiles Server WMI Class](../../../develop/reference/sum/sms_cicontentfiles-server-wmi-class.md)   
 [RebuildPackage Method in Class SMS_SoftwareUpdatesPackage](../../../develop/reference/sum/rebuildpackage-method-in-class-sms_softwareupdatespackage.md)   
 [RemoveContent Method in Class SMS_SoftwareUpdatesPackage](../../../develop/reference/sum/removecontent-method-in-class-sms_softwareupdatespackage.md)
