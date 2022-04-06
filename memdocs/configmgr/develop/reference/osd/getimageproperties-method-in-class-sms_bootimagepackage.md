---
title: "GetImageProperties Method in SMS_BootImagePackage"
titleSuffix: "Configuration Manager"
description: "The GetImageProperties WMI class method reads all metadata from the specified .wim source file for a boot image to an XML string."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 3aa1d771-6c93-4878-89cc-92d9afe1a350
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# GetImageProperties Method in Class SMS_BootImagePackage
The `GetImageProperties` Windows Management Instrumentation (WMI) class method, in Configuration Manager, reads all metadata from the specified .wim source file for a boot image to an XML string.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 GetImageProperties(  
      String SourceImagePath,  
      String ImageProperty  
);  
```  

#### Parameters  
 `SourceImagePath`  
 Data type: `String`  

 Qualifiers: [in]  

 Path to the .wim source file to query for metadata.  

 `ImageProperty`  
 Data type: `String`  

 Qualifiers: [out]  

 XML document containing the image metadata.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  
 This method accesses the source .wim file metadata by using the `ImageProperty` property of [SMS_BootImagePackage Server WMI Class](../../../develop/reference/osd/sms_bootimagepackage-server-wmi-class.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_BootImagePackage Server WMI Class](../../../develop/reference/osd/sms_bootimagepackage-server-wmi-class.md)   
 [ReloadImageProperties Method in Class SMS_BootImagePackage](../../../develop/reference/osd/reloadimageproperties-method-in-class-sms_bootimagepackage.md)
