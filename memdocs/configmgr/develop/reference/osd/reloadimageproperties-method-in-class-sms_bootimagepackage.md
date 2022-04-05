---
title: ReloadImageProperties method in class SMS_BootImagePackage
titleSuffix: "Configuration Manager"
description: "Reloads image metadata from a boot image source .wim file and synchronizes the metadata with the database."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 91abc6f0-6ed7-485e-af9c-e4e8f2832f16
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# ReloadImageProperties Method in Class SMS_BootImagePackage
The `ReloadImageProperties` Windows Management Instrumentation WMI class method, in Configuration Manager, reloads image metadata from a boot image source .wim file and synchronizes the metadata with the database.  

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
 The application uses this method if the administrator changes the boot image source .wim file outside of the Configuration Manager console. The application should:  

1.  Establish a connection to the SMS Provider. For more information, see [SMS Provider fundamentals](../../core/understand/sms-provider-fundamentals.md).  

2.  Obtain the [SMS_BootImagePackage Server WMI Class](../../../develop/reference/osd/sms_bootimagepackage-server-wmi-class.md) object to update.  

3.  Call `ReloadImageProperties`.  

4.  Commit the `SMS_BootImagePackage` object.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_BootImagePackage Server WMI Class](../../../develop/reference/osd/sms_bootimagepackage-server-wmi-class.md)   
 [UpdateImage Method in Class SMS_BootImagePackage](../../../develop/reference/osd/updateimage-method-in-class-sms_bootimagepackage.md)
