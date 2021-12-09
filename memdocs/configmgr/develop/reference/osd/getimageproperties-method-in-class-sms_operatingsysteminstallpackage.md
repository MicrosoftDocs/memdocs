---
title: "GetImageProperties Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: d7ce0984-1790-4030-bc69-09c2a7433821
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# GetImageProperties Method in Class SMS_OperatingSystemInstallPackage
The `GetImageProperties` Windows Management Instrumentation (WMI) class method, in Configuration Manager, reads all metadata from the specified .wim source file to an XML string.  

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

 The path to the source file to query for metadata.  

 `ImageProperty`  
 Data type: `String`  

 Qualifiers: [out]  

 The XML string defining the metadata.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  
 This method accesses the source .wim file metadata by using the `ImageProperty` property of [SMS_OperatingSystemInstallPackage Server WMI Class](../../../develop/reference/osd/sms_operatingsysteminstallpackage-server-wmi-class.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_OperatingSystemInstallPackage Server WMI Class](../../../develop/reference/osd/sms_operatingsysteminstallpackage-server-wmi-class.md)   
 [ReloadImageProperties Method in Class SMS_OperatingSystemInstallPackage](../../../develop/reference/osd/reloadimageproperties-method-in-class-sms_operatingsysteminstallpackage.md)
