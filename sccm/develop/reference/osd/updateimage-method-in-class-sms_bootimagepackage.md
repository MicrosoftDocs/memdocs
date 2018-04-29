---
title: "UpdateImage Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: edd9c38e-004b-4bf9-9d9b-d8e6b7d4d179
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# UpdateImage Method in Class SMS_BootImagePackage
The `UpdateImage` Windows Management Instrumentation (WMI) class method, in Configuration Manager, creates a copy of the current boot image source .wim file and updates the copy with the most current operating system deployment binaries.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 UpdateImage();  
```  

#### Parameters  
 None.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  
 Your application calls this method only when Configuration Manager is upgrading from an operating system release candidate to an RTM version.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_BootImagePackage Server WMI Class](../../../develop/reference/osd/sms_bootimagepackage-server-wmi-class.md)
