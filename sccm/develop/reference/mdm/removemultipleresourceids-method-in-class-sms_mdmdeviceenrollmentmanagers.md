---
title: "RemoveMultipleResourceIds Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: e90daafd-62cd-4939-ad9b-ec65f92eb692
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# RemoveMultipleResourceIds Method in Class SMS_MDMDeviceEnrollmentManagers
The `RemoveMultipleResourceIds` Windows Management Instrumentation (WMI) class method, in Configuration Manager, deletes multiple resource IDs.  

## Syntax  

```  
 sint32 RemoveMultipleResourceIds(  
     UInt32 ResourceIds  
);  

```  

#### Parameters  
 `ResourceIds`  
 Data type: `UInt32 Array`  

 Qualifiers: [in]  

 Resource IDs.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_MDMDeviceEnrollmentManagers Server WMI Class](../../../develop/reference/mdm/sms_mdmdeviceenrollmentmanagers-server-wmi-class.md)   
 [Mobile Device Management Server WMI Classes](../../../develop/reference/mdm/mobile-device-management-server-wmi-classes.md)
