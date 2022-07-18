---
description: Learn how to use the RemoteContent class method to remove the content for the given content ID from a package.  
title: RemoveContent method in class SMS_ContentPackage
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 94f37a42-380b-4b79-9f07-acd2b8ddfe0e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# RemoveContent Method in Class SMS_ContentPackage
The `RemoveContent` Windows Management Instrumentation (WMI) class method, in Configuration Manager, removes the content for the given content ID from the package.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 RemoveContent(  
     uint32  ContentIDs[],  
     boolean bRefreshDPs[],  
);  
```  

#### Parameters  
 `ContentIDs`  
 Data type: `UInt32` Array  

 Qualifiers: `[in, optional]`  

 Content identifiers for content to be removed.  

 `bRefreshDPs`  
 Data type: `Boolean` Array  

 Qualifiers: `[in]`  

 `true`, if distribution points should be refreshed. The default value is `true`.  

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Application Server WMI Class](../../../../../develop/reference/apps/sms_application-server-wmi-class.md)   
