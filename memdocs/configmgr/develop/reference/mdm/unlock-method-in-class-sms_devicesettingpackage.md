---
title: "Unlock Method"
titleSuffix: "Configuration Manager"
description: "Sets the source site to the current site, unlocking the device setting package in Configuration Manager." 
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 0d714937-63a5-4224-8c2a-16ffd1d25cd3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# Unlock Method in Class SMS_DeviceSettingPackage
The `Unlock` Windows Management Instrumentation (WMI) class method, in Configuration Manager, sets the source site to the current site, unlocking the device setting package.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 Unlock();  
```  

#### Parameters  
 None.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## See Also  
 [SMS_DeviceSettingPackage Server WMI Class](../../../develop/reference/mdm/sms_devicesettingpackage-server-wmi-class.md)   
 [RefreshPkgSource Method in Class SMS_DeviceSettingPackage](../../../develop/reference/mdm/refreshpkgsource-method-in-class-sms_devicesettingpackage.md)   
 [SetSourceSite Method in Class SMS_DeviceSettingPackage](../../../develop/reference/mdm/setsourcesite-method-in-class-sms_devicesettingpackage.md)
