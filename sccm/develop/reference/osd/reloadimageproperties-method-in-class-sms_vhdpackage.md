---
title: "ReloadImageProperties Method in SMS_VhdPackage"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: dc8cdcda-5519-4555-87a1-09c875ffa8d1
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# ReloadImageProperties Method in Class SMS_VhdPackage
The `ReloadImageProperties` Windows Management Instrumentation (WMI) class method, in Configuration Manager, reloads image metadata from a VHD source file and synchronizes the metadata with the database.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 ReloadImageProperties();  
```  

#### Parameters  
 None.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  
 For an example of the use of this method, see [How to Update an Operating System Image Package in Configuration Manager](../../../develop/osd/how-to-update-an-operating-system-image-package.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_VhdPackage Server WMI Class](../../../develop/reference/osd/sms_vhdpackage-server-wmi-class.md)   
 [GetImageProperties Method in Class SMS_VhdPackage](../../../develop/reference/osd/getimageproperties-method-in-class-sms_vhdpackage.md)   
 [How to Update an Operating System Image Package in Configuration Manager](../../../develop/osd/how-to-update-an-operating-system-image-package.md)
